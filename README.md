#  ARIELA AI

> A Retrieval-Augmented Generation (RAG) service for evidence-based women's health Q&A.

Custom medical-grade AI backend powering the [ARIELA](https://github.com/Sharonne-ariel/ariela-mobile-app) mobile application.

[![Python](https://img.shields.io/badge/Python-3.11-3776AB?logo=python)](https://www.python.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.111-009688?logo=fastapi)](https://fastapi.tiangolo.com)
[![ChromaDB](https://img.shields.io/badge/ChromaDB-0.5-FF6B6B)](https://www.trychroma.com)
[![HF Spaces](https://img.shields.io/badge/🤗-Spaces-yellow)](https://huggingface.co/spaces/Shariel/ariela-ai)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 🚀 Live API

The service is publicly deployed and available at:

**`https://shariel-ariela-ai.hf.space`**

Try it from your terminal:
```bash
curl -X POST https://shariel-ariela-ai.hf.space/ask \
  -H "Content-Type: application/json" \
  -d '{"question":"Why am I tired before my period?","top_k":3}'
```

---

## 🎯 What it does

ARIELA AI answers women's health questions by retrieving the most semantically relevant entries from a curated dataset of 235 expert-validated Q/A pairs and returning them with their original medical sources.

The system was designed to **avoid the hallucination risks of free-form language models** in clinical contexts: every answer is grounded on text sourced from authoritative medical institutions, and every response cites its source.

---

## 📊 Evaluation results

Benchmarked on a held-out golden set of 20 reformulated test questions:

| Metric | Score |
|---|---|
| **Top-1 accuracy** | **65%** |
| **Top-3 accuracy** | **90%** |
| Mean top-1 similarity | 0.642 |
| Crisis question (mental health) | ✅ Top-1 retrieved |

The mental-health crisis question ("I'm having dark thoughts and don't know what to do") was correctly retrieved at rank 1, demonstrating the system's ability to surface crisis support resources even when the user uses indirect, non-clinical language.

---

## 🏗 Architecture

ariela-ai/
├── data/
│   ├── dataset/              # 5 JSON files = 235 Q/A
│   │   ├── 01_menstrual_cycle.json
│   │   ├── 02_first_period.json
│   │   ├── 03_fertility.json
│   │   ├── 04_pregnancy.json
│   │   └── 05_mental_health.json
│   └── golden_set/
│       └── eval_questions.json   # 20 held-out test questions
├── deploy/
│   ├── app.py                # FastAPI service
│   ├── Dockerfile            # Container definition
│   ├── requirements.txt      # Python dependencies
│   └── README.md             # HF Spaces metadata
├── notebooks/
│   └── rag_pipeline.ipynb    # Embedding + ChromaDB + evaluation
└── README.md
---

## 🚀 Local development

### Prerequisites
- Python 3.11+
- pip

### Setup
```bash
git clone https://github.com/Sharonne-ariel/ariela-ai.git
cd ariela-ai/deploy
pip install -r requirements.txt
```

### Run locally
```bash
uvicorn app:app --reload --port 7860
```

The API is now available at `http://localhost:7860`.

### Test
```bash
curl http://localhost:7860/
curl -X POST http://localhost:7860/ask \
  -H "Content-Type: application/json" \
  -d '{"question":"What is PMS?","top_k":3}'
```

---

## ⚠️ Medical Disclaimer

ARIELA AI is **not a medical device** and does not provide medical diagnosis or treatment. The retrieved content is for general informational purposes only and always recommends consulting a qualified healthcare professional. For mental health emergencies, the system surfaces crisis hotlines, but it is not a substitute for professional crisis intervention.

---

## 🗺 Future Work

- Minimum similarity threshold filter to handle out-of-scope follow-up questions
- Fine-tuning a domain-specific embedding model on the medical dataset
- Conversation context awareness (currently each /ask call is stateless)
- Expansion to additional languages (Spanish, Arabic, Portuguese)
- Continuous evaluation pipeline with monthly golden set refresh

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.

---

## 👤 Author

**Sharonne Kabamba Muadi** 
Software Engineering student 
Final-year project, Spring 2026

Built as part of the İME workplace application training course under the supervision of PR.Ersin Aslan.
