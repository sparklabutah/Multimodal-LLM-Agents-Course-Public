---
layout: page
title: Assignments
permalink: /assignments/
---

These assignments are adapted from the [Hugging Face Agents Course](https://huggingface.co/learn/agents-course/). In this self-paced version of the course, they are **completely optional** — use them for hands-on practice if you'd like.

You can also download the original instructions: [Assignment 1]({{ site.baseurl }}/Assignments/HW0.docx) · [Assignment 2]({{ site.baseurl }}/Assignments/HW1_instructions.docx) · [Assignment 3]({{ site.baseurl }}/Assignments/HW2_instructions.docx)

---

## Assignment 1: Setting Up an HF Agent

Read through [Unit 1 of the HF Agents Course](https://huggingface.co/learn/agents-course/en/unit1/tutorial) and complete the first hands-on exercise setting up an agent.

This is a simple assignment to get you set up with HF agent frameworks and your workflow for the rest of the assignments.

**To complete this assignment, create a Jupyter notebook containing:**
- All of the code that the tutorial asks you to write, with cell outputs
- Written responses to the following questions:
  - How do you feel about the course so far? Are you clear on what the course is about and what you need to do?
  - What topics in the course excite you the most right now?
  - Initial thoughts on the Hugging Face tutorial. Was it clear how to set this up? Is this helpful for your understanding of how to implement agents?

You can use Google Colab or a local environment. Note: `app.py` has dependencies with other files in the project, so it's recommended to clone the whole project into your workspace before modifying its code.

---

## Assignment 2: Building Coding and Tool Calling Agents

Read through Unit 2.1 of the HF Agents Course:
- [Code Agents](https://huggingface.co/learn/agents-course/en/unit2/smolagents/code_agents)
- [Tool Calling Agents](https://huggingface.co/learn/agents-course/en/unit2/smolagents/tool_calling_agents)
- [Tools (optional deeper dive)](https://huggingface.co/learn/agents-course/en/unit2/smolagents/tools)

**Goals:**
- Build a `CodeAgent` that takes actions by generating Python tool-call code
- Build a `ToolCallingAgent` that takes actions by generating structured tool calls (JSON)
- Define and use tools with clear interfaces (name, description, typed inputs/outputs)

**Instructions:**

You may work locally (recommended for stability) or use Colab. Note: if using larger models like Qwen 80B, Colab may require larger runtime sessions.

Set up your HF token if you want to use the HF Hub and inference API.

**CodeAgent:** Create a `CodeAgent` that completes a non-trivial task. It should include 2 tools total (at least 1 custom tool you wrote), and show:
- The prompt you gave the agent
- The agent's replies and tool usages
- The final answer/output

**ToolCallingAgent:** Create a `ToolCallingAgent` that completes a similar non-trivial task. It should include 2 tools total (at least 1 custom tool you wrote), and show:
- The prompt you gave the agent
- The agent's tool calls
- The final answer/output

**Self-assessment checklist:**
- CodeAgent works as specified
- ToolCallingAgent works as specified
- Tools have clear interfaces, sensible descriptions, and typed arguments/returns
- Code outputs are included and reproducible

---

## Assignment 3: Building a RAG Agent

Read through the following sections of the HF Agents Course:
- [Retrieval Agents (Unit 2)](https://huggingface.co/learn/agents-course/en/unit2/smolagents/retrieval_agents)
- [Agentic RAG (Unit 3)](https://huggingface.co/learn/agents-course/en/unit3/agentic-rag/invitees)

**Goals:**
- Build a RAG agent that can decide when to retrieve and answer grounded in retrieved evidence
- Implement a retriever (BM25 or similar) and integrate it as a tool the agent can call
- Evaluate your RAG agent on a small set of questions and report basic retrieval and answer quality

**Instructions:**

You may work locally or use Colab. Note: larger models may require more compute.

Set up your HF token if you want to use the HF Hub and inference API. Pin your dependencies in a `requirements.txt` or install cells at the top of your notebook.

**Recommended project layout:**
- `retriever.py` — loads the invitees dataset, converts records to documents, builds BM25 (or another retriever), exposes `retrieve(query, k)`
- `tools.py` — defines tools used by the agent (local retrieval or web search)
- `app.py` — instantiates model and agent, registers tools, runs a demo loop and evaluation

---

**Part 1: Build Your Local Knowledge Base Retriever**

- Load the Unit 3 provided dataset
- Convert each record with consistent formatting (name, role, org, bio, etc.)
- Build a retriever (BM25 is fine)
- Verify retrieval with at least 4–5 manual queries

Show the following outputs:
- The query
- Top-3 retrieved results (or snippets)
- Which result you believe is the best match

---

**Part 2: Build the RAG Agent**

Create an agent that decides when to call retrieval, uses retrieved snippets to answer, and produces answers with an Evidence section.

Minimum requirements:
- Tool-based retrieval must be used for invitees-related questions
- Final answer must include an **Answer** and an **Evidence** section (2–3 short quotes from retrieved results)

Demo: run at least 5 prompts:
- 3 answerable from the invitees knowledge base
- 2 unanswerable / out-of-scope

---

**Part 3: Mini Evaluation**

Create a small evaluation set of 10 questions:
- 7 answerable from the invitees knowledge base
- 3 unanswerable (agent should respond "not found" or ask a follow-up)

---

**Self-assessment checklist:**
- Retriever and indexing work — documents built correctly, retrieval returns sensible top-k snippets
- RAG agent works with grounding — correct tool usage, answers include evidence
- Code outputs are included and reproducible
