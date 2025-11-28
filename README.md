# DeltaRAG – Lakehouse-Native RAG Pipeline on Databricks

A production-style **ETL + RAG (Retrieval-Augmented Generation)** pipeline built on **Databricks**, **Delta Lake**, and **PySpark**.

This project ingests raw text, cleans and chunks it into a **Bronze → Silver → Gold** medallion architecture, generates **vector embeddings**, and performs **semantic retrieval** to build a RAG prompt that can be sent to any LLM (OpenAI, Azure OpenAI, etc.).

---

## 🔍 What this project demonstrates

- ✅ **Medallion architecture** on Delta Lake  
  - `delta_rag_bronze` – raw text  
  - `delta_rag_silver` – cleaned, normalized text  
  - `delta_rag_gold_chunks` – overlapping chunks for RAG  
  - `delta_rag_gold_embeddings` – vectorized chunks  
- ✅ **PySpark + Delta Lake** for scalable data processing
- ✅ **PyArrow** for efficient in-memory conversions
- ✅ **SentenceTransformers** for dense text embeddings  
- ✅ **Vector search (cosine similarity)** for semantic retrieval
- ✅ **RAG prompt builder** that assembles top-K chunks into a single context block

This is intentionally written as **clean, modular Python**, so it can serve as a portfolio project for a mid-level Data Engineer / Analytics Engineer.

---

## 🧱 Architecture

```mermaid
graph TD
    A[Source Text Documents<br/>Hard-coded / External] --> B[Bronze Layer<br/>delta_rag_bronze]
    B --> C[Silver Layer<br/>delta_rag_silver<br/>clean_text]
    C --> D[Gold Layer – Chunks<br/>delta_rag_gold_chunks<br/>chunk_text]
    D --> E[Embeddings Table<br/>delta_rag_gold_embeddings<br/>vector column]
    F[User Query] --> G[SentenceTransformer<br/>query embedding]
    E --> H[Vector Search<br/>cosine similarity]
    G --> H
    H --> I[Top-K Relevant Chunks]
    I --> J[RAG Prompt Builder<br/>final context prompt]
    J --> K[(LLM of choice<br/>OpenAI / Azure / etc.)]
# DeltaRAG-Lakehouse
