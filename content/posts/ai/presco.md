+++
date = '2025-05-20T12:44:47+10:00'
draft = false
title = 'presco'
tags = ['LLM', 'Design Patterns']
+++

LLM design patterns are reusable strategies for building robust, efficient, and scalable AI applications. They help developers structure retrieval, reading, rewriting, memory, agent, and orchestration workflows for large language models. These patterns improve performance, maintainability accuracy, cost and security.

## Introduction
Instruction were 2, 1. keep it basic 2. AI WG experinces -  3 usecases are in progress. we will be sharing some basics wrt to the learnings as strategies or design patterns here. if haven't already will go through.
* security arch approvals
* cost
* availablility of an appropriate model 
* model support for context size
* amount of data in the knowledge base.
* format of the data (e.g table, plantuml xmls)
* challenges with the quality of context data.
* Speed of models

Before we proceed setting the stage.

## LLMs
- GPT-3: 175B Parameters, ~350B tokens. GPT-4:is 6x bigger. GPT-5 was supposed to be 20x bigger but is counter intuitive 300B Parameters.
- Chinchilla's Law: model performance optimal when training tokens ≈ 20 × model parameters.
    - Example: 70B parameters → ~1.4T tokens needed.
    - hundreds of billions/trillions of parameters requires enormous data more than available high-quality text.
  - GPT-5 leverages on many architectural innovations like:
    - Unified Intelligence System: integrates multiple reasoning and perception modules for more general intelligence.
    - Mixture-of-Experts: routes inputs to specialized sub-models for improved efficiency and accuracy.
    - Multimodal Integration: processes and understands text, images, and other data types together.
- Sometimes we have bigger models but often we have restrictions using best available model due reasons mentioned before. Hence we have to compensate with design patterns. we will be going to few models available to atleast the Fintech and how do we get past some of the common issues.

## Transformer Architecture: 
  - LLMs use the transformer neural network architecture.
  - Transformers understand relationships between words, regardless of their position in the text.
  - The architecture enables prediction of the next word in a sequence. that is to say they should not expected to perform for accurate mathematical computation; lot of our AI usecases some have some math involved.

## Tokens:
  - A token is a chunk of text, it could be entire word or part.
  - Roughly, one token is about 4 characters or for calculation sake 75% of  words in English language.
  - why important? - for us to estimate monthly cost: (tokens used per month) × (API cost per token).
  - If transaction rate is T tokens/sec, that's about (T × 0.75) words/sec. (include ss)

## LLM Model Variants and Techniques:
  - Two main techniques:
    - Predict next word (causal language modeling): Used by models like GPT; generates text by predicting the next token in a sequence.
    - Predict masked word: Used by models like BERT; predicts masked tokens within a sentence for better understanding of context.
  - GPT models: Focus on text generation, conversation, and completion tasks.
  - BERT models: Focus on understanding, classification, and extracting information from text.
  - Other flavours:
    - Encoder-only (BERT): Good for understanding and classification.
    - Decoder-only (GPT): Good for generation and completion.
    - Encoder-decoder (T5, BART): Good for translation, summarization, and more complex tasks.
  - Many LLMs are specialized for tasks like code generation, multimodal input (text + images), or domain-specific knowledge.


## Chat Models
- Chat models are specialized LLMs designed for conversational interactions.

| Model                                                                                                        | Provider       | Strengths                                   | Typical Use Cases                                 |
|--------------------------------------------------------------------------------------------------------------|----------------|---------------------------------------------|---------------------------------------------------|
| Copilot                                                                                        |  Copilot utilizes Mixture-of-Experts - uses variety of AI models to provide coding assistance, adapting to different tasks and user needs. OpenAI and Microsoft's property models and tools      | Text generation, conversation, code, summarization | Chatbots, assistants, writing, code, content      |
| LLaMA                                                                                                        | Meta           | Open-source, efficient, adaptable           | Research, custom training, open-source apps       |
| Claude                                                                                                       | Anthropic      | Safety-focused, reliable, conversational    | Support, safe chatbots, document analysis         |
| Mistral                                                                                                      | Mistral AI     | Kind of something from all aspects - Efficient, open weights, strong benchmarks  | Research, production NLP, open-source projects    |
| Gemini                                                                                                       | Google DeepMind | Multimodal (text, image, audio), reasoning  | Multimodal assistants, content analysis           |
| Anthropic (Claude), Amazon (Titan), Meta (Llama),<br/>Mistral, AI21 Labs (Jurassic), Cohere (Command) | Amazon Bedrock | Wide model selection, enterprise integration, scalable APIs | Chatbots, search, summarization, enterprise AI    |

## Popular LLM Tools and Frameworks

| Tool/Framework         | Language   | Focus/Strengths                  | Integration      | Use Case Examples              |
|-----------------------|------------|----------------------------------|------------------|-------------------------------|
| LangChain             | Python     | Chaining, agents, retrieval      | Many LLM APIs    | Chatbots, RAG, workflows      |
| LangGraph             | Python     | Multi-agent, graph orchestration | LangChain        | Reasoning, modular agents     |
| Spring AI             | Java       | Enterprise, abstraction          | Spring ecosystem | Business apps, backend        |
| HF Transformers       | Python     | Model training, deployment       | Model hub, APIs  | NLP tasks, research, prod     |
| Agentic AI (AutoGPT, CrewAI, N8N) | Python/JS | Autonomous agents, automation | Various          | Task automation, multi-agent  |

## Prompt
- A prompt is the input text or set of instruction given to an LLM to guide its response. 
- Considerations for prompts:
  - **Clarity**: Avoiding ambiguity to get accurate results. Cannot use our own DSLs. 
  - **Context**: Provide relevant background or examples.
  - **Length**: Too short may lack detail; too long may confuse or dilute intent.
  - **Structure**: Use formatting, lists, or step-by-step instructions for better outputs.
  - **Constraints**: Specify requirements, style, or limitations as needed.
  - **Iteration**: Refine prompts based on model responses to improve outcomes.
  - **Inconsistent results**: Due to different models and also different model parameters.

## Prompt Engineering and Patterns
- Prompt engineering is the practice of designing and refining prompts to optimize LLM outputs.
- Prompt engineers experiment with wording, structure, and context to achieve desired results.
- Common patterns:

| **Type**                       | **Definition**                                                       | **Example**                                                                 |
|--------------------------------|----------------------------------------------------------------------|------------------------------------------------------------------------------|
| **Single-String Prompting**    | One large text prompt, meant to be completed.             | `Translate to French: "How are you?"`                                      |
| **Chat-Based Prompting**       | Structured messages with roles (`system`, `user`, `assistant`).     | System: "You are helpful." User: "Translate 'How are you?' to French."     |
| **Zero-Shot**                  | No examples provided; just the instruction.                         | `Summarize this text in one sentence: ...`                                  |
| **Few-Shot**                   | Include a few examples to guide the output.                         | `Q: Capital of France? A: Paris. Q: Capital of Germany? A:`                |
| **Chain-of-Thought (CoT)**     | Ask model to reason step-by-step before answering.                  | `Explain step by step: If you have 3 apples and eat 1, how many are left?` |
| **Self-Consistency**           | Model generates multiple solutions, picks most consistent.          |  reasoning-heavy tasks. Why is the balance showing at $200 instead of $100? Generate multiple reasoning paths                                              |
| **Role-Based / Persona**       | Assign a role or persona for better context.                        | `Act as an expert Python tutor. Explain decorators.`                        |
| **Instruction-Based**          | Direct task-oriented commands without dialogue.                     | `Extract all email addresses from the text.`                                |
| **Structured Output**          | Request output in JSON, table, or specific format.                  | `Return the answer in JSON with keys: name, age.`                           |
| **ReAct (Reason + Act)**       | Model reasons, then calls tools or APIs.                            | `Thought: I need weather info. Action: call weather API.`                   |
| **Retrieval-Augmented (RAG)**  | Combine prompt with retrieved external knowledge.                   | `[Context] Answer based on above.`                                          |
| **Multimodal Prompting**       | Combines text + images (or other modalities).                       | `Describe the scene in this image.`                                         |
| **Prompt Assiting**       | Similar to meta prompting but using copilot to generate prompts for mistral                       | `Describe the scene in this image.`                                         |
| **Prompt Chaining**            | Splits a task into multiple linked prompts.                         | Step 1: Summarize → Step 2: Extract entities → Step 3: Generate questions. |
| **Reflection / Deliberation**  | Ask model to review or critique its own response.                   | `Check your previous answer and improve it.`                                |
| **Dynamic Prompt Composition** | Build prompts programmatically for personalization.                 | Insert user name, context dynamically from a database.                      |
| **Tool Calling**               | Enable model to trigger external tools for answers.                 | `If math needed, call calculator function.`                                  |
| **Function Calling**           | Model outputs structured JSON to call specific function.            | `{ "function": "get_weather", "location": "Paris" }`                        |

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
Structured output model returns data in a **specific or predefined, machine-readable format** like JSON or CSV, instead of free-form text.

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
- Use **prompt engeinnering techniques** with examples to guide the structure.
- **Use of Strong models**: Models such as OpenAI or use of CoPilot Strong support via JSON mode or function calling.

## Output & performance

| Strategy                   | Description / Tips                                                                                       |
|-----------------------------|---------------------------------------------------------------------------------------------------------|
| **Streaming vs Batch**      | Stream for user-facing outputs (low latency). Batch multiple prompts with templates for high throughput. |
| **Prompt Optimization**     | Keep prompts concise. Reuse templates and few-shot examples efficiently.                                |
| **Token Management**        | Limit `max_tokens`. Use `stop` sequences to avoid unnecessary generation.                               |
| **Parallelization**         | Run independent requests concurrently. Use async frameworks or thread pools.                             |
| **Prompt Caching**                 | Cache repeated prompts/responses to reduce API calls and latency.                                       |
| **Model Selection**         | Use smaller/faster models for simple tasks; larger models for complex reasoning or high-quality output. |
| **Tooling Integration**     | Use RAG or vector databases to reduce redundant computation.                                           |
| **Function/Structured Output** | Use function calls or structured outputs to reduce parsing and token overhead.                        |

* Writing templates for prompts help reusable prompts.
* Some frameworks support, **Imperative or Declarative Composition** which helps in controlling the sequence and flow of operations with LLMs, tools, and data. precise control over prompts, model calls, or conditional logic.


## Embeddings
- Embeddings are dense vector representations of text (words, sentences, or documents) generated by LLMs.
- advantage is they capture semantic meaning, allowing for usecases - **semantic search, recommendation systems, document classification, clustering, and information retrieval**.
- Common models for embeddings: **OpenAI Embeddings, Cohere, Sentence Transformers, BERT.**

  - An embedding model is an algorithm that converts a text into a numerical representation of its meaning.  
  - The output is a long array of floating-point numbers called dimensions.  
  - These are called **dense embeddings**, where most dimensions have non-zero values.  
  - Each number is a floating-point value representing a **semantic dimension** of the text.
  - **traveling the meaning** in space by using the elementary math operations of addition and subtraction: for instance, the operation king – man + woman = queen. take the meaning (or semantic embedding) of king, subtract the meaning of man, I guess you reach something like a ruler, add woman, would've arrived close to word queen. 
  
- Embedding models produce vectors for **semantic understanding**, while chat models produce **human-readable text**.

## Model Paramaters
| Parameter            | Description                                                                                     | Typical Range        | Impact                                                                 |
|----------------------|-------------------------------------------------------------------------------------------------|----------------------|------------------------------------------------------------------------|
| **temperature**      | Controls randomness. Lower = deterministic, higher = creative/unpredictable.                  | `0.0` – `2.0`       | `0.0` = deterministic, `1.0` = balanced, `>1.2` = very random.        |
| **top_p**            | Nucleus sampling. keep adding tokens from smallest set until the cumulative probability ≥ p.           | `0.1` – `1.0`       | Lower = more focused, 1.0 = no restriction.                           |
| **top_k**            | Limits token selection to the k most probable tokens at each step.                                           | `1` – `100`         | Low values reduce creativity, high values allow more variation.       |
| **max_tokens**       | Maximum tokens to generate in the response.                                                   | Depends on model    | Controls output length.                                               |
| **min_tokens**       | Minimum tokens to generate before stopping.                                                   | Depends on model    | Ensures longer answers if needed.                                     |
| **presence_penalty** | Penalizes tokens already present in the text (encourages new topics).                          | `-2.0` – `2.0`      | Higher = more diversity.                                              |
| **frequency_penalty**| Penalizes frequent tokens to reduce repetition.                                               | `-2.0` – `2.0`      | Higher = less repetition.                                             |
| **stop**             | List of stop sequences where generation should halt.                                          | Strings / tokens    | Useful for structured responses.                                      |
| **seed**             | Fixes randomness for reproducibility.                                                         | Integer             | Same seed = same output (with sampling).                              |
| **length_penalty**   | Adjusts likelihood for longer sequences in beam search.                                       | `>0`                | Higher = longer outputs favored.                                      |
| **early_stopping**   | Stops beam search when best candidates are found.                                             | `true` / `false`    | Speeds up generation, may miss better completions.                    |
| **logit_bias**       | dictionary to control probability of certain token ids   | Useful for forcing or avoiding words.                                 |
| **echo**             | Return the prompt along with the completion.                                                  | `true` / `false`    | For debugging or prompt reconstruction.                                |


## RAG (Retrieval-Augmented Generation)
- Models have limited knowledge in the context of a specific business use case or problem, augmenting it with Business related knowledge base is essential. RAG Combines retrieval of relevant documents with LLM generation. Helps LLMs answer questions using external knowledge beyond their training data.
  
- **3 stages**
  - **Indexing:** create and storing embeddings of data in a vector store.
  - **Retrieval:** retrieving the relevant embeddings and data from vector store
    - **Techniques / Similarity Measures:**  
      - **Cosine Similarity:** Measures angle between vectors; commonly used for semantic similarity.  
      - **Euclidean Distance:** Measures straight-line distance in embedding space; good for spatial closeness.  
      - **Dot Product / Inner Product:** Measures magnitude of similarity; 
      - **Approximate Nearest Neighbors (KNN):** Efficient search in large vector stores for top-k similar vectors.  
  - **Generation:** Augmenting the original prompt with the relevant retrieved documents. 

- **Key Issues you may face:**  
  - Large context data cause the model to give incorrect results.  
  - will have to split data into appropriately sized documents which will cause incorrect results.  
  - Too much context requires the model to filter irrelevant info → risk of hallucination.

- **Common Approaches:**  
  - Indexing documents for fast retrieval.  
  - Retrieval of top-k relevant documents before generation.  
  - Hybrid methods combining multiple retrieval strategies.


## Vector Store
- A vector store is a database for storing and searching embeddings.
- good for similarity search and retrieval of relevant documents or data points based on vector operations.
- Popular vector stores: Pinecone, FAISS, PgVector.
- Use cases: retrieval-augmented generation (RAG), semantic search and knowledge management.

### Vector Stores and Embeddings: Problems Solved & Techniques

- **Problems They Solve:**  
  - **Semantic Search:** Find documents or text that are meaningfully similar to a query.
  - **Classification:** Assigning a new document to a previously identified group or label (for instance, a topic)
  - **Question Answering:** Retrieve relevant context for LLMs to answer questions accurately.  
  - **Recommendation Systems:** Suggest items based on similarity of embeddings.  
  - **Clustering & Topic Analysis:** Group similar content or detect topics.  
  - **Anomaly Detection:** Identify outliers by distance from typical embeddings.



## Strategies for Loading Documents into Chat Model Prompts

### 1. Template-Driven Solution Walkthroughs and Designs
- Many solution designs and documentation have structured templates and formats.  
- These templates often provide the **context needed for the LLM**.  
- Knowledge can be provided as plain text, PDF, or **Markdown** format.  
- Markdown is particularly useful because it can be easily converted to Confluence or other documentation tools using converters like `pandoc`.  

### 2. Representing Information
- Representing information in **tables** is effective.  
- Each cell corresponds to a **row and column**, making structured retrieval easier for the model.  

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

## Vector Stores
- Embeddings can be stored in a **vector store** for efficient retrieval.  
- In our context, the simplest options were **PgVector** and **FAISS**:  
  - **PgVector:** Integrated with PostgreSQL, making it easy to get security approval since it runs in RDS within a VPC.  
  - **FAISS:** In-memory vector store providing high-performance similarity search.  

### Using PgVector with Embedding Models

* 1. Flexibility
  - PgVector is a **PostgreSQL extension** that stores and searches vector data efficiently.  
  - You can store embeddings from any model: OpenAI (`text-embedding-3`), HuggingFace, custom embeddings, etc.  
  - Queries like cosine similarity, Euclidean distance, or inner product can be applied regardless of the embedding source.

* 2. Why Embedding Model Choice Matters
  - **Semantic quality:** Better embeddings produce more accurate similarity search results.  
  - **Dimensionality:** PgVector supports different vector sizes, but you must define a fixed dimension when creating the column. All vectors in that column must have the same size.  
  - **Use case alignment:**  
    - `text-embedding-3-small` → lightweight, lower cost, suitable for smaller semantic search.  
    - `text-embedding-3-large` → higher dimensional, better for nuanced semantic similarity.  
  - **Consistency:** If you mix embeddings from different models in the same column, similarity calculations may be meaningless.  

* 3. Best Practices
  - Pick a **single embedding model per vector column**.  
  - Match vector dimension with the model output.  
  - Use an embedding model appropriate for your application (search, clustering, recommendation).  

* Vector Stores
  - Embeddings can be stored in a **vector store** for efficient retrieval.  
  - In our context, the simplest options were **PgVector** and **FAISS**:  
    - **PgVector:** Integrated with PostgreSQL, making it easy to get security approval since it runs in RDS within a VPC.  
    - **FAISS:** In-memory vector store providing high-performance similarity search.  

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
- **Document Change Tracking**: Use a SQL record manager library or similar strategies to track document updates.
  - Versioning with Metadata: Each document update creates a new version; store version_id in metadata.
  -   Hash-Based Updates: Compute hash for each chunk; update only changed chunks.
  - Soft Deletes (Active Flag): Mark old chunks as is_active=False and insert new ones.
  ```python
  vectorstore.similarity_search(query, filter={"is_active": True})
  ```
- **Design Pattern**: Follows *CQRS (Command Query Responsibility Segregation)* principle — separate write (doc updates) and read (retrieval) models for consistency.  
- **Approach**: Maintain unique IDs across vector store and doc store for sync.  

## Indexing Optimization Patterns
**Problem**: Mixed-content documents (text + tables) can lose structure if split only by text.
### MultiVector Retrieval  
<img width="1200" height="611" alt="image" src="https://github.com/user-attachments/assets/830dff2f-637f-4987-9825-44a56cacb205" />
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

### Recursive Abstractive Processing for Tree-Organized Retrieval (RAPTOR) —  
<img width="2274" height="1330" alt="image" src="https://github.com/user-attachments/assets/0aefd58f-99a9-47dd-9510-91326c91b4a1" />

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

### ColBERT: Optimizing Embeddings
<img width="1400" height="578" alt="image" src="https://github.com/user-attachments/assets/cc1d9783-9da8-4220-a1c4-e7b48beb5e16" />

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

---

## Effective Strategies Using RAG

- Part of our data can be stored in a **vector store** for operations like semantic search.  
- Depending on the data type, it may be more efficient to store data in **RDBMS** or **NoSQL** or **Object Store**.  

### Query Transformation
- Incoming inputs can be **varied and uncontrolled**, e.g.:  
  1. Event-driven data  
  2. Future integration with other systems  
  3. User interface inputs  
- **Solution:** Transform queries into a format the system can reliably answer.  
- Benefits:  
  - Ensures consistent processing across diverse inputs.  
  - Helps address security concerns and prevents misuse.  

### Step-Back Prompting
- Ask the model to **analyze or reflect** before giving a final answer.  
- Helps identify assumptions, gaps, or errors in reasoning.  
- Reduces mistakes in **multi-step reasoning**.

### Subquestion Prompting
- Breaks a **complex question into smaller subquestions**.  
- Answer each subquestion individually and aggregate results.  
- Improves accuracy for **multi-part queries** and reduces hallucination.

### Rewritten Prompting aka Rewrite-Retrieve-Read 
- Reformulates a query to **clarify intent or simplify language**.  
- Ensures the LLM focuses on the intended question.  
- Reduces misinterpretation and improves output quality.
  
### Multi-Query Retrieval
<img width="1676" height="596" alt="image" src="https://github.com/user-attachments/assets/595030dc-1a2b-4fa4-8a82-4ec58822a72d" />

- **Problem:** A single user query may not capture the full scope of information needed for a comprehensive answer.  

- **Solution:** Multi-query retrieval strategy:
  1. **Query Expansion:** Use an LLM to generate multiple related queries from the user’s initial query.  
  2. **Parallel Retrieval:** Execute each generated query against the data source (vector store, RDBMS, etc.).  
  3. **Context Aggregation:** Combine retrieved results as prompt context for the LLM.  
  4. **Final Output:** The LLM generates a more complete and accurate answer using the aggregated context.  

- **Benefit:** Improves coverage and accuracy by capturing **all relevant information** across the dataset.
- **Example**: What is the weather in Sydney?”, give me 5 possible queries:
    1. What is the current temperature in Sydney?
    2. Are there any weather warnings or alerts in Sydney right now?
    3. What is the forecast for Sydney for the next few hours?
    4. Is it sunny, rainy, or cloudy in Sydney currently?
    5. What is the humidity and wind speed in Sydney today?

### RAG-Fusion
<img width="1284" height="481" alt="image" src="https://github.com/user-attachments/assets/9597f42d-7e23-40f5-985e-cabef52035b3" />

RAG-Fusion (Retrieval-Augmented Generation with Fusion) is an extension of the multi-query retrieval strategy. It enhances the retrieval process by introducing a **final reranking step** using the **Reciprocal Rank Fusion (RRF)** algorithm.

### Key Steps

1. **Query Expansion:** Generate multiple related queries from the user's initial query.
2. **Parallel Retrieval:** Execute each query independently against the data source (vector store, RDBMS, or search engine).
3. **Reciprocal Rank Fusion (RRF):**  
   - Each retrieved document has a rank for each query.  
   - RRF combines these ranks into a single, unified ranking.  
   - Formula: ```math  RRF Score = \sum_{i} \frac{1}{k + \text{rank}_i}``` where \(k\) is a constant (commonly 60) to reduce the effect of lower-ranked documents. a big contant so that the rank doesn't domainate and have advantage.
   - The most relevant documents across all queries rise to the top.
4. **Context Aggregation:** Use the top-ranked documents as context for the LLM.
5. **Final Output:** LLM generates a more accurate and comprehensive answer using aggregated, reranked context.

#### Benefits

- Improves retrieval quality by prioritizing documents relevant to multiple query perspectives.
- Handles queries with different scoring scales or distributions effectively.
- Reduces noise from less relevant results while promoting consensus across queries.

#### Use Cases

1. **Legal or Compliance like ACMA or TCP or Security documenations:**  
   - Searching across multiple regulations, rules, and previous incidents.  
   - RRF helps surface the most relevant documents that are supported across different search formulations.

2. **Enterprise Search:**  
   - Documents across Telstra for example Flexcab.

RAG-Fusion is particularly powerful when the information space is large and diverse, and a single query is insufficient to capture all relevant context.
## Hypothetical Document Embeddings (HyDE)
<img width="460" height="300" alt="image" src="https://github.com/user-attachments/assets/564420f8-9bd2-4f97-9e68-0e0dbcfb02f4" />

**HyDE** is a retrieval strategy that leverages LLMs to improve vector-based search by creating a **hypothetical document** from the user’s query. The idea is that the LLM can expand, paraphrase, or contextualize the query into a richer representation that is more semantically similar to relevant documents in the dataset.
HyDE effectively **bridges the gap between natural language queries and document embeddings**, improving the relevance of retrieved documents in retrieval-augmented generation (RAG) systems.
### How HyDE Works
  - The user provides a query, e.g., `"What is the current Balance and give step by step how you arrive at that."`
  - An LLM generates a **hypothetical document** or passage as if it were an answer to the query.  
  - The hypothetical document is converted into a **vector embedding** using the same embedding model as used for the document database.
  - The embedding is used to perform a **vector search** against the document corpus.  
  - The assumption: the LLM-generated document is **closer in embedding space** to relevant documents than the raw query. 
  - Top-k similar documents are retrieved and can then be fed as context to the LLM for final answer generation. 

### Benefits

- **Query Expansion without Manual Effort:** LLM generates richer semantic content automatically.
- **Better Retrieval Accuracy:** Hypothetical documents are often closer to relevant documents in embedding space than terse user queries.
- **Works with Sparse Queries:** Short or ambiguous queries benefit from the additional context generated by the LLM.

---

## Query Routing

Query routing is a strategy used in retrieval or search systems to **direct a user query to the most relevant subset of data or service**. The goal is to improve retrieval efficiency, relevance, and response time. There are two main strategies: **logical routing** and **semantic routing**.

---

### 1. Logical Routing
Logical routing directs queries based on **predefined rules, categories, or metadata** associated with the documents or data sources.
- Documents are classified or tagged into **logical partitions** (e.g., departments, product lines, regions).  
- Queries are routed to the partition(s) that match certain **keywords, tags, or rules**.  

**Example:**  
```python
class RouteQuery(BaseModel):
    """Route a user query to the most relevant datasource."""
    datasource: Literal["python_docs", "js_docs"] = Field(
        ...,
        description="Choose the most relevant datasource based on keywords."
    )
```
---

### 2. Semantic Routing
Semantic routing directs queries based on **meaning or intent**, often using embeddings, LLMs, or vector similarity, rather than strict keywords or rules.

**How it works:**  
- Queries are converted into **semantic representations** (embeddings).  
- Documents or partitions are also represented in the same embedding space.  
- The system routes the query to the **most semantically relevant subset**.  

**Example:**  
```python
physics_template = """You are a very smart physics professor. You are great at     answering questions about physics in a concise and easy-to-understand manner.     When you don't know the answer to a question, you admit that you don't know. Here is a question: {query}"""
math_template = """You are a very good mathematician. You are great at answering     math questions. You are so good because you are able to break down hard     problems into their component parts, answer the component parts, and then     put them together to answer the broader question. Here is a question: {query}"""

# Embed prompts
embeddings = OpenAIEmbeddings()
prompt_templates = [physics_template, math_template]
prompt_embeddings = embeddings.embed_documents(prompt_templates)

# Route question to prompt
@chain
def prompt_router(query):
    query_embedding = embeddings.embed_query(query)
    similarity = cosine_similarity([query_embedding], prompt_embeddings)[0]
    most_similar = prompt_templates[similarity.argmax()]
    print("Using MATH" if most_similar == math_template else "Using PHYSICS")
    return PromptTemplate.from_template(most_similar)
```
**Use Cases:**  
- Logical routing: Enterprise databases, departmental knowledge bases, FAQs.  
- Semantic routing: RAG systems, multi-domain knowledge search, chatbots, recommendation engines.  

## Query Construction

Query construction is the process of **transforming a user's natural language query into a structured query** that can be executed against various data sources. This is essential for retrieval systems, vector stores, and relational databases.

---

## 1. Text-to-Metadata Conversion

Vector stores often support **metadata-based filtering**, allowing more precise searches. During the embedding process:

- **Attach metadata**: Each vector can be associated with key-value pairs (e.g., document type, author, date)
- **Filter on query**: When performing a search, you can specify metadata filters to narrow down results

1. **Embed documents and attach metadata:**
   ```python
   {
       "text": "Annual financial report 2024",
       "embedding": [...],
       "metadata": {"year": 2024, "type": "report"}
   }
   ```

2. **Construct a query with metadata filters:**
   ```python
   query_embedding = embed("Financial summary 2024")
   results = vector_store.search(
       query_embedding,
       filter={"year": 2024, "type": "report"}
   )
   ```

### Self-Querying Approach
An LLM can translate a natural language query into metadata filters automatically.

**Example:** "Show event by event name and event publisher" → `{"event_name": "payment event", "event_publisher": "payment system"}`

---

## 2. Text-to-SQL
Relational databases require SQL queries, which are not naturally compatible with human language. Text-to-SQL allows LLMs to translate user queries into SQL queries.

### Strategies for Effective Translation
#### Database Description (Grounding SQL)
Provide the LLM with table definitions using `CREATE TABLE` statements, including:
- Column names and types
- Sample rows (typically 2-3 examples)
This helps the LLM generate syntactically and semantically correct SQL queries.

#### Few-Shot Examples

Include question-to-SQL examples in the prompt to guide query generation.

**Example:**
* Q: Total salary of HR employees
* SQL: SELECT SUM(salary) FROM employees WHERE department='HR';

#### Error Handling
When SQL execution fails, the LLM can:
- Regenerate the query based on error messages
- Repair the existing query with corrections
- Improve robustness when working with dynamic or unfamiliar schemas

## Summary
| Query Construction Type | Description | Key Techniques |
|------------------------|-------------|----------------|
| **Text-to-Metadata** | Attach metadata to vectors and filter during search | Metadata key-value pairs, LLM-assisted filter extraction |
| **Text-to-SQL** | Translate natural language to SQL queries | Database description, few-shot examples, error recovery |

These strategies enable LLMs and retrieval systems to effectively interact with both unstructured and structured data, ensuring more accurate and relevant results.

