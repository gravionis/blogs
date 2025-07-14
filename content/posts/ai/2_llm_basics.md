+++
date = '2025-05-10T12:44:47+10:00'
draft = false
title = 'LLM Basics'
tags = ['LLM', 'Agentic AI']
+++

In this post, we explore Agentic AI—systems where agents activate results by the guidance of intelligence. Rather than relying solely on static models or manual intervention, agentic AI leverages autonomous or semi-autonomous agents that can perceive, reason, and act within their environment to achieve specific goals. Here we deep dive into the patterns and best practices that underpin successful agentic AI workflows.

## Generative v/s predictive models

| Model Type   | What it does                                                                 | Example Tasks                        | Example Models                                  | Typical Questions Answered |
|--------------|------------------------------------------------------------------------------|--------------------------------------|-------------------------------------------------|---------------------------|
| Generative   | Creates new data instances that resemble a given dataset by learning its underlying distribution. | Text/image/audio generation          | GPT-4 (text), DALL·E (images), Stable Diffusion (images) | What could be created?    |
| Predictive   | Forecasts outcomes or classifies inputs based on learned patterns; detects anomalies. | Regression, classification, anomaly detection | XGBoost (tabular), ResNet (image classification), ARIMA (time series) | What is likely to happen? (regression)<br>What category does this belong to? (classification)<br>Is something abnormal or an outlier? (density estimation) |

---

## Factors for Choosing a model

- **Model Performance**: Accuracy, robustness, and reliability of the model for your task.
- **Model Parameters (Size)**: Number of parameters; affects capability, resource needs, and deployment.
- **Use Case (Model Type)**: Match the model type (generative, predictive, etc.) to your application.
- **Training Input**: Nature, quality, and quantity of data available for training.
- **Training Method**: Approach used (supervised, unsupervised, reinforcement learning, etc.).
- **Context Token Size**: Maximum input length the model can handle at once (important for LLMs).
- **Model Speed (Deployment)**: Inference latency and throughput; critical for real-time or large-scale use.
- **Local or Shared Model**: Whether the model runs on local infrastructure or is accessed via API/cloud.
- **Model Cost**: Expenses for training, deployment, and ongoing usage (compute, storage, licensing, etc.).

### Models

- Open AI: gpt-4o-mini
- Antropic: Claude-3-7-Sonnet
- Google: Gemini-2.0-flash
- DeepSeek AI: DeepSeek V3, DeepSeek R1
- Groq: open source LLMs invluding Llama3.3
- Ollama: Local open source LLMs including Llama3.2

[Vellum Leaderboard](https://www.vellum.ai/llm-leaderboard)

---

## What is an Agent? Why Agentic AI?

An agent is an autonomous or semi-autonomous system that perceives its environment, makes decisions, and takes actions to achieve specific objectives—guided by intelligence rather than fixed rules. Agentic AI leverages such agents to perform complex tasks, adapt to new situations, and optimize outcomes, often with minimal human intervention. This approach enables more flexible, scalable, and effective AI-driven solutions.

In many cases, it is far cheaper and more accurate to use agentic AI to achieve desired results than to attempt the same outcome by training a larger or more complex model.

Large Language Models (LLMs) are powerful but limited by factors like training data, token limits and architecture. Many of these constraints can be mitigated through effective prompt engineering. 

Often, a single query requires context built from diverse data sources. Differences in reasoning (e.g., Gemini 2.5 Pro outperforming LLaMA 3.1), token limits, and features like function calling (e.g., supported in GPT-3.5) highlight model variability.

Despite these differences, common LLM challenges can be addressed using established design patterns—structured approaches that promote consistency, scalability, and efficiency.

### Workflow v/s Agentic Flow

A **workflow** is a predefined, often linear sequence of steps or tasks designed to achieve a specific outcome. Traditional workflows are typically static, rule-based, and follow a fixed path, making them suitable for repetitive or well-understood processes (e.g., document approval, data processing pipelines).

An **agentic flow**, in contrast, is dynamic and adaptive. It leverages intelligent agents that can perceive, reason, and act based on real-time context and feedback. Agentic flows are not strictly linear; agents can make decisions, change strategies, invoke tools, and even collaborate with other agents or humans as needed. This enables handling of complex, ambiguous, or evolving tasks where flexibility and autonomy are required.

**Summary Table:**

| Aspect            | Workflow (Traditional)                | Agentic Flow (AI/Agentic)                |
|-------------------|--------------------------------------|------------------------------------------|
| Structure         | Predefined, static steps             | Dynamic, adaptive, context-driven        |
| Decision Making   | Rule-based, manual                   | Autonomous, intelligent, feedback-driven |
| Flexibility       | Low                                  | High                                     |
| Adaptability      | Limited                              | Can adjust to new situations             |
| Example           | Invoice approval process             | Autonomous research assistant            |

---

## Autonomy Spectrum

![](../autonomy_spectrum.jpg)

| Level                   | Description                                                                                           | Example(s)                    |
|-------------------------|-------------------------------------------------------------------------------------------------------|-------------------------------|
| LLM as a Tool / Assistant | User-driven; LLM provides responses or completions. No memory, planning, or action-taking.           | ChatGPT answering questions   |
| LLM as a Copilot        | Semi-automated assistance; user remains in control. Suggests next actions, writes code, drafts emails, etc. | GitHub Copilot, Replit Ghostwriter |
| LLM-Augmented Agents    | LLM integrated into an agent loop (think-act-observe). Has memory, planning, and tool-use abilities. Requires some supervision or task input. | AutoGPT, LangGraph agents     |
| Autonomous Agents       | Fully self-directed; can generate goals, plan, execute actions across steps. Operates over long time horizons with minimal or no human input. Needs feedback, error correction, safety. | AgentVerse, OpenAgents        |

[source](https://ukparliament.shorthandstories.com/AI-in-weapons-systems-lords-report/)

---

## Systems
### Single agent system

A single agent system typically consists of several core components that enable it to operate intelligently and autonomously:

1. **Action & Tool Use**: The agent can interact with its environment and utilize external tools or APIs to accomplish tasks.
2. **Profile and Persona**: The agent maintains a defined identity, role, or persona, which guides its behavior and responses.
3. **Memory & Knowledge**: The agent stores and retrieves relevant information, context, and learned knowledge to inform its actions.
4. **Reasoning & Evaluation**: The agent analyzes situations, makes decisions, and evaluates outcomes to improve performance.
5. **Planning & Feedback**: The agent formulates plans to achieve objectives and incorporates feedback to adapt and optimize its strategies.

### Multi-Agent Systems

Multi-agent systems involve multiple autonomous agents interacting within a shared environment to solve problems collaboratively or competitively. These agents can communicate, coordinate, and negotiate with each other to achieve individual or collective goals. In the context of agentic AI, multi-agent systems enable more complex, distributed, and scalable solutions—allowing for emergent behaviors and robust problem-solving capabilities that go beyond what a single agent can accomplish.

---

## Patterns
* [microsoft autogen](https://microsoft.github.io/autogen/0.2/docs/Examples/)


