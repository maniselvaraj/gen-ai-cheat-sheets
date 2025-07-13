RAG


RAG Fundamentals

**What is RAG?**

Retrieval Augmented Generation (RAG), a technique that fetches data from company data sources and enriches the prompt to provide more relevant and accurate responses.

**Why do we need RAG?**

* LLMs are pre-trained on some “set” of data. It is from the past. Knowledge is cut off. This is also referred as “Parametric knowledge”
* Organizations need to query **domain-specific, proprietary data** to answer questions. We need to pass “Source knowledge” to the LLM.
* Options to circumvent the knowledge cut off are:
  + Train the LLM again i.e., Fine tune
  + RAG

## Comparing Off the shelf LLM vs RAG vs Fine-tuning

| **Off Shelf LLM** | **RAG** | **Fine Tuned LLM** |
| --- | --- | --- |
| * Easy to set up and use * Cannot add domain specific data | * Easy to set up * Builds on top of off shelf LLMs | * Not an easy set up * Can add domain specific data * Adapts pre-trained LLMs for specific tasks/datasets * Tailored responses to be domain relevant, boosting production value * Addresses LLM’s limitations in specific task-oriented problems * Cost-effective: leverages advanced models without building from scratch |

**When not to use RAG?**

# Core RAG

RAG workflow consists of 2 stages:

1. Offline mode data preparation done in Indexing pipeline.
2. Strategies/choices to be considered in this phase are:
   1. Chunking strategies
   2. Embedding models selection
   3. **Vector Database Selection & Optimization**
      1. For example, Comparative analysis of Pinecone, Weaviate, Chroma, FAISS, and performance considerations
   4. **Embedding Models & Strategies**
      1. A few are:
         1. dense vs sparse embeddings,
         2. hybrid search approaches,
         3. embedding fine-tuning
   5. **Chunking Strategies & Document Processing** -
      1. A few are:
         1. Semantic chunking,
         2. hierarchical chunking,
         3. overlap strategies, and
         4. metadata preservation
   6. **Retrieval Algorithms**
      1. A few are:
         1. Semantic similarity,
         2. hybrid search (BM25 + vector),
         3. re-ranking mechanisms,
         4. and query expansion
3. Online mode retrieval done in retrieval pipeline
   1. Strategies/choices to be considered in this phase are:
      1. Hybrid Search. Combine keyword search with vector search. This improves accuracy by catching terms that vector search might miss.
      2. Re-ranking. Use a two-stage search. A simple model first fetches many results. A smarter model then re-ranks them for the best relevance.
      3. Query Processing and Transformations. Use an LLM to improve user queries. It can rephrase questions or break complex ones into smaller sub-queries.
      4. Context augmentation & generation
      5. Generation with references

# RAG for the Enterprise

Strategies to be considered for the enterprise

* Cost isolation
* Data isolation
* Multi-tenancy
* TTL
* **Scalability.** Discuss challenges in maintaining low latency as your document count grows.
* **Observability.** Cover how to monitor the system for performance, quality, and cost.
* **Security.** Explain how to enforce document-level access control in the retrieval process. This is crucial for data governance.
* **Data Management**
  + Data Ingestion Pipelines - ETL/ELT processes, real-time vs batch processing, and data validation
  + Data Updates: Describe efficient strategies for adding, removing, or changing documents in the vector index without downtime.
  + Data Governance -
    - Isolation between tenants
    - Version control,
    - lineage tracking, and
    - quality assurance frameworks •
  + Knowledge Base Maintenance - Automated updates, conflict resolution, and content lifecycle management

# Evaluation

* **Component Metrics.** Explain how to measure the parts.
  + **Retriever:** Use metrics like **Hit Rate** and **Mean Reciprocal Rank (MRR)**.
  + **Generator:** Evaluate the final output.
* **End-to-End Metrics.** Focus on the quality of the final answer.
  + **Faithfulness:** Does the answer stick to the retrieved source text?
  + **Answer Relevance:** Does the answer actually address the user's query?
* **Evaluation Tools.** Mention open-source frameworks like RAGAs that help automate these measurements.
* Testing

# Advanced RAG

### **Advanced RAG Patterns & Techniques**

This section explores sophisticated patterns that extend the capabilities of a basic RAG system.

* **Agentic and Autonomous RAG**
  + **Agentic RAG:** An LLM-powered agent dynamically determines if, when, and how to retrieve information, rather than following a fixed pipeline.
  + **Tool-Augmented RAG:** Integrating with external APIs, databases, or other tools to enhance responses.
  + **Self-Reflective RAG:** Designing systems that can critique and improve their own generated responses.
* **Advanced Data & Retrieval Structures**
  + **Hierarchical & Graph RAG:** Using document hierarchy or knowledge graphs for more context-aware retrieval.
  + **Multi-Modal RAG:** Building systems that can retrieve and process information from text, images, and tables.
  + **Conversational RAG:** Managing conversation history to handle follow-up questions effectively.
  + **RAG Fusion:** Combining results from multiple retrieval strategies to produce a better outcome

## **Advanced Topics**

* **RAG Fusion & Ensemble Methods** - Combining multiple retrieval strategies and result merging •
* **Self-Reflective RAG** - Systems that evaluate and improve their own responses
* **Tool-Augmented RAG** - Integration with external APIs, databases, and computational tools •
* **Federated RAG** - Cross-organizational knowledge sharing while maintaining data sovereignty

**References**

1. <https://www.pinecone.io/learn/series/langchain/langchain-retrieval-augmentation/>