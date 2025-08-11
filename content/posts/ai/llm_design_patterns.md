+++
date = '2025-05-20T12:44:47+10:00'
draft = false
title = 'LLM Design Patterns'
tags = ['LLM', 'Design Patterns']
+++

LLM design patterns are reusable strategies for building robust, efficient, and scalable AI applications. They help developers structure retrieval, reading, rewriting, memory, agent, and orchestration workflows for large language models, improving performance and maintainability.

## Table of Contents

- [Retrieve Pattern](#retrieve-pattern)
- [Read Pattern](#read-pattern)
- [Rewrite Pattern](#rewrite-pattern)
- [Multi-Query Pattern](#multi-query-pattern)
- [ColBERT Pattern](#colbert-pattern)
- [Raptor Pattern](#raptor-pattern)
- [Fusion Pattern](#fusion-pattern)
- [Re-Ranking Pattern](#re-ranking-pattern)
- [Chunking Pattern](#chunking-pattern)
- [Routing Pattern](#routing-pattern)
- [Augmented Generation Pattern](#augmented-generation-pattern)
- [Tool Use Pattern](#tool-use-pattern)
- [Self-Ask Pattern](#self-ask-pattern)
- [Retrieval-Augmented Generation (RAG)](#retrieval-augmented-generation-rag)
- [Agent Pattern](#agent-pattern)
- [Conversational Memory Pattern](#conversational-memory-pattern)
- [Few-Shot Pattern](#few-shot-pattern)
- [Zero-Shot Pattern](#zero-shot-pattern)
- [Chain of Thought Pattern](#chain-of-thought-pattern)
- [ReAct Pattern](#react-pattern)
- [HyDE Pattern](#hyde-pattern)
- [Map-Reduce Pattern](#map-reduce-pattern)
- [Ensemble Pattern](#ensemble-pattern)
- [Guardrails Pattern](#guardrails-pattern)
- [Prompt Chaining Pattern](#prompt-chaining-pattern)
- [Function Calling Pattern](#function-calling-pattern)
- [Multi-Hop Pattern](#multi-hop-pattern)
- [Structured Output Pattern](#structured-output-pattern)
- [Intermediate Output Pattern](#intermediate-output-pattern)
- [Streaming Output Pattern](#streaming-output-pattern)
- [Human-in-the-Loop Pattern](#human-in-the-loop-pattern)
- [Resume/Restart/Edit/Fork Pattern](#resumerestarteditfork-pattern)
- [Multitasking Pattern](#multitasking-pattern)
- [Supervisor/Multi-Agent Pattern](#supervisormulti-agent-pattern)
- [Router Architecture](#router-architecture)
- [Chain Architecture](#chain-architecture)
- [LLM Call Architecture](#llm-call-architecture)
- [Subgraph Pattern](#subgraph-pattern)
- [Summary](#summary)

---

## Retrieve Pattern

Fetches relevant documents or data chunks from a large corpus using search or embedding-based retrieval.

**When to use:**  
- When narrowing context for LLMs from large datasets.

**When not to use:**  
- When all data fits in context or is already relevant.

---

## Read Pattern

Uses the LLM to extract, summarize, or answer questions from retrieved documents.

**When to use:**  
- For QA, summarization, or extracting insights from retrieved data.

**When not to use:**  
- When direct retrieval suffices.

---

## Rewrite Pattern

Transforms queries or outputs to improve retrieval, clarity, or user experience.

**When to use:**  
- To clarify ambiguous queries or rephrase answers.

**When not to use:**  
- When input/output is already optimal.

---

## Multi-Query Pattern

Generates multiple queries from the original user input to improve recall and coverage in retrieval.

**When to use:**  
- When a single query may miss relevant information.

**When not to use:**  
- When queries are already comprehensive.

---

## ColBERT Pattern

Uses late interaction models (like ColBERT) for efficient, scalable neural retrieval.

**When to use:**  
- For large-scale, high-performance semantic search.

**When not to use:**  
- For small datasets or when classical retrieval suffices.

---

## Raptor Pattern

Recursive Abstractive Processing for Tree-Organized Retrieval; combines recursive summarization and retrieval for hierarchical data.

**When to use:**  
- For tree-structured or hierarchical document retrieval.

**When not to use:**  
- For flat or small datasets.

---

## Fusion Pattern

Combines results from multiple retrieval sources or methods to improve diversity and coverage.

**When to use:**  
- When no single retrieval method is sufficient.

**When not to use:**  
- When one source is clearly superior.

---

## Re-Ranking Pattern

Uses LLMs or other models to reorder retrieved results for better relevance.

**When to use:**  
- When initial retrieval is noisy or imprecise.

**When not to use:**  
- When retrieval is already highly accurate.

---

## Chunking Pattern

Splits large documents into smaller chunks for more effective retrieval and context management.

**When to use:**  
- When documents exceed context window limits.

**When not to use:**  
- When all data fits in context.

---

## Routing Pattern

Directs queries to different models, tools, or retrieval systems based on query type or intent.

**When to use:**  
- For multi-modal or multi-domain systems.

**When not to use:**  
- When all queries are similar.

---

## Augmented Generation Pattern

Uses external tools, APIs, or databases to supplement LLM outputs with up-to-date or factual information.

**When to use:**  
- When LLMs need external knowledge or capabilities.

**When not to use:**  
- When LLM output alone is sufficient.

---

## Tool Use Pattern

Integrates external tools (calculators, search engines, APIs) into LLM workflows for enhanced capabilities.

**When to use:**  
- For tasks requiring computation or external data.

**When not to use:**  
- When LLM can answer directly.

---

## Self-Ask Pattern

LLM decomposes complex queries into sub-questions and answers them step by step.

**When to use:**  
- For multi-hop or reasoning-intensive queries.

**When not to use:**  
- For simple, direct questions.

---

## Retrieval-Augmented Generation (RAG)

Combines retrieval and generation, using retrieved documents as context for LLM responses.

**When to use:**  
- For knowledge-intensive tasks.

**When not to use:**  
- When generation alone suffices.

---

## Agent Pattern

LLM acts as an agent, planning and executing multi-step tasks, often using tools and memory.

**When to use:**  
- For complex workflows and automation.

**When not to use:**  
- For single-turn, simple tasks.

---

## Conversational Memory Pattern

Maintains context across multiple turns in a conversation, allowing the LLM to reference previous exchanges.

**When to use:**  
- For chatbots and assistants needing context retention.

**When not to use:**  
- For stateless, single-turn interactions.

---

## Few-Shot Pattern

Provides a few examples in the prompt to guide the LLM’s output.

**When to use:**  
- When task-specific examples improve accuracy.

**When not to use:**  
- When examples are unnecessary or context window is limited.

---

## Zero-Shot Pattern

Relies on the LLM’s generalization ability without providing examples.

**When to use:**  
- For generic tasks or when examples are unavailable.

**When not to use:**  
- When the task is highly specialized.

---

## Chain of Thought Pattern

Encourages the LLM to reason step-by-step before answering.

**When to use:**  
- For complex reasoning or math problems.

**When not to use:**  
- For simple, direct queries.

---

## ReAct Pattern

Combines reasoning and acting, allowing the LLM to plan, execute actions (like tool calls), and reflect.

**When to use:**  
- For tasks requiring both reasoning and tool use.

**When not to use:**  
- For simple, direct answers.

---

## HyDE Pattern

Hypothetical Document Embeddings: Generates hypothetical answers and uses them to retrieve relevant documents.

**When to use:**  
- When queries are ambiguous or lack context.

**When not to use:**  
- When queries are clear and direct.

---

## Map-Reduce Pattern

Splits a task into smaller subtasks (map), processes them in parallel, and combines results (reduce).

**When to use:**  
- For large-scale summarization or QA over many documents.

**When not to use:**  
- For small datasets or simple tasks.

---

## Ensemble Pattern

Combines outputs from multiple models or chains to improve robustness and accuracy.

**When to use:**  
- When diversity or consensus is needed.

**When not to use:**  
- When one model is sufficient.

---

## Guardrails Pattern

Implements safety checks, validation, or moderation on LLM outputs.

**When to use:**  
- For compliance, safety, or quality assurance.

**When not to use:**  
- When outputs are inherently safe.

---

## Prompt Chaining Pattern

Links multiple prompts together, passing outputs as inputs to subsequent prompts.

**When to use:**  
- For multi-step workflows or complex tasks.

**When not to use:**  
- For single-step tasks.

---

## Function Calling Pattern

Uses LLMs to call external functions or APIs based on user intent.

**When to use:**  
- For automation, integration, or tool use.

**When not to use:**  
- When no external actions are needed.

---

## Multi-Hop Pattern

Solves tasks requiring reasoning over multiple pieces of information or steps.

**When to use:**  
- For complex QA or reasoning tasks.

**When not to use:**  
- For direct, single-hop queries.

---

## Structured Output Pattern

Ensures LLM outputs are in a specific format (e.g., JSON, XML) for downstream processing.

**When to use:**  
- When machine-readable output is required.

**When not to use:**  
- When free-form text is sufficient.

---

## Intermediate Output Pattern

Captures intermediate steps or reasoning from the LLM for transparency or debugging.

**When to use:**  
- For explainability or step-by-step reasoning.

**When not to use:**  
- When only final output is needed.

---

## Streaming Output Pattern

Streams LLM output token-by-token for real-time applications.

**When to use:**  
- For chatbots, live assistants, or real-time feedback.

**When not to use:**  
- For batch or offline tasks.

---

## Human-in-the-Loop Pattern

Involves human review, correction, or intervention in LLM workflows.

**When to use:**  
- For critical tasks, moderation, or training.

**When not to use:**  
- For fully automated, low-risk tasks.

---

## Resume/Restart/Edit/Fork Pattern

Allows users to resume, restart, edit, or fork LLM sessions or states.

**When to use:**  
- For long-running or collaborative workflows.

**When not to use:**  
- For stateless, single-turn interactions.

---

## Multitasking Pattern

Handles multiple concurrent tasks or inputs, managing queueing, interruption, or parallel execution.

**When to use:**  
- For assistants or agents handling many requests.

**When not to use:**  
- For single-task systems.

---

## Supervisor/Multi-Agent Pattern

Coordinates multiple agents or sub-agents, possibly with a supervisor agent managing others.

**When to use:**  
- For complex, distributed, or multi-role workflows.

**When not to use:**  
- For simple, single-agent tasks.

---

## Router Architecture

Directs requests to different chains, agents, or tools based on logic or semantics.

**When to use:**  
- For modular, scalable, multi-domain applications.

**When not to use:**  
- For monolithic or single-purpose systems.

---

## Chain Architecture

Composes multiple LLM calls or steps into a pipeline or chain.

**When to use:**  
- For multi-step reasoning or processing.

**When not to use:**  
- For atomic, single-step tasks.

---

## LLM Call Architecture

Direct, single LLM call for simple tasks.

**When to use:**  
- For straightforward completions or generations.

**When not to use:**  
- For complex, multi-step workflows.

---

## Subgraph Pattern

Uses subgraphs or modular chains within a larger workflow for reuse and organization.

**When to use:**  
- For complex, reusable, or hierarchical workflows.

**When not to use:**  
- For simple, flat workflows.

---

## Summary

LLM design patterns and architectures help structure retrieval, reading, rewriting, multi-query, fusion, reranking, chunking, routing, agent, memory, few-shot, zero-shot, chain-of-thought, ReAct, HyDE, map-reduce, ensemble, guardrails, prompt chaining, function calling, multi-hop, structured output, intermediate output, streaming, human-in-the-loop, multitasking, supervisor, router, chain, subgraph, and LLM call workflows for AI applications.  
They improve efficiency, scalability, and maintainability, and are essential for building advanced LLM-powered systems.
