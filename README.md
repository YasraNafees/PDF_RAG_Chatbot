# 📚 PDF RAG Chatbot

![Python](https://img.shields.io/badge/Python-3.10+-blue) ![LangChain](https://img.shields.io/badge/LangChain-Enabled-green) ![FAISS](https://img.shields.io/badge/FAISS-VectorStore-blue) ![DeepSeek](https://img.shields.io/badge/DeepSeek-v3.1-red) ![License](https://img.shields.io/badge/License-MIT-yellow)

### SHA256 Fingerprinting | Smart Index Caching | Streaming Responses

A RAG-powered chatbot that lets you have intelligent conversations with any PDF document. Built with smart index caching via SHA256 fingerprinting — if the same PDF is loaded again, it skips re-indexing entirely and loads instantly.

---

## 🎬 Demo

[![Watch Demo](https://img.youtube.com/vi/yg0Zn1DVod8/maxresdefault.jpg)](https://youtu.be/yg0Zn1DVod8)

> Click the thumbnail to watch the full demo on YouTube.

---

## ✨ Key Features

- **SHA256 Index Fingerprinting:** Generates a unique hash per PDF based on content, chunk size, overlap, and embedding model — identical documents are never re-indexed.
- **Smart Cache System:** FAISS index persists locally under `.indices/` — instant load on repeated use.
- **Zero Hallucination:** Strict system prompt ensures answers come only from PDF context — never fabricated.
- **Streaming Responses:** Real-time token-by-token output via LangChain streaming callbacks.
- **Modular Pipeline:** Clean separation of backend (RAG pipeline) and frontend (Streamlit UI).
- **Chat History:** Full conversation memory within session via Streamlit state management.

---

## 🛠️ Tech Stack & Design Decisions

| Component | Tool | Why |
|---|---|---|
| Orchestration | LangChain | Modular RAG pipeline with RunnableParallel |
| LLM | DeepSeek v3.1 via OpenRouter | Free tier, high-quality reasoning |
| Embeddings | all-MiniLM-L6-v2 | Lightweight, high semantic accuracy |
| Vector Store | FAISS | Fast local retrieval, no cloud dependency |
| PDF Loader | PyMuPDF | Reliable text extraction from complex PDFs |
| UI | Streamlit | Lightweight chat interface with streaming support |

---

## 🏗️ Architecture Flow
```
PDF Document
      ↓
SHA256 Fingerprint Check
      ↓
Cache Hit? → Load FAISS Index Instantly
Cache Miss? → PyMuPDF Loader → Text Splitter (1000 chars, 200 overlap)
      ↓
HuggingFace Embeddings (all-MiniLM-L6-v2)
      ↓
FAISS Vector Store (Persisted locally)
      ↓
User Query → Top-4 Similarity Retrieval
      ↓
DeepSeek v3.1 → Streaming Answer
      ↓
Streamlit Chat UI
```

---

## 🚀 Quick Start

**1. Clone the repo:**
```bash
git clone https://github.com/YasraNafees/PDF-RAG-Chatbot.git
cd PDF-RAG-Chatbot
```

**2. Install dependencies:**
```bash
pip install -r requirements.txt
```

**3. Set environment variables:**

Create a `.env` file:
```
OPENROUTER_API_KEY=your_key_here
OPENROUTER_API_BASE=https://openrouter.ai/api/v1
```

**4. Add your PDF:**

Place your PDF in the root directory and update `PDF_PATH` in `backend.py`:
```python
PDF_PATH = "your_document.pdf"
```

**5. Run the app:**
```bash
streamlit run app.py
```

---

## 🤝 Contributing

Pull requests are welcome. For major changes, please open an issue first.
