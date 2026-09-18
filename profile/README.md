<div align="center">

# Ragmux

**A self-hosted AI gateway. One OpenAI-compatible API in front of every provider, with retrieval built in.**

[![Latest release](https://img.shields.io/github/v/release/Ragmux/ragmux?style=flat-square&color=2f81f7&label=release)](https://github.com/Ragmux/ragmux/releases)
[![CI](https://img.shields.io/github/actions/workflow/status/Ragmux/ragmux/ci.yml?branch=main&style=flat-square&label=CI)](https://github.com/Ragmux/ragmux/actions)
[![Go](https://img.shields.io/github/go-mod/go-version/Ragmux/ragmux?style=flat-square&logo=go&logoColor=white&label=go)](https://github.com/Ragmux/ragmux)
[![License](https://img.shields.io/github/license/Ragmux/ragmux?style=flat-square&color=blue)](https://github.com/Ragmux/ragmux/blob/main/LICENSE)
[![Container](https://img.shields.io/badge/ghcr.io-ragmux%2Fragmux-1f6feb?style=flat-square&logo=docker&logoColor=white)](https://github.com/Ragmux/ragmux/pkgs/container/ragmux)

[**Repository**](https://github.com/Ragmux/ragmux) · [**Website**](https://ragmux.com) · [**Documentation**](https://github.com/Ragmux/ragmux#documentation) · [**Releases**](https://github.com/Ragmux/ragmux/releases)

</div>

---

## What Ragmux is

[**Ragmux**](https://github.com/Ragmux/ragmux) is a single-binary AI gateway written in Go.
It sits between your applications and LLM providers, exposes one **OpenAI-compatible API**,
and can augment every request with **retrieval (RAG)** from documents you upload.

All state — users, model connections, projects, documents, chunks, vectors and metrics —
lives in one **PostgreSQL** database with the `pgvector` extension. Two containers, no Redis,
no separate vector database.

```
client  ──►  POST /v1/chat/completions (Bearer sk-proj-…)
             │
             ├─ project → model connection (provider credentials stay server-side)
             ├─ project → RAG store (optional): embed query → top-k chunks → inject context
             └─ adapter: OpenAI · Anthropic · Gemini · DeepSeek · Ollama · custom OpenAI (vLLM…)
                          JSON and SSE streaming, normalised to the OpenAI schema
             │
             └─ PostgreSQL + pgvector: users, connections (AES-256-GCM keys), projects,
                documents (bytea), chunks, HNSW vector indexes, request logs
```

## What it gives you

| | |
|---|---|
| **One API, every provider** | `/v1/chat/completions` and `/v1/models`, JSON and SSE streaming. Point any OpenAI SDK at it by changing `base_url` and `api_key`. Anthropic and Gemini requests and streams are translated for you. |
| **Retrieval that ships with the gateway** | PDF / DOCX / HTML / TXT / Markdown, section-aware chunking with contextual embeddings, hybrid vector + full-text search (RRF), optional LLM reranking. |
| **Keys that never leave the server** | One `sk-proj-…` key per project, mapped to a model connection, a system prompt and an optional RAG store. Provider credentials are encrypted at rest with AES-256-GCM. |
| **Users, roles and an audit trail** | `admin` / `editor` / `viewer`, project membership, login rate limiting with lockout, and an audit log of every management action. |
| **Rate limits and budgets** | Per-project requests and tokens per minute, daily and monthly token budgets shared across replicas, OpenAI-style `429` and `x-ratelimit-*` headers. |
| **Metrics and a dashboard** | Per-request logs (tokens, latency, status, streaming, RAG use), summaries, daily series, CSV export — behind an embedded UI at `/admin/` and a REST API. |

## Try it

```bash
git clone https://github.com/Ragmux/ragmux.git && cd ragmux
cp .env.example .env
echo "SECRET_KEY=$(openssl rand -hex 32)" >> .env
echo "POSTGRES_PASSWORD=$(openssl rand -hex 16)" >> .env
echo "RAGMUX_DB_PASSWORD=$(openssl rand -hex 16)" >> .env
docker compose up -d
```

Open <http://localhost:8080/admin/> and create the first administrator. Prebuilt images are
published as `ghcr.io/ragmux/ragmux`. The full walkthrough — connections, RAG stores, projects
and the first call — is in the [repository README](https://github.com/Ragmux/ragmux#readme).

## Getting involved

Issues and pull requests are welcome on [**Ragmux/ragmux**](https://github.com/Ragmux/ragmux).
Start with [CONTRIBUTING.md](https://github.com/Ragmux/.github/blob/main/CONTRIBUTING.md),
and please report security problems privately as described in
[SECURITY.md](https://github.com/Ragmux/.github/blob/main/SECURITY.md) — never in a public issue.

- 🐛 [Report a bug](https://github.com/Ragmux/ragmux/issues/new?template=bug_report.yml)
- 💡 [Request a feature](https://github.com/Ragmux/ragmux/issues/new?template=feature_request.yml)
- 📖 [Read the docs](https://github.com/Ragmux/ragmux#documentation)
- 📬 <contact@ragmux.com>

## About

Ragmux is a [**Tunedness**](https://tunedness.com) project, built by
[**Muhammet Şafak**](https://www.muhammetsafak.com.tr/en/).

It is free software licensed under the **GNU Affero General Public License v3.0 or later**
(AGPL-3.0-or-later). The network-service clause applies: run a modified version as a service
that users reach over a network, and you must offer them the corresponding source.
