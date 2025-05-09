+++
date = '2025-05-03T12:44:47+10:00'
draft = false
title = 'Langchain & Langgraph'
+++

## Excerpt
This post, we aim to deep dive (a bit) into LangChain and Langgraph: 
* As essential tools for implementing Prompt Engineering strategies.
* Exploration of design patterns in Generative AI to address repetitive problems efficiently
* Focus on leveraging established patterns to avoid reinventing solutions in the context of AI workflows.

## Introduction

### Why Prompt Engineering and Why Design Patterns for LLMs with Langchain?

Large Language Models (LLMs) are powerful but limited by factors like training data, token limits and architecture. Many of these constraints can be mitigated through effective prompt engineering.

Often, a single query requires context built from diverse data sources. Differences in reasoning (e.g., Gemini 2.5 Pro outperforming LLaMA 3.1), token limits, and features like function calling (e.g., supported in GPT-3.5) highlight model variability.

Despite these differences, common LLM challenges can be addressed using established design patterns—structured approaches that promote consistency, scalability, and efficiency.
