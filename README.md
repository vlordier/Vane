# Vane 🔍

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Docker Pulls](https://img.shields.io/docker/pulls/itzcrazykns1337/vane?color=blue)](https://hub.docker.com/r/itzcrazykns1337/vane)
[![Discord](https://dcbadge.limes.pink/api/server/26aArMy8tT?style=flat)](https://discord.gg/26aArMy8tT)

Vane is a **privacy-focused AI answering engine** that runs entirely on your own hardware. It combines internet knowledge with support for **local LLMs** (Ollama) and cloud providers (OpenAI, Claude, Gemini, Groq), delivering accurate answers with **cited sources** while keeping your searches private.

![preview](.assets/vane-screenshot.png)

## ⚡ Key Features

- **Multi-provider LLMs** — Use local (Ollama) or cloud (OpenAI, Claude, Gemini, Groq) models, or mix them
- **Private web search** — Powered by SearxNG, no identity leakage
- **Smart search modes** — Speed, Balanced, and Quality modes for different use cases
- **Rich widgets** — Weather, stock prices, calculations, and more
- **File uploads** — PDFs, text files, images — ask questions about your documents

## 🏗 Architecture

```mermaid
graph TB
    subgraph client["Client"]
        UI[Next.js Web UI<br/>React + Tailwind]
    end

    subgraph backend["Vane Backend"]
        API[API Routes<br/>Next.js]
        CHAT[Chat Controller]
        SRC[Search Router]
        WIDGET[Widget Engine]
        DB[(SQLite Drizzle)]
        UPLOAD[File Processor]
    end

    subgraph search["Search"]
        SEARXNG[SearxNG Instance]
        TAVILY[Tavily API]
        EXA[Exa API]
    end

    subgraph llm["LLM Providers"]
        OLLAMA[Ollama<br/>Local]
        OPENAI[OpenAI]
        ANTHROPIC[Anthropic]
        GOOGLE[Google Gemini]
        GROQ[Groq]
    end

    UI --> API
    API --> CHAT
    CHAT --> SRC
    CHAT --> WIDGET
    CHAT --> UPLOAD
    SRC --> SEARXNG
    SRC --> TAVILY
    SRC --> EXA
    CHAT --> OLLAMA
    CHAT --> OPENAI
    CHAT --> ANTHROPIC
    CHAT --> GOOGLE
    CHAT --> GROQ
    CHAT --> DB

    classDef client fill:#e3f2fd,stroke:#1976d2,color:#000
    classDef backend fill:#fff3e0,stroke:#f57c00,color:#000
    classDef search fill:#e8f5e9,stroke:#388e3c,color:#000
    classDef llm fill:#f3e5f5,stroke:#7b1fa2,color:#000

    class UI client
    class API,CHAT,SRC,WIDGET,DB,UPLOAD backend
    class SEARXNG,TAVILY,EXA search
    class OLLAMA,OPENAI,ANTHROPIC,GOOGLE,GROQ llm
```

## 📦 Installation

### Docker (Recommended)

```bash
docker run -d -p 3000:3000 -v vane-data:/home/vane/data --name vane itzcrazykns1337/vane:latest
```

With your own SearxNG instance:

```bash
docker run -d -p 3000:3000 -e SEARXNG_API_URL=http://your-searxng:8080 -v vane-data:/home/vane/data --name vane itzcrazykns1337/vane:slim-latest
```

### From Source

```bash
git clone https://github.com/ItzCrazyKns/Vane.git
cd Vane
npm i && npm run build && npm run start
```

> Full docs: [installation](docs/installation), [architecture](docs/architecture/README.md), [API](docs/API/SEARCH.md)

## 🔧 Development

```bash
npm run dev     # Start development server
npm run build   # Production build
npm run lint    # ESLint check
```

## 🌐 Deployment

One-click deployment options available for Sealos, RepoCloud, ClawCloud, and Hostinger. See [docker-compose.yaml](docker-compose.yaml) for self-hosted Docker setup.

## 📚 Citation & Attribution

This project has received funding from the European Union's Horizon Europe research programme (grant No. 101070238).

## 🤝 Contributing

Found a bug or have an idea? Open a [GitHub issue](https://github.com/ItzCrazyKns/Vane/issues) or join our [Discord](https://discord.gg/EFwsmQDgAu). See [CONTRIBUTING.md](CONTRIBUTING.md) for contribution guidelines.
