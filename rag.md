RAG

[**LLM Basics 1**](#_ygik01au7yhb)

[Controlling Randomness and Diversity 1](#_1kk9hile49i9)

[Prompt + Parameters 1](#_9zc8yt2533r2)

[Hallucination 2](#_yl56zecdjnbe)

[Reducing Hallucination 2](#_ufgdv64c2zfz)

[**Core RAG 4**](#_16h5usvsme49)

[**RAG for the Enterprise 4**](#_5xapw8duatkh)

[**Evaluation 5**](#_14mgvajetplq)

[**Advanced RAG 5**](#_x0sjjsqrm4g)

[Advanced RAG Patterns & Techniques 5](#_h1q175kuqaf0)

[3. Explaining Agentic RAG 6](#_tghazptsgflw)

[Advanced Topics 6](#_bu6qpth5sjrg)

#

# LLM Basics

## Controlling Randomness and Diversity

Three Key Parameters​

1. Temperature​
   1. Controls probability distribution of word selection​
   2. Low (→0): Selects high-probability words → deterministic responses​
   3. High: Allows lower-probability words → creative/random responses​
2. Top K​
   1. Limits selection to K most probable next words​
   2. Example: K=50 means choose from top 50 candidate words​
   3. Prevents selection of highly unusual words
3. Top P​
   1. Caps word choices based on cumulative probability threshold​
   2. P<1.0 focuses on most probable options, ignoring unlikely ones​
   3. Alternative to Top K that uses probability sum instead of word count​
4. Example: "I hear the hoof beats of..."​
   1. High temp + no limits: May get "unicorns" (creative but unusual)​
   2. Temp = 0: Likely gets "horses" (most probable)​
   3. High temp + Top K/P limits: Gets "horses" or "zebras" (balanced creativity)

## Prompt + Parameters

| **Example use case**​ | **Temperature**​ | **top\_p**​ | **Description**​ |
| --- | --- | --- | --- |
| Brainstorming session​ | High​ | High​ | High randomness with large pool of potential tokens. The results will be highly diverse, often leading to very creative and unexpected results.​ |
| Email generation​ | Low​ | Low​ | Deterministic output with high probable predicted tokens. This results in predictable, focused, and conservative outputs.​ |
| Creative writing​ | High​ | Low​ | High randomness with a small pool of potential tokens. This combination produces creative outputs but still remains coherent.​ |
| Translation​ | Low​ | High​ | Deterministic output with high probable predicted tokens. Produces coherent output with a wider range of vocabulary, leading to outputs with linguistic variety. |

## Hallucination

An LLM hallucination occurs when a large language model (LLM) generates a​

response that is either​:

* factually incorrect,​
* Nonsensical​
* or disconnected from the input prompt.​

Hallucinations are a byproduct of the probabilistic nature of language models which generates responses based on patterns learned from vast datasets​ rather than factual understanding.

### Reducing Hallucination

1. Data Quality is King​

* Clean, Diverse, & Relevant Data: Train on high-quality, balanced, and domain-specific datasets.​
* Regular Updates: Keep training and grounding data current.​

2. Grounding with RAG​

* Retrieval-Augmented Generation (RAG): Anchor AI responses to external, authoritative knowledge bases.​
* Prepare Grounding Data: Organize and curate your enterprise data for accurate retrieval.​

3. Model & Prompt Engineering​

* Advanced Models: Leverage larger, more sophisticated models.​
* Self-Correction: Implement mechanisms for the AI to verify its own outputs.​
* Clear Prompts: Give explicit, contextual, and example-driven instructions.​
* Lower Temperature: Reduce model creativity for factual accuracy.​

4. Human Oversight & Testing​

* Fact-Checking: Validate AI outputs, especially for critical use cases.​
* Continuous Monitoring: Regularly test and refine models based on real-world performance.

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