---
layout: page
title: Assignments
permalink: /assignments/
---

These assignments are adapted from the [Hugging Face Agents Course](https://huggingface.co/learn/agents-course/). In this self-paced version of the course, they are **completely optional** — use them for hands-on practice if you'd like.

---

<details>
<summary><strong>Assignment 1: Setting Up an HF Agent</strong></summary>
<br>

Read through <a href="https://huggingface.co/learn/agents-course/en/unit1/tutorial">Unit 1 of the HF Agents Course</a> and complete the first hands-on exercise setting up an agent.

This is a simple assignment to get you set up with HF agent frameworks and your workflow for the rest of the assignments.

<strong>To complete this assignment, create a Jupyter notebook containing:</strong>
<ul>
  <li>All of the code that the tutorial asks you to write, with cell outputs</li>
  <li>Written responses to the following questions:
    <ul>
      <li>How do you feel about the course so far? Are you clear on what the course is about and what you need to do?</li>
      <li>What topics in the course excite you the most right now?</li>
      <li>Initial thoughts on the Hugging Face tutorial. Was it clear how to set this up? Is this helpful for your understanding of how to implement agents?</li>
    </ul>
  </li>
</ul>

You can use Google Colab or a local environment. Note: <code>app.py</code> has dependencies with other files in the project, so it's recommended to clone the whole project into your workspace before modifying its code.

</details>

---

<details>
<summary><strong>Assignment 2: Building Coding and Tool Calling Agents</strong></summary>
<br>

Read through Unit 2.1 of the HF Agents Course:
<ul>
  <li><a href="https://huggingface.co/learn/agents-course/en/unit2/smolagents/code_agents">Code Agents</a></li>
  <li><a href="https://huggingface.co/learn/agents-course/en/unit2/smolagents/tool_calling_agents">Tool Calling Agents</a></li>
  <li><a href="https://huggingface.co/learn/agents-course/en/unit2/smolagents/tools">Tools (optional deeper dive)</a></li>
</ul>

<strong>Goals:</strong>
<ul>
  <li>Build a <code>CodeAgent</code> that takes actions by generating Python tool-call code</li>
  <li>Build a <code>ToolCallingAgent</code> that takes actions by generating structured tool calls (JSON)</li>
  <li>Define and use tools with clear interfaces (name, description, typed inputs/outputs)</li>
</ul>

<strong>Instructions:</strong>

You may work locally (recommended for stability) or use Colab. Note: if using larger models like Qwen 80B, Colab may require larger runtime sessions. Set up your HF token if you want to use the HF Hub and inference API.

<strong>CodeAgent:</strong> Create a <code>CodeAgent</code> that completes a non-trivial task. It should include 2 tools total (at least 1 custom tool you wrote), and show:
<ul>
  <li>The prompt you gave the agent</li>
  <li>The agent's replies and tool usages</li>
  <li>The final answer/output</li>
</ul>

<strong>ToolCallingAgent:</strong> Create a <code>ToolCallingAgent</code> that completes a similar non-trivial task. It should include 2 tools total (at least 1 custom tool you wrote), and show:
<ul>
  <li>The prompt you gave the agent</li>
  <li>The agent's tool calls</li>
  <li>The final answer/output</li>
</ul>

<strong>Self-assessment checklist:</strong>
<ul>
  <li>CodeAgent works as specified</li>
  <li>ToolCallingAgent works as specified</li>
  <li>Tools have clear interfaces, sensible descriptions, and typed arguments/returns</li>
  <li>Code outputs are included and reproducible</li>
</ul>

</details>

---

<details>
<summary><strong>Assignment 3: Building a RAG Agent</strong></summary>
<br>

Read through the following sections of the HF Agents Course:
<ul>
  <li><a href="https://huggingface.co/learn/agents-course/en/unit2/smolagents/retrieval_agents">Retrieval Agents (Unit 2)</a></li>
  <li><a href="https://huggingface.co/learn/agents-course/en/unit3/agentic-rag/invitees">Agentic RAG (Unit 3)</a></li>
</ul>

<strong>Goals:</strong>
<ul>
  <li>Build a RAG agent that can decide when to retrieve and answer grounded in retrieved evidence</li>
  <li>Implement a retriever (BM25 or similar) and integrate it as a tool the agent can call</li>
  <li>Evaluate your RAG agent on a small set of questions and report basic retrieval and answer quality</li>
</ul>

<strong>Instructions:</strong>

You may work locally or use Colab. Note: larger models may require more compute. Set up your HF token if you want to use the HF Hub and inference API. Pin your dependencies in a <code>requirements.txt</code> or install cells at the top of your notebook.

<strong>Recommended project layout:</strong>
<ul>
  <li><code>retriever.py</code> — loads the invitees dataset, converts records to documents, builds BM25 (or another retriever), exposes <code>retrieve(query, k)</code></li>
  <li><code>tools.py</code> — defines tools used by the agent (local retrieval or web search)</li>
  <li><code>app.py</code> — instantiates model and agent, registers tools, runs a demo loop and evaluation</li>
</ul>

<strong>Part 1: Build Your Local Knowledge Base Retriever</strong>
<ul>
  <li>Load the Unit 3 provided dataset</li>
  <li>Convert each record with consistent formatting (name, role, org, bio, etc.)</li>
  <li>Build a retriever (BM25 is fine)</li>
  <li>Verify retrieval with at least 4–5 manual queries</li>
</ul>

Show the following outputs:
<ul>
  <li>The query</li>
  <li>Top-3 retrieved results (or snippets)</li>
  <li>Which result you believe is the best match</li>
</ul>

<strong>Part 2: Build the RAG Agent</strong>

Create an agent that decides when to call retrieval, uses retrieved snippets to answer, and produces answers with an Evidence section.

Minimum requirements:
<ul>
  <li>Tool-based retrieval must be used for invitees-related questions</li>
  <li>Final answer must include an <strong>Answer</strong> and an <strong>Evidence</strong> section (2–3 short quotes from retrieved results)</li>
</ul>

Demo: run at least 5 prompts:
<ul>
  <li>3 answerable from the invitees knowledge base</li>
  <li>2 unanswerable / out-of-scope</li>
</ul>

<strong>Part 3: Mini Evaluation</strong>

Create a small evaluation set of 10 questions:
<ul>
  <li>7 answerable from the invitees knowledge base</li>
  <li>3 unanswerable (agent should respond "not found" or ask a follow-up)</li>
</ul>

<strong>Self-assessment checklist:</strong>
<ul>
  <li>Retriever and indexing work — documents built correctly, retrieval returns sensible top-k snippets</li>
  <li>RAG agent works with grounding — correct tool usage, answers include evidence</li>
  <li>Code outputs are included and reproducible</li>
</ul>

</details>
