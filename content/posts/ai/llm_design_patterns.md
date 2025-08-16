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
- Common patterns:
| **Type**                       | **Definition**                                                       | **Example**                                                                 |
|--------------------------------|----------------------------------------------------------------------|------------------------------------------------------------------------------|
| **Single-String Prompting**    | One large text prompt, typically for completion models.             | `Translate to French: "How are you?"`                                      |
| **Chat-Based Prompting**       | Structured messages with roles (`system`, `user`, `assistant`).     | System: "You are helpful." User: "Translate 'How are you?' to French."     |
| **Zero-Shot**                  | No examples provided; just the instruction.                         | `Summarize this text in one sentence: ...`                                  |
| **Few-Shot**                   | Include a few examples to guide the output.                         | `Q: Capital of France? A: Paris. Q: Capital of Germany? A:`                |
| **Chain-of-Thought (CoT)**     | Ask model to reason step-by-step before answering.                  | `Explain step by step: If you have 3 apples and eat 1, how many are left?` |
| **Self-Consistency**           | Model generates multiple solutions, picks most consistent.          | Used in reasoning-heavy tasks.                                              |
| **Role-Based / Persona**       | Assign a role or persona for better context.                        | `Act as an expert Python tutor. Explain decorators.`                        |
| **Instruction-Based**          | Direct task-oriented commands without dialogue.                     | `Extract all email addresses from the text.`                                |
| **Structured Output**          | Request output in JSON, table, or specific format.                  | `Return the answer in JSON with keys: name, age.`                           |
| **ReAct (Reason + Act)**       | Model reasons, then calls tools or APIs.                            | `Thought: I need weather info. Action: call weather API.`                   |
| **Retrieval-Augmented (RAG)**  | Combine prompt with retrieved external knowledge.                   | `[Context] Answer based on above.`                                          |
| **Multimodal Prompting**       | Combines text + images (or other modalities).                       | `Describe the scene in this image.`                                         |
| **Prompt Chaining**            | Splits a task into multiple linked prompts.                         | Step 1: Summarize → Step 2: Extract entities → Step 3: Generate questions. |
| **Instruction Tuning Alignment**| Prompts aligned to model training objectives for better accuracy.   | `Follow these steps exactly as shown in instructions.`                      |
| **Reflection / Deliberation**  | Ask model to review or critique its own response.                   | `Check your previous answer and improve it.`                                |
| **Dynamic Prompt Composition** | Build prompts programmatically for personalization.                 | Insert user name, context dynamically from a database.                      |
| **Tool Calling**               | Enable model to trigger external tools for answers.                 | `If math needed, call calculator function.`                                  |
| **Function Calling**           | Model outputs structured JSON to call specific function.            | `{ "function": "get_weather", "location": "Paris" }`                        |

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
| **developer** (optional) | Provides additional instructions (multi-role systems) | "Add unit tests for the function above."                               |

apart from the system, user and assistant roles which are the default roles in some frameworks most frameworks support custom roles.
```python
from langchain.schema import ChatMessage

messages = [
    ChatMessage(role="system", content="You are an expert AI."),
    ChatMessage(role="developer", content="Always include type hints in Python code."),
    ChatMessage(role="user", content="Write a function to add two numbers.")
]
```

## Structured Output
Structured output is when the model returns data in a **predefined, machine-readable format** like JSON or CSV, instead of free-form text.

### Common Issues
- Output format varies by model:
  - Some prepend `assistant:` or add Markdown fences (```json```).
  - Some omit required fields or slightly alter the structure.
  - Nested structures may be inconsistent or flattened unexpectedly. This was particularly the case with Mistral.
- Models may generate **extra explanations** or comments alongside the data.
- Inconsistent **data types** (numbers as strings, null vs missing fields).
- Missing **mandatory keys** in JSON or headers in CSV.
- Some models **truncate long outputs**, breaking the structure.
- Free-text injections may appear despite formatting instructions.

### Solutions
- Use **few-shot prompting** with examples to guide the structure.
- **Use of Strong models**: Models such as OpenAI or use of CoPilot (GitHub Copilot utilizes a variety of AI models to provide coding assistance, adapting to different tasks and user needs.OpenAI, Claude, Gemini) Strong support via JSON mode or function calling.
- **Other models**: Use parsers like **Pydantic** to validate and enforce the schema.

### Common Structured Outputs in Our Projects
- **JSON**: For APIs and downstream processing.  
- **CSV**: For tabular data export and analysis.

## Performance
### Performance Tips for LLMs

| Strategy                   | Description / Tips                                                                                       |
|-----------------------------|---------------------------------------------------------------------------------------------------------|
| **Streaming vs Batch**      | Stream for user-facing outputs (low latency). Batch multiple prompts with templates for high throughput. |
| **Prompt Optimization**     | Keep prompts concise. Reuse templates and few-shot examples efficiently.                                |
| **Token Management**        | Limit `max_tokens`. Use `stop` sequences to avoid unnecessary generation.                               |
| **Parallelization**         | Run independent requests concurrently. Use async frameworks or thread pools.                             |
| **Caching**                 | Cache repeated prompts/responses to reduce API calls and latency.                                       |
| **Model Selection**         | Use smaller/faster models for simple tasks; larger models for complex reasoning or high-quality output. |
| **Tooling Integration**     | Use RAG or vector databases to reduce redundant computation.                                           |
| **Error Handling & Retry**  | Implement retries with exponential backoff. Validate outputs to reduce downstream errors.               |
| **Function/Structured Output** | Use function calls or structured outputs to reduce parsing and token overhead.                        |
| **Monitoring & Metrics**    | Track latency, token usage, and response quality to identify bottlenecks and optimize usage.           |

* Writing templates for prompts help reusable prompts.
* Some frameworks support, **Imperative or Declarative Composition** which helps in explicitly controlling the sequence and flow of operations with LLMs, tools, and data, rather than relying on declarative pipelines. It’s especially relevant when you need precise control over prompts, model calls, or conditional logic.


## RAG (Retrieval-Augmented Generation)

  - Models have limited knowledge in the context of a specific business use case or problem, augmenting it with Business related knowledge base is essential. RAG Combines retrieval of relevant documents with LLM generation. Helps LLMs answer questions using external knowledge beyond their training data.

- **Key Issues:**  
  - Large context data can overwhelm the model.  
  - Must split data into appropriately sized documents.  
  - Too much context requires the model to filter irrelevant info → risk of hallucination.

- **Common Approaches:**  
  - Indexing documents for fast retrieval.  
  - Retrieval of top-k relevant documents before generation.  
  - Hybrid methods combining multiple retrieval strategies.
    
## Embeddings

- **What it is:**  
  - An embedding model is an algorithm that converts a piece of text into a numerical representation of its meaning.  
  - The output is a long list of floating-point numbers, usually between 100 and 2,000 dimensions.  
  - These are called **dense embeddings**, where most dimensions have non-zero values, unlike sparse embeddings.  
  - Each number is a floating-point value representing a **semantic dimension** of the text.
  - **traveling the meaning** in space by using the elementary math operations of addition and subtraction: for instance, the operation king – man + woman = queen. If you take the meaning (or semantic embedding) of king, subtract the meaning of man, presumably you arrive at the more abstract meaning of monarch, at which point, if you add the meaning of woman, you’ve arrived close to the meaning (or embedding) of the word queen. 

- **Semantic Embeddings:**  
  - Capture the meaning of text in such a way that similar texts have similar embeddings.  

- **Example:**  
  - Texts: `"Apple is a fruit"` vs `"Orange is a fruit"`  
  - Their embeddings will be vectors of floating-point numbers.  
  - The **cosine similarity** between these vectors will be high because their meanings are similar.  

- **Key Notes:**  
  - Each floating-point number represents a semantic aspect of the text.  
  - The vector as a whole encodes the overall meaning of the input text.
 
### Vector Stores and Embeddings: Problems Solved & Techniques

- **Problems They Solve:**  
  - **Semantic Search:** Find documents or text that are meaningfully similar to a query.
  - **Classification:** Assigning a new document to a previously identified group or label (for instance, a topic)
  - **Question Answering:** Retrieve relevant context for LLMs to answer questions accurately.  
  - **Recommendation Systems:** Suggest items based on similarity of embeddings.  
  - **Clustering & Topic Analysis:** Group similar content or detect topics.  
  - **Anomaly Detection:** Identify outliers by distance from typical embeddings.  

- **Techniques / Similarity Measures:**  
  - **Cosine Similarity:** Measures angle between vectors; commonly used for semantic similarity.  
  - **Euclidean Distance:** Measures straight-line distance in embedding space; good for spatial closeness.  
  - **Dot Product / Inner Product:** Measures magnitude-aligned similarity; often used in dense retrieval.  
  - **Approximate Nearest Neighbors (ANN):** Efficient search in large vector stores for top-k similar vectors.  

- **Workflow Example:**  
  1. Convert documents into embeddings.  
  2. Store embeddings in a vector store (e.g., FAISS, Pinecone, Weaviate).  
  3. Query with embedding of input text.  
  4. Retrieve top-k nearest embeddings using cosine similarity or ANN.  
  5. Use retrieved content for search, LLM context, or recommendations.  
## Strategies for Loading Documents into Chat Model Prompts

### 1. Template-Driven Solution Walkthroughs and Designs
- Many solution designs and documentation have structured templates and formats.  
- These templates often provide the **context needed for the LLM**.  
- Knowledge can be provided as plain text, PDF, or **Markdown** format.  
- Markdown is particularly useful because it can be easily converted to Confluence or other documentation tools using converters like `pandoc`.  

### 2. Representing Information
- Representing information in **tables** is effective.  
- Each cell corresponds to a **row and column**, making structured retrieval easier for the model.  

---

## Strategies for Splitting Text into Meaningful Chunks

### 1. Chunking with Overlap
- Split large text into chunks with a **character or token overlap** between chunks.  
- **Advantages:**  
  - Maintains context between chunks.  
  - Reduces risk of losing important information at chunk boundaries.  
- **Disadvantages:**  
  - Increases the total number of chunks → more embeddings and storage.  
  - Can introduce redundancy in retrieval.  

### 2. Language or Format-Aware Chunking
- Split based on the type of content:  
  - **Markdown or structured text:** split by headings, sections, or paragraphs.  
  - **Code (Python, etc.):** split by functions, classes, or logical blocks.  
- Ensures each chunk is **semantically coherent**.  

### 3. Maintaining References
- Keep a **reference to the original document** after splitting.  
- Useful for workflows like **Reflexion**, where you might need to trace information back to the source.  
- Helps the LLM provide **accurate citations or context**.  


## Embedding Models vs Chat Models

| Aspect | Embedding Models | Chat Models |
|--------|----------------|------------|
| **Purpose** | Convert text into **dense numerical vectors** representing semantic meaning. | Generate **natural language responses** given a prompt or conversation context. |
| **Input / Output** | Input: text or document; Output: high-dimensional vector (list of floats). | Input: text or conversation; Output: text (string). |
| **Use Cases** | Semantic search, similarity, clustering, recommendation, retrieval for RAG. | Chatbots, summarization, question answering, text completion. |
| **Training Objective** | Learn to encode semantic relationships in vector space. | Learn to predict next token in sequence and generate coherent text. |
| **Example Models** | OpenAI `text-embedding-3-small`, `text-embedding-3-large` | OpenAI `gpt-4`, `gpt-3.5-turbo` |
| **Interaction** | Usually **stateless** and fast; no conversation history required. | Stateful (can use conversation history) for context and coherence. |

**Key Point:**  
- Chat models may internally use embeddings (e.g., for context or RAG workflows), but they are **not the same as dedicated embedding models**.  
- Embedding models produce vectors for **semantic understanding**, while chat models produce **human-readable text**.

## Vector Stores
- Embeddings can be stored in a **vector store** for efficient retrieval.  
- In our context, the simplest options were **PgVector** and **FAISS**:  
  - **PgVector:** Integrated with PostgreSQL, making it easy to get security approval since it runs in RDS within a VPC.  
  - **FAISS:** In-memory vector store providing high-performance similarity search.  

# Using pgvector with Embedding Models

## 1. Flexibility
- pgvector is a **PostgreSQL extension** that stores and searches vector data efficiently.  
- You can store embeddings from any model: OpenAI (`text-embedding-3`), HuggingFace, custom embeddings, etc.  
- Queries like cosine similarity, Euclidean distance, or inner product can be applied regardless of the embedding source.

## 2. Why Embedding Model Choice Matters
- **Semantic quality:** Better embeddings produce more accurate similarity search results.  
- **Dimensionality:** pgvector supports different vector sizes, but you must define a fixed dimension when creating the column. All vectors in that column must have the same size.  
- **Use case alignment:**  
  - `text-embedding-3-small` → lightweight, lower cost, suitable for smaller semantic search.  
  - `text-embedding-3-large` → higher dimensional, better for nuanced semantic similarity.  
- **Consistency:** If you mix embeddings from different models in the same column, similarity calculations may be meaningless.  

## 3. Best Practices
- Pick a **single embedding model per vector column**.  
- Match vector dimension with the model output.  
- Use an embedding model appropriate for your application (search, clustering, recommendation).  

## Vector Stores
- Embeddings can be stored in a **vector store** for efficient retrieval.  
- In our context, the simplest options were **PgVector** and **FAISS**:  
  - **PgVector:** Integrated with PostgreSQL, making it easy to get security approval since it runs in RDS within a VPC.  
  - **FAISS:** In-memory vector store providing high-performance similarity search.  

# Using pgvector with Embedding Models

## 1. Flexibility
- pgvector is a **PostgreSQL extension** that stores and searches vector data efficiently.  
- You can store embeddings from any model: OpenAI (`text-embedding-3`), HuggingFace, custom embeddings, etc.  
- Queries like cosine similarity, Euclidean distance, or inner product can be applied regardless of the embedding source.

## 2. Why Embedding Model Choice Matters
- **Semantic quality:** Better embeddings produce more accurate similarity search results.  
- **Dimensionality:** pgvector supports different vector sizes, but you must define a fixed dimension when creating the column. All vectors in that column must have the same size.  
- **Use case alignment:**  
  - `text-embedding-3-small` → lightweight, lower cost, suitable for smaller semantic search.  
  - `text-embedding-3-large` → higher dimensional, better for nuanced semantic similarity.  
- **Consistency:** If you mix embeddings from different models in the same column, similarity calculations may be meaningless.  

## 3. Best Practices
- Pick a **single embedding model per vector column**.  
- Match vector dimension with the model output.  
- Use an embedding model appropriate for your application (search, clustering, recommendation).  

```python
# 1. Semantic Search
query = "Find documents about long documents."
results = pgvector_store.similarity_search(query, k=3)

# 2. Question Answering
answer = qa.run("What does the document talk about?")

# 3. Classification
nearest_docs = pgvector_store.similarity_search("New text to classify", k=1)
predicted_label = nearest_docs[0].metadata.get("label")

# 4. Recommendation
recommendations = pgvector_store.similarity_search("Guide on API design", k=5)

# 5. Clustering
all_embeddings = pgvector_store.get_embeddings()  # then apply KMeans externally

# 6. Anomaly Detection
new_embedding = embeddings.embed_query("Some unusual text.")
nearest = pgvector_store.similarity_search_by_vector(new_embedding, k=1)
```

## Vector DB Issues  
- **Document Change Tracking**: Use a SQL record manager or similar system to track document updates.  
- **Design Pattern**: Follows *CQRS (Command Query Responsibility Segregation)* principle — separate write (doc updates) and read (retrieval) models for consistency.  
- **Approach**: Maintain unique IDs across vector store and doc store for sync.  

## Indexing Optimization  
- **Problem**: Mixed-content documents (text + tables) can lose structure if split only by text.
- 
- **Approach 1**: Use **MultiVector Retrieval** —  
    - Store summaries or embeddings in **vector store**.  
    - Store original content (tables, full text) in **doc store** (RDBMS, NoSQL, object store, or in-memory).  
    - Link via **ID references**.  
    
```python
# Helper function to fetch docs from MySQL
def fetch_docs_from_mysql(ids):
    placeholders = ','.join(['%s'] * len(ids))
    query = f"SELECT id, content, metadata FROM documents WHERE id IN ({placeholders})"
    mysql_cursor.execute(query, tuple(ids))
    rows = mysql_cursor.fetchall()
    return [Document(page_content=row['content'], metadata=row['metadata']) for row in rows]

# 3. Create MultiVectorRetriever
retriever = MultiVectorRetriever(
    vectorstore=pgvector_store,
    docstore=fetch_docs_from_mysql,
    id_key="id"
)
```

or 
```python
docstore = InMemoryDocstore()

# 2. Add documents to InMemoryDocstore
doc_ids = ["doc1", "doc2"]
chunks = [
    Document(page_content="First document about LangChain.", metadata={"category": "AI"}),
    Document(page_content="Second document about Vector Stores.", metadata={"category": "Database"})
]
docstore.mset(list(zip(doc_ids, chunks)))

# 3. Create MultiVectorRetriever
retriever = MultiVectorRetriever(
    vectorstore=pgvector_store,  # Same as before
    docstore=docstore,           # InMemoryDocstore instance
    id_key="id"                  # ID used in vector store entries
)
```

- **Approach 2**: Use *Recursive Abstractive Processing for Tree-Organized Retrieval (RAPTOR) ** —  
- **Problem:**  
  - RAG systems must handle:
    - **Lower-level questions:** referencing specific facts in a single document.  
    - **Higher-level questions:** synthesizing ideas across multiple documents.  
  - Standard k-nearest neighbors (k-NN) retrieval on document chunks struggles to cover both types effectively.  

- **Solution: RAPTOR Approach**
  - **Step 1:** Create **document summaries** capturing higher-level concepts.  
  - **Step 2:** **Embed and cluster** the documents based on semantic similarity.  
  - **Step 3:** **Summarize each cluster**, producing higher-level abstractions.  
  - **Step 4:** Repeat the process **recursively**, forming a **tree of summaries** with increasing abstraction.  

- **Indexing:**  
  - Index **both the summaries and the original documents** together.  
  - Ensures coverage for **questions ranging from low-level facts to high-level concepts**.

- **Benefit:**  
  - Efficient handling of **multi-granular retrieval**.  
  - Supports queries spanning **single facts to overarching ideas**.
 
    
```python
# 2. Split documents into chunks
docs = [Document(page_content=doc) for doc in all_documents]  # all_documents is your text list
splitter = RecursiveCharacterTextSplitter(chunk_size=500, chunk_overlap=50)
chunks = []
for doc in docs:
    chunks.extend(splitter.split_text(doc.page_content))

# 3. Generate summaries for each chunk
chunk_summaries = []
for chunk in chunks:
    summary = llm(f"Summarize the following text concisely:\n{chunk}")
    chunk_summaries.append(Document(page_content=summary))

# 4. Cluster summaries
num_clusters = 5
summary_embeddings = [embeddings.embed_query(s.page_content) for s in chunk_summaries]
kmeans = KMeans(n_clusters=num_clusters, random_state=0).fit(summary_embeddings)

# 5. Summarize each cluster (recursive abstraction)
cluster_summaries = []
for cluster_idx in range(num_clusters):
    cluster_docs = [chunk_summaries[i].page_content for i in range(len(chunk_summaries)) 
                    if kmeans.labels_[i] == cluster_idx]
    cluster_text = "\n".join(cluster_docs)
    cluster_summary = llm(f"Summarize the following cluster text:\n{cluster_text}")
    cluster_summaries.append(Document(page_content=cluster_summary))

# 6. Index both original chunks and cluster summaries in vector store
vectorstore.add_documents(chunks + cluster_summaries)

# 7. Query example
query = "Explain high-level ideas from the documents."
results = vectorstore.similarity_search(query, k=3)
for r in results:
    print(r.page_content)
```

## ColBERT: Optimizing Embeddings

- **Problem with standard embeddings:**  
  - Fixed-length embeddings compress entire text into a single vector.  
  - Useful for retrieval, but embedding irrelevant/redundant content can cause **hallucination** in LLM outputs.  

- **ColBERT Approach:**  
  1. **Contextual token embeddings:** Generate embeddings for **each token** in the document and query instead of a single vector.  
  2. **Token-level similarity scoring:** Calculate similarity between **each query token** and **all document tokens**.  
  3. **Aggregate scores:** For each query token, take the **maximum similarity** to any document token; sum these to get a **document-level score**.  

- **Benefits:**  
  - Provides **granular, token-level retrieval**.  
  - Reduces irrelevant content impact.  
  - Improves accuracy of retrieved context for LLMs.  

- **Key takeaway:**  
  - ColBERT is an embedding model designed to implement this **token-level scoring mechanism**, optimizing document retrieval for downstream applications.


```python
from ragatouille import RAGPretrainedModel
# Load the ColBERT-based RAG model
RAG = RAGPretrainedModel.from_pretrained("colbert-ir/colbertv2.0")

# Example usage: encode documents or queries
docs = ["LangChain helps build applications with LLMs efficiently."]
query = "How to use LangChain for LLM apps?"

# Encode the documents (token-level embeddings)
doc_embeddings = RAG.encode_documents(docs)

# Encode the query
query_embedding = RAG.encode_query(query)

# Retrieve top-k relevant documents
results = RAG.retrieve(query_embedding, k=3)
for r in results:
    print(r)
```

