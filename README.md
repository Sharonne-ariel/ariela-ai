# ARIELA AI Assistant

> Retrieval-Augmented Generation (RAG) system for women's health Q&A, designed to provide reliable, sourced, and personalized answers without the hallucination risks of standalone LLMs.

## Overview

ARIELA AI is the conversational AI layer of the ARIELA women's health mobile app. Rather than relying solely on a generative language model — which can hallucinate dangerous medical advice — this system uses **Retrieval-Augmented Generation (RAG)** over a curated dataset of expert-validated Q&A pairs sourced from authoritative medical institutions (Mayo Clinic, WHO, ACOG, NHS, NIH, Planned Parenthood, Cleveland Clinic).

## Key features

- 🔎 **Semantic retrieval** over a curated dataset of 220 expert-validated Q&A pairs
- 🧠 **Hybrid architecture** combining retrieval and (optional) generation
- 🌍 **Multilingual-ready** (English first, French planned)
- 🩺 **5 medical categories** : Menstrual Cycle, First Period, Fertility, Pregnancy, Mental Health
- 🔒 **No hallucinations** : answers grounded in verified sources
- 📊 **Evaluation** on a held-out golden set with precision@k metrics

## Tech stack

| Component | Technology |
|---|---|
| Embeddings | `sentence-transformers/all-MiniLM-L6-v2` |
| Vector store | ChromaDB |
| Backend | FastAPI |
| Deployment | Hugging Face Spaces |
| Evaluation | scikit-learn, custom metrics |

## Project structure