+++
date = '2025-05-10T12:44:47+10:00'
draft = false
title = 'Autogen'
tags = ['Agentic AI']
+++

## 🧠 Core Agent Classes

| Class Name               | Description                                                                |
| ------------------------ | -------------------------------------------------------------------------- |
| `UserProxyAgent`         | Represents a human (or simulated human); can start or steer conversations. |
| `AssistantAgent`         | Represents an LLM-powered assistant; responds to messages autonomously.    |
| `RetrieveUserProxyAgent` | Extends `UserProxyAgent`; adds document retrieval (RAG) support.           |
| `GroupChatManager`       | Manages coordination of multiple agents in a group chat.                   |
| `GroupChat`              | Defines a chat session involving multiple agents.                          |
| `CodeInterpreterAgent`   | Executes Python code snippets during the conversation.                     |

## 🤖 Specialized Agents (LLM-backed)

| Class Name             | Description                                                               |
| ---------------------- | ------------------------------------------------------------------------- |
| `ConversableAgent`     | Abstract base class for agents that can converse (e.g. `AssistantAgent`). |
| `GPTAssistantAgent`    | A concrete implementation using OpenAI GPT LLMs.                          |
| `FunctionCallingAgent` | Supports OpenAI-style function-calling flows.                             |
| `OpenAIWrapperAgent`   | Agent using direct OpenAI API with wrapper capabilities.                  |

## 📁 Retrieval & RAG

| Class Name               | Description                                                                                |
| ------------------------ | ------------------------------------------------------------------------------------------ |
| `RetrieveUserProxyAgent` | User proxy with document retrieval.                                                        |
| `AutoRetriever`          | Fetches documents from URLs, files, and APIs; used internally by `RetrieveUserProxyAgent`. |
| `SimpleDocRetriever`     | Basic local document retriever for small datasets.                                         |
| `LocalDocRetriever`      | More configurable retriever using local vector store (e.g. FAISS).                         |

## ⚙️ Tooling & Execution

| Class Name           | Description                                  |
| -------------------- | -------------------------------------------- |
| `PythonCodeExecutor` | Runs Python code in secure environments.     |
| `DockerCodeExecutor` | Executes code within Docker (for isolation). |
| `ToolAgent`          | Agent that wraps command-line or web tools.  |
| `WebRetriever`       | Fetches web content for retrieval.           |

## 🛠 Utility Components

| Class Name / Concept | Description                                                  |
| -------------------- | ------------------------------------------------------------ |
| `Message`            | Internal representation of a chat message.                   |
| `AgentContext`       | Tracks message state and execution context per agent.        |
| `ChatResult`         | Standard output from LLM chat calls.                         |
| `LLMConfig`          | Dict that defines temperature, model name, API configs, etc. |
