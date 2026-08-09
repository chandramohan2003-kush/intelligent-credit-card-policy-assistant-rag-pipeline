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

## Architecture

!(image.png)
