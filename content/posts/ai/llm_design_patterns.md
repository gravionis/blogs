+++
date = '2025-05-20T12:44:47+10:00'
draft = false
title = 'LLM Design Patterns'
tags = ['LLM', 'Design Patterns']
+++

LLM design patterns are reusable strategies for building robust, efficient, and scalable AI applications. They help developers structure retrieval, reading, rewriting, memory, agent, and orchestration workflows for large language models. These patterns improve performance, maintainability accuracy, cost and security.

## Introduction
* About  LLMs
  - GPT-3: 175B Parameters, ~350B tokens. GPT-4:is 6x bigger. GPT-5 was supposed to be 20x bigger but is counter intuitive 300B Parameters.
  - GPT-5 leverages on many architectural innovations like the Unified Intelligence System,
    - Unified Intelligence System: integrates multiple reasoning and perception modules for more general intelligence.
    - Mixture-of-Experts: routes inputs to specialized sub-models for improved efficiency and accuracy.
    - Multimodal Integration: processes and understands text, images, and other data types together.
  - We have bigger better models but also better architectures and training methods.
  - We have restrictions using best available model due to cost, security, and other factors. Hence we have to compensate with design patterns.

* Transformer Architecture:
  - LLMs use the transformer neural network architecture.
  - Transformers handle data as sequences of tokens, capturing the meaning and context of words.
  - The architecture enables prediction of the next word in a sequence.
  - Transformers understand relationships between words, regardless of their position in the text.
  - This leads to comprehensive understanding of sentences, paragraphs, and larger text structures.
  - Transformers are not designed for accurate mathematical computation; LLMs often use external tools (like calculators or code interpreters) to perform precise math.

* Tokens:
  - A token is a chunk of text, often a word or part of a word.
  - Roughly, one token is about 4 characters or 0.75 words in English.
  - Tokenization allows models to process text efficiently and consistently.
  - To estimate monthly cost: (tokens used per month) × (API cost per token).
  - If transaction rate is T tokens/sec, that's about (T × 0.75) words/sec.
  - 
## Some applicable Laws
- Chinchilla's Law: optimal model performance when training tokens ≈ 20× model parameters.
    - Example: 70B parameters → ~1.4T tokens needed.
    - Scaling to hundreds of billions/trillions of parameters requires enormous data, often exceeding available high-quality text.
    - Highlights challenges in scaling LLMs beyond current limits.
