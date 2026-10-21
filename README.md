# Class 10 Social Studies RAG Tutor

An AI-assisted study companion for Class 10 Social Studies. The tutor uses retrieval-augmented generation (RAG) to ground answers in the prescribed textbook, helping students explore topics while staying close to the source material.

## What It Does

- Answers study questions using textbook-backed retrieval
- Supports optional chapter and syllabus-period context
- Generates topic-related YouTube and e-resource suggestions
- Exposes a FastAPI backend with a React frontend
- Provides an administrative endpoint for rebuilding the document index

## Architecture

```
React frontend → FastAPI service → local vector index → prescribed textbook
                         └──────→ Ollama language model
```

## Tech Stack

Python · FastAPI · RAG · Ollama · React · Vite

## Run Locally

### Prerequisites

- Python 3.10+
- Node.js 18+
- [Ollama](https://ollama.com/)
- A local copy of the prescribed Social Studies textbook PDF

### Backend

```bash
python -m venv venv
# macOS/Linux
source venv/bin/activate
# Windows
# venv\Scripts\activate

pip install -r backend/requirements.txt
ollama pull llama3
python -m backend.scripts.build_index
uvicorn backend.main:app --reload --host 0.0.0.0 --port 8001
```

Place `Social_textbook_10.pdf` in the project root before building the index.

### Frontend

```bash
cd frontend
npm install
npm run dev
```

The development client proxies API requests to the local backend.

## API

| Endpoint | Purpose |
| --- | --- |
| `GET /health` | Service health check |
| `GET /api/chapters` | Available syllabus chapters |
| `POST /api/chat` | Textbook-grounded answer with sources |
| `POST /api/references` | Topic-related video and web resources |
| `POST /admin/rebuild_index` | Rebuild the textbook index |

## Optional API Keys

Set these environment variables to improve reference retrieval:

```env
YOUTUBE_API_KEY=...
GOOGLE_API_KEY=...
GOOGLE_CSE_ID=...
# or
SERPAPI_KEY=...
```

## Note on Responsible Use

This tool is designed to support learning, not replace teacher guidance or textbook reading. Verify important answers against the prescribed material.

## License

No license has been specified. All rights reserved unless the repository owner states otherwise.
