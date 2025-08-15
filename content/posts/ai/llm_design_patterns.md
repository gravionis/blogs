+++
date = '2025-05-20T12:44:47+10:00'
draft = false
title = 'LLM Design Patterns'
tags = ['LLM', 'Design Patterns']
+++

LLM design patterns are reusable strategies for building robust, efficient, and scalable AI applications. They help developers structure retrieval, reading, rewriting, memory, agent, and orchestration workflows for large language models. These patterns improve performance, maintainability accuracy, cost and security.

## LLMs
  - GPT-3: 175B Parameters, ~350B tokens. GPT-4:is 6x bigger. GPT-5 was supposed to be 20x bigger but is counter intuitive 300B Parameters.
  - GPT-5 leverages on many architectural innovations like the Unified Intelligence System,
    - Unified Intelligence System: integrates multiple reasoning and perception modules for more general intelligence.
    - Mixture-of-Experts: routes inputs to specialized sub-models for improved efficiency and accuracy.
    - Multimodal Integration: processes and understands text, images, and other data types together.
  - We have bigger better models but also better architectures and training methods.
  - We have restrictions using best available model due to cost, security, and other factors. Hence we have to compensate with design patterns.

## Transformer Architecture: 
  - LLMs use the transformer neural network architecture.
  - Transformers handle data as sequences of tokens, capturing the meaning and context of words.
  - The architecture enables prediction of the next word in a sequence.
  - Transformers understand relationships between words, regardless of their position in the text.
  - This leads to comprehensive understanding of sentences, paragraphs, and larger text structures.
  - Transformers are not designed for accurate mathematical computation; LLMs often use external tools (like calculators or code interpreters) to perform precise math.

## Tokens:
  - A token is a chunk of text, often a word or part of a word.
  - Roughly, one token is about 4 characters or 0.75 words in English.
  - Tokenization allows models to process text efficiently and consistently.
  - To estimate monthly cost: (tokens used per month) × (API cost per token).
  - If transaction rate is T tokens/sec, that's about (T × 0.75) words/sec.

## LLM Model Variants and Techniques:
  - Two main techniques:
    - Predict next word (causal language modeling): Used by models like GPT; generates text by predicting the next token in a sequence.
    - Predict missing word (masked language modeling): Used by models like BERT; predicts masked tokens within a sentence for better understanding of context.
  - GPT models: Focus on text generation, conversation, and completion tasks.
  - BERT models: Focus on understanding, classification, and extracting information from text.
  - Other flavours:
    - Encoder-only (BERT): Good for understanding and classification.
    - Decoder-only (GPT): Good for generation and completion.
    - Encoder-decoder (T5, BART): Good for translation, summarization, and more complex tasks.
  - Many LLMs are specialized for tasks like code generation, multimodal input (text + images), or domain-specific knowledge.

## Some applicable Laws
- Chinchilla's Law: optimal model performance when training tokens ≈ 20× model parameters.
    - Example: 70B parameters → ~1.4T tokens needed.
    - Scaling to hundreds of billions/trillions of parameters requires enormous data, often exceeding available high-quality text.
    - Highlights challenges in scaling LLMs beyond current limits.

## Popular LLM Tools and Frameworks

| Tool/Framework         | Language   | Focus/Strengths                  | Integration      | Use Case Examples              |
|-----------------------|------------|----------------------------------|------------------|-------------------------------|
| LangChain             | Python     | Chaining, agents, retrieval      | Many LLM APIs    | Chatbots, RAG, workflows      |
| LangGraph             | Python     | Multi-agent, graph orchestration | LangChain        | Reasoning, modular agents     |
| Spring AI             | Java       | Enterprise, abstraction          | Spring ecosystem | Business apps, backend        |
| HF Transformers       | Python     | Model training, deployment       | Model hub, APIs  | NLP tasks, research, prod     |
| Agentic AI (AutoGPT, CrewAI, N8N) | Python/JS | Autonomous agents, automation | Various          | Task automation, multi-agent  |

## Prompt
- A prompt is the input text or instruction given to an LLM to guide its response.
- Effective prompts are clear, specific, and context-aware.
- Considerations for prompts:
  - Clarity: Avoiding ambiguity to get accurate results. Cannot use our own DSLs. 
  - Context: Provide relevant background or examples.
  - Length: Too short may lack detail; too long may confuse or dilute intent.
  - Structure: Use formatting, lists, or step-by-step instructions for better outputs.
  - Constraints: Specify requirements, style, or limitations as needed.
  - Iteration: Refine prompts based on model responses to improve outcomes.
  - Inconsistent results: Due to different models and also different model parameters.

## Prompt Engineering and Patterns
- Prompt engineering is the practice of designing and refining prompts to optimize LLM outputs.
- Prompt engineers experiment with wording, structure, and context to achieve desired results.
- Common patterns include:
  - Zero-shot: Ask the model to perform a task without examples.
  - Few-shot: Provide examples to guide the model's response.
  - Chain-of-thought: Encourage step-by-step reasoning for complex tasks.
  - Role assignment: Specify the model's persona or expertise (e.g., "Act as a legal advisor").
  - Structured Output: Request specific formats, styles, or limitations.
  - Iterative refinement: Adjust prompts based on model feedback to improve accuracy and relevance.
  - Context injection: Add relevant background information or previous conversation.
  - Self-consistency: Ask the model to generate multiple solutions and select the best.
  - ReAct (Reason + Act): Combine reasoning steps with actions or tool use.
  - Retrieval Augmented Generation: Incorporate external knowledge or documents into the prompt.
  - Multi-turn: Structure prompts for ongoing dialogue or multi-step tasks.
  - Instruction tuning: Use prompts aligned with how the model was trained for better results.
  - Reflection or Deliberation: Ask the model to reflect or critique its own answer before finalizing.
  - Template-based: Use reusable prompt templates for consistency across tasks.
  - Tool calling: Enable the model to invoke external tools or APIs (e.g., calculators, search engines) for enhanced capabilities.
  - Function calling: Structure prompts so the model can call specific functions or code snippets to solve tasks.
  - Dynamic prompt composition: Build prompts programmatically based on user input or context for flexible interactions.

## Chat Models
- Chat models are specialized LLMs designed for conversational interactions.

| Model                                                                                                        | Provider       | Strengths                                   | Typical Use Cases                                 |
|--------------------------------------------------------------------------------------------------------------|----------------|---------------------------------------------|---------------------------------------------------|
| GPT-3 / GPT-4 / GPT-5                                                                                        | OpenAI         | Text generation, conversation, code, summarization | Chatbots, assistants, writing, code, content      |
| BERT                                                                                                         | Google         | Context understanding, classification, QA   | Search, sentiment, entity recognition, classification|
| LLaMA                                                                                                        | Meta           | Open-source, efficient, adaptable           | Research, custom training, open-source apps       |
| Claude                                                                                                       | Anthropic      | Safety-focused, reliable, conversational    | Support, safe chatbots, document analysis         |
| Mistral                                                                                                      | Mistral AI     | Efficient, open weights, strong benchmarks  | Research, production NLP, open-source projects    |
| Gemini                                                                                                       | Google DeepMind | Multimodal (text, image, audio), reasoning  | Multimodal assistants, content analysis           |
| Cohere                                                                                                       | Cohere         | Embeddings, classification, retrieval       | Semantic search, enterprise NLP, clustering       |
| Anthropic (Claude), Amazon (Titan), Meta (Llama),<br/>Mistral, AI21 Labs (Jurassic), Cohere (Command) | Amazon Bedrock | Wide model selection, enterprise integration, scalable APIs | Chatbots, search, summarization, enterprise AI    |

## Embeddings
- Embeddings are dense vector representations of text (words, sentences, or documents) generated by LLMs.
- They capture semantic meaning, allowing for similarity comparison, clustering, and retrieval.
- Common models for embeddings: OpenAI Embeddings, Cohere, Sentence Transformers, BERT.
- Use cases: semantic search, recommendation systems, document classification, clustering, and information retrieval.

## Vector Store
- A vector store is a database or storage system optimized for storing and searching embeddings.
- It enables fast similarity search and retrieval of relevant documents or data points using vector operations.
- Popular vector stores: Pinecone, Weaviate, FAISS, Milvus, Qdrant.
- Use cases: retrieval-augmented generation (RAG), semantic search, personalized recommendations, and knowledge management.


## Model Paramaters
| Parameter            | Description                                                                                     | Typical Range        | Impact                                                                 |
|----------------------|-------------------------------------------------------------------------------------------------|----------------------|------------------------------------------------------------------------|
| **temperature**      | Controls randomness. Lower = deterministic, higher = creative/unpredictable.                  | `0.0` – `2.0`       | `0.0` = deterministic, `1.0` = balanced, `>1.2` = very random.        |
| **top_p**            | Nucleus sampling. Chooses tokens from smallest set whose cumulative probability ≥ p.           | `0.1` – `1.0`       | Lower = more focused, 1.0 = no restriction.                           |
| **top_k**            | Limits sampling to the top K tokens by probability.                                           | `1` – `100`         | Low values reduce creativity, high values allow more variation.       |
| **max_tokens**       | Maximum tokens to generate in the response.                                                   | Depends on model    | Controls output length.                                               |
| **min_tokens**       | Minimum tokens to generate before stopping.                                                   | Depends on model    | Ensures longer answers if needed.                                     |
| **presence_penalty** | Penalizes tokens already present in the text (encourages new topics).                          | `-2.0` – `2.0`      | Higher = more diversity.                                              |
| **frequency_penalty**| Penalizes frequent tokens to reduce repetition.                                               | `-2.0` – `2.0`      | Higher = less repetition.                                             |
| **stop**             | List of stop sequences where generation should halt.                                          | Strings / tokens    | Useful for structured responses.                                      |
| **seed**             | Fixes randomness for reproducibility.                                                         | Integer             | Same seed = same output (with sampling).                              |
| **do_sample**        | Enables probabilistic sampling instead of greedy decoding.                                    | `true` / `false`    | Needed for temperature/top_p/top_k to take effect.                    |
| **num_beams**        | Number of beams for beam search decoding.                                                     | `1` – `10+`         | Higher = more accurate, slower, less creative.                        |
| **length_penalty**   | Adjusts likelihood for longer sequences in beam search.                                       | `>0`                | Higher = longer outputs favored.                                      |
| **early_stopping**   | Stops beam search when best candidates are found.                                             | `true` / `false`    | Speeds up generation, may miss better completions.                    |
| **logit_bias**       | Adjusts probability of specific tokens (positive = more likely, negative = less likely).       | Dict of token IDs   | Useful for forcing or avoiding words.                                 |
| **echo**             | Return the prompt along with the completion.                                                  | `true` / `false`    | For debugging or prompt reconstruction.                                |

## Roles
| Role        | Purpose                                                       | Example                                                                 |
|-------------|--------------------------------------------------------------|------------------------------------------------------------------------|
| **system**  | Sets high-level instructions, behavior, or persona for model | "You are an expert software engineer. Respond concisely with examples." |
| **user**    | Represents the end-user’s input or question                  | "Write a Python function to reverse a string."                         |
| **assistant**| Represents the model’s own response                         | "Here is the Python code:\n```python\ndef reverse_string(s): return s[::-1]\n```" |
| **tool**    | Output from an external tool or function call                | `{"result": "42"}` (after a calculator function call)                  |
| **function**| (Older term for tool) Shows result from a function           | Same as tool                                                           |
| **critic**  | Used for self-evaluation or reinforcement learning loops     | "Check if the previous answer followed all constraints."               |

