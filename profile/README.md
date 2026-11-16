# Astro — NASA Knowledge Base

A full-stack **Retrieval-Augmented Generation (RAG)** system for querying NASA bioscience research. Built for the **NASA Space Apps 2026 NYC Hackathon**, where it won Best Cloudflair Implementation award for using the entirety of cf stack in its approach to document processing and AI-powered knowledge retrieval.

The project connects a serverless backend (Cloudflare Workers) that ingests PDFs and runs semantic search with a space-themed React frontend where users can chat with an AI that answers from those documents.

<p align="center">
  <img src="IMG_7611.jpg" alt="Astro at NASA Space Apps 2025" width="45%" />
  <img src="Space Apps 2025 Cloudflare Winners.jpg" alt="Space Apps 2025 Cloudflare Winners" width="45%" />
</p>

---

## What This Repository Includes

| Component | Description |
|-----------|-------------|
| **Backend (cf_ai_astro-rag)** | Cloudflare Workers API that fetches PDFs, extracts text/images/tables, generates embeddings, and serves RAG queries using vector search. |
| **Frontend (Astro)** | React + Vite app with an animated landing page and chat interface for talking to the RAG system. |

---

## The Story

### What It Is

Astro is a document-to-query system: you ingest PDFs (e.g. NASA reports or research papers), and the system turns them into a searchable knowledge base. Users ask questions in natural language and get answers grounded in those documents, with source citations and optional web search for broader context.

### Why It Was Built

The project was created for the **NASA NYC Hackathon** with two goals:

1. **Document intelligence** — Turn dense PDFs (text, tables, images) into structured, searchable content using AI.
2. **Accessible research** — Let anyone query NASA bioscience research without manually reading long documents.

The result is a cloud-native RAG stack (Cloudflare D1, Vectorize, Workers, and Google Gemini) that is scalable and runs at the edge.

### How It Works

1. **Ingestion**: PDF URLs are sent to the backend. Text is extracted, tables and images are processed, and content is chunked and embedded.
2. **Storage**: Chunks go into Cloudflare D1; embeddings go into Vectorize.
3. **Query**: User questions are embedded, matched to chunks via vector search, and answered by Gemini with source attribution.
4. **Interface**: The frontend provides a chat UI with voice input, hybrid search mode, and relevance indicators for sources.

---

## Directory Structure

```
cf/
├── README.md                    # This file — project overview and navigation
│
├── cf_ai_astro-rag/             # Backend: RAG API (Cloudflare Workers)
│   ├── src/
│   │   └── index.js             # Worker entry point, routing, ingest/query handlers
│   ├── queryHandling.js         # RAG query logic (embedding, vector search, response)
│   ├── queryHandling.py         # Python reference implementation
│   ├── test/
│   │   └── index.spec.js        # Test suite
│   ├── wrangler.jsonc           # Cloudflare Workers config (D1, Vectorize, env)
│   └── package.json             # Dependencies (pnpm)
│
└── Astro/                       # Frontend: chat UI
    ├── README.md                # Frontend setup and config
    └── astro-nasa-chat/         # React + Vite app
        ├── src/
        │   ├── App.jsx          # Main app, chat UI, API integration
        │   ├── main.jsx         # Entry point
        │   └── index.css        # Tailwind styles
        ├── index.html
        ├── package.json         # Dependencies (npm)
        └── vite.config.js       # Vite configuration
```

### Quick Navigation

| If you want to… | Go to |
|-----------------|-------|
| Understand the RAG pipeline, ingestion, and API | [`cf_ai_astro-rag/README.md`](./cf_ai_astro-rag/README.md) |
| Run the backend locally or deploy it | [`cf_ai_astro-rag/`](./cf_ai_astro-rag/) |
| Understand the frontend features and config | [`Astro/README.md`](./Astro/README.md) |
| Run the chat UI locally | [`Astro/astro-nasa-chat/`](./Astro/astro-nasa-chat/) |

---

## Getting Started

### Backend

```bash
cd cf_ai_astro-rag
pnpm install
pnpm run dev          # Local development
npx wrangler deploy   # Deploy to Cloudflare
```

See [`cf_ai_astro-rag/README.md`](./cf_ai_astro-rag/README.md) for D1, Vectorize, and env setup.

### Frontend

```bash
cd Astro/astro-nasa-chat
npm install
npm start
```

Open [http://localhost:3000](http://localhost:3000). Configure the API endpoint in `App.jsx` to point at your deployed backend.

---

## Tech Stack Summary

| Layer | Technologies |
|-------|--------------|
| **Backend** | Cloudflare Workers, D1, Vectorize, Google Gemini (2.5 Pro, 1.5 Flash, Embeddings 004) |
| **Frontend** | React, Vite, Tailwind CSS, Lucide Icons |
| **APIs** | Google AI, Google Custom Search (optional hybrid mode) |

---

## Achievement

**Winner of the NASA NYC Hackathon** — Recognized for combining document processing, vector search, and AI chat into an accessible research tool.

---

## License

MIT — see the LICENSE file in the repository.
