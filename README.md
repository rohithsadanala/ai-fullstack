# ai-fullstack

> A full-stack, self-hosted AI chat application — a learning copy / experiment based on Open WebUI (v0.6.36).

## Attribution — please read first

**This is not original work by Rohith Sadanala, and Open WebUI is not claimed as his work.**

The code in this repository is a copy of [Open WebUI](https://github.com/open-webui/open-webui) (version 0.6.36, as of November 6, 2025), an open-source project created by Timothy Jaeryang Baek and the Open WebUI contributors. It is kept here as a full-stack AI app starter and learning experiment, to study and run a production-style AI chat application locally.

For the official project, documentation, and support, see:

- Upstream repository: https://github.com/open-webui/open-webui
- Documentation: https://docs.openwebui.com/

No original features of Open WebUI are claimed here. See `LICENSE`, `LICENSE_HISTORY`, and `LICENSE_NOTICE` in this repository for the upstream licensing terms.

## What it does

A self-hosted web interface for chatting with large language models, running entirely on your own machine or server:

- Chat with local models through [Ollama](https://ollama.com/), or with OpenAI-compatible APIs
- Local retrieval-augmented generation (RAG) over your own documents
- Multiple models in one conversation, model / prompt building, and image generation integrations
- User accounts, roles, and permissions, with a responsive web UI and mobile PWA support

These features come from the upstream Open WebUI codebase; this copy adds no new application features.

## Tech stack

- **Frontend:** SvelteKit / Svelte, TypeScript, Vite, Tailwind CSS — see `package.json` (package name `open-webui`, version `0.6.36`)
- **Backend:** Python, FastAPI, Uvicorn, Pydantic, SQLAlchemy / Alembic, python-socketio — see `pyproject.toml` (project name `open-webui`)
- **AI runtime:** Ollama for local models, plus OpenAI-compatible API endpoints
- **Infrastructure:** Docker and Docker Compose, with Kubernetes manifests in `kubernetes/`

## How to run

### With Docker Compose (recommended)

```bash
docker compose up -d
```

This starts two services, as defined in `docker-compose.yaml`:

- `ollama` — the local model runner
- `open-webui` — the web app, on port `3000` by default (`${OPEN_WEBUI_PORT:-3000}:8080`), with `OLLAMA_BASE_URL=http://ollama:11434`

Then open http://localhost:3000 and create an admin account on first launch.

To pull a model into Ollama, for example:

```bash
docker exec -it ollama ollama pull llama3.1
```

### Local development

```bash
npm install
npm run dev
```

See `INSTALLATION.md` and the upstream documentation at https://docs.openwebui.com/ for the full local setup, including the Python backend.

## Project structure

```text
.
├── backend/            # Python FastAPI backend (API, auth, RAG, models, database)
├── src/                # SvelteKit frontend (routes, components, stores)
├── static/             # Static frontend assets
├── cypress/            # End-to-end tests
├── docs/               # Documentation
├── kubernetes/         # Kubernetes deployment manifests
├── scripts/            # Helper scripts (including Pyodide setup)
├── docker-compose.yaml # Ollama + Open WebUI services
├── Dockerfile          # Application image
├── package.json        # Frontend dependencies and scripts
└── pyproject.toml      # Backend dependencies
```

## Status

This repository is a snapshot / experiment, not an actively developed fork. Upstream fixes and features should be taken from the official Open WebUI project, not from here.
