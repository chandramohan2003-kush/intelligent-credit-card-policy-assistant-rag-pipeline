# Intelligent Credit Card Policy Assistant

An AI-powered **Retrieval-Augmented Generation (RAG)** system that answers questions from official Credit Card **Most Important Terms & Conditions (MITC)** documents of multiple banks.

The system combines semantic retrieval, **MMR-based retrieval**, **cross-encoder reranking**, and **Gemini-based answer generation** to produce concise, document-grounded responses to credit-card policy questions.

---

## Overview

Credit-card MITC documents are long, policy-heavy documents containing fees, charges, eligibility rules, interest rates, reward policies, payment conditions, and transaction-specific rules.

Finding the correct information manually can be difficult, especially when the same type of information appears across multiple sections or documents.

This project builds a RAG pipeline that:

- Ingests official bank MITC PDFs
- Extracts their content while preserving document structure
- Splits documents into retrieval-friendly chunks
- Generates semantic embeddings
- Retrieves relevant chunks using FAISS + MMR
- Reranks retrieved chunks using a cross-encoder
- Generates answers using Gemini
- Evaluates the RAG system using multiple LLM-based evaluation metrics

---

## Supported Documents

The knowledge base contains MITC documents from eight banks:

- Axis Bank
- City Union Bank
- HDFC Bank
- ICICI Bank
- Kotak Mahindra Bank
- RBL Bank
- SBI Card
- YES BANK

The current knowledge base contains:

| Property | Value |
|---|---:|
| Bank documents | 8 |
| Total pages processed | 402 |
| Generated chunks | 2,559 |
| Embedding dimension | 384 |

---

## 🏗️ RAG Architecture

1. **PDF Document Processing**  
   Official bank MITC PDFs are processed using **PyMuPDF4LLM** for structure-aware text extraction.

2. **Document Chunking**  
   Extracted documents are split into chunks of **600 characters** with **100-character overlap**.

3. **Semantic Embeddings**  
   Each chunk is converted into a **384-dimensional vector** using `all-MiniLM-L6-v2`.

4. **Vector Retrieval**  
   Embeddings are indexed using **FAISS**, followed by **MMR-based retrieval** with `k=6` and `fetch_k=15`.

5. **Cross-Encoder Reranking**  
   Retrieved candidates are reranked using **BGE Reranker Base**, and the **top 4 contexts** are selected.

6. **Answer Generation**  
   The selected contexts are passed to **Gemini 3.1 Flash Lite** for context-grounded answer generation.

7. **Final Response**  
   The system returns the generated answer along with the relevant **source information**.
