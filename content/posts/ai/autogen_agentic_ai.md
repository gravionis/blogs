+++
date = '2025-05-10T12:44:47+10:00'
draft = true
title = '🔮 Autogen'
tags = ['Agentic AI']
+++

Autogen is an open-source framework developed by Microsoft for building agentic AI systems. It provides a flexible set of agent classes and utilities that enable the creation of multi-agent workflows, conversational agents, and retrieval-augmented generation (RAG) pipelines. With Autogen, developers can orchestrate interactions between humans, LLM-powered assistants, and specialized tool agents to solve complex tasks in a collaborative and autonomous manner.


## 🧠 Core Agent Classes

| Class Name               | Description                                                                |
| ------------------------ | -------------------------------------------------------------------------- |
| `UserProxyAgent`         | Represents a human (or simulated human); can start or steer conversations. |
| └── `RetrieveUserProxyAgent` | Extends `UserProxyAgent`; adds document retrieval (RAG) support.           |
| `AssistantAgent`         | Represents an LLM-powered assistant; responds to messages autonomously.    |
| `GroupChatManager`       | Manages coordination of multiple agents in a group chat.                   |
| `GroupChat`              | Defines a chat session involving multiple agents.                          |
| `CodeInterpreterAgent`   | Executes Python code snippets during the conversation.                     |

## 🤖 Specialized Agents (LLM-backed)

| Class Name             | Description                                                               |
| ---------------------- | ------------------------------------------------------------------------- |
| `ConversableAgent`     | Abstract base class for agents that can converse (e.g. `AssistantAgent`). |
| └── `GPTAssistantAgent`    | A concrete implementation using OpenAI GPT LLMs.                          |
| └── `FunctionCallingAgent` | Supports OpenAI-style function-calling flows.                             |
| └── `OpenAIWrapperAgent`   | Agent using direct OpenAI API with wrapper capabilities.                  |

## 📁 Retrieval & RAG

| Class Name               | Description                                                                                |
| ------------------------ | ------------------------------------------------------------------------------------------ |
| `RetrieveUserProxyAgent` | User proxy with document retrieval.                                                        |
| └── `AutoRetriever`          | Fetches documents from URLs, files, and APIs; used internally by `RetrieveUserProxyAgent`. |
| └── `SimpleDocRetriever`     | Basic local document retriever for small datasets.                                         |
| └── `LocalDocRetriever`      | More configurable retriever using local vector store (e.g. FAISS).                         |

## ⚙️ Tooling & Execution

| Class Name                     | Description                                         |
| ------------------------------ | ---------------------------------------------------|
| `PythonCodeExecutor`           | Runs Python code in secure environments.            |
| `DockerCodeExecutor`           | Executes code within Docker (for isolation).        |
| `DockerCommandLineCodeExecutor`| Runs command-line code/scripts inside Docker.       |
| `LocalCommandLineCodeExecutor` | Runs command-line code/scripts on the local machine.|
| `ToolAgent`                    | Agent that wraps command-line or web tools.         |
| `WebRetriever`                 | Fetches web content for retrieval.                  |

## 🛠 Utility Components

| Class Name / Concept | Description                                                  |
| -------------------- | ------------------------------------------------------------ |
| `Message`            | Internal representation of a chat message.                   |
| `AgentContext`       | Tracks message state and execution context per agent.        |
| `ChatResult`         | Standard output from LLM chat calls.                         |
| `LLMConfig`          | Dict that defines temperature, model name, API configs, etc. |

## References
-[Introduction: Multi-agent Conversation Framework
](https://microsoft.github.io/autogen/0.2/docs/Use-Cases/agent_chat)
-[Read all pages: AutoGen Tutorials](https://microsoft.github.io/autogen/0.2/docs/tutorial/introduction/)
- [Documentation](https://microsoft.github.io/autogen/stable//user-guide/core-user-guide/installation.html)
- [Building Generative AI Agents_ Using LangGraph, AutoGen, and CrewAI Tom Taulli, Gaurav Deshmukh](https://drive.google.com/file/d/1CLLQFKlsn29nqbgASe3MzsCWAoraHpmK/view?usp=drive_link)
- [AI Agent in Action](https://drive.google.com/file/d/1gDgi948sX7BBGyQggY82GfxJNpGXIuYt/view?usp=drive_link)