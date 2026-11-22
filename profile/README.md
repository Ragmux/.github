<div align="center">

# Ragmux

**A self-hosted AI gateway. One OpenAI-compatible API in front of every provider, with retrieval built in.**

[![Latest release](https://img.shields.io/github/v/release/Ragmux/ragmux?style=flat-square&color=2f81f7&label=release)](https://github.com/Ragmux/ragmux/releases)
[![CI](https://img.shields.io/github/actions/workflow/status/Ragmux/ragmux/ci.yml?branch=main&style=flat-square&label=CI)](https://github.com/Ragmux/ragmux/actions)
[![Go](https://img.shields.io/github/go-mod/go-version/Ragmux/ragmux?style=flat-square&logo=go&logoColor=white&label=go)](https://github.com/Ragmux/ragmux)
[![License](https://img.shields.io/github/license/Ragmux/ragmux?style=flat-square&color=blue)](https://github.com/Ragmux/ragmux/blob/main/LICENSE)
[![Docker Hub](https://img.shields.io/docker/v/ragmux/ragmux?sort=semver&style=flat-square&logo=docker&logoColor=white&label=docker%20hub)](https://hub.docker.com/r/ragmux/ragmux)

[![Designed & Maintained with Tan](https://muhammetsafak.com/badges/designed-maintained-with-tan.svg)](https://muhammetsafak.com/tan/)

[**Repository**](https://github.com/Ragmux/ragmux) · [**Website**](https://ragmux.com) · [**Documentation**](https://github.com/Ragmux/ragmux#documentation) · [**Wiki**](https://github.com/Ragmux/ragmux/wiki) · [**Releases**](https://github.com/Ragmux/ragmux/releases)

</div>

---

## What Ragmux is

[**Ragmux**](https://github.com/Ragmux/ragmux) is a single-binary AI gateway written in Go.
It sits between your applications and LLM providers, exposes one **OpenAI-compatible API**
(and an Anthropic-compatible one), keeps provider credentials on the server, and can augment
every request with **retrieval (RAG)** from documents you upload.

All state — users, model connections, projects, documents, chunks, vectors and metrics —
lives in one **PostgreSQL** database with the `pgvector` extension. No Redis, no separate
vector database: one all-in-one container, or the gateway against your own PostgreSQL.

```
client  ──►  /v1/chat/completions · /v1/messages · /v1/embeddings · /mcp   (Bearer sk-proj-…)
             │
             ├─ key checks: CIDR / Origin allowlist, rate limits, budgets, end-user limits
             ├─ guardrails: block, redact or flag before the request, retrieval and answer
             ├─ project → RAG store (optional): hybrid search → rerank → inject context
             ├─ project → route: prioritised targets, retry, fallback, circuit breaker
             └─ adapter: OpenAI · Azure OpenAI · Anthropic · Gemini · DeepSeek · Ollama ·
                         any OpenAI-compatible server (vLLM, LM Studio, LiteLLM…)
             │
             └─ PostgreSQL + pgvector: users, encrypted credentials, projects, documents,
                chunks, HNSW vector indexes, request logs, audit log
```

## What it gives you

| | |
|---|---|
| **One API, every provider** | `/v1/chat/completions` (JSON and SSE), `/v1/models`, `/v1/embeddings`, `/v1/rerank`, `/v1/moderations`, plus `/v1/messages` for Anthropic SDKs and Claude Code. Change `base_url` and `api_key` in any official SDK; tool calls and reasoning settings are translated between providers. |
| **Retrieval that ships with the gateway** | PDF / DOCX / HTML / TXT / Markdown, section-aware chunking, hybrid search (pgvector with Postgres full-text or ParadeDB BM25), reranking, metadata filters and sources returned with the answer. |
| **Agents and MCP** | An MCP server at `/mcp` that exposes a project's RAG store as a search tool, per-project tool allow and deny lists, and session tracking to follow and cap an agent's run. |
| **Routing and resilience** | Named routes with prioritised, weighted targets, retries before the first byte and a circuit breaker per connection. |
| **Security controls** | `admin` / `editor` / `viewer` roles, TOTP two-factor login, an audit log, CIDR and `Origin` allowlists per key, guardrails with `/v1/moderations`, and credentials encrypted at rest with the key optionally held in Vault Transit or AWS KMS. |
| **Limits and cost** | Rate limits and token budgets per project and per end user, shared across replicas, signed webhook alerts at 80 % and 100 % of a budget, and an editable price table that estimates the cost of every request. |
| **Feedback, privacy and observability** | `/v1/feedback` scores without content, KVKK anonymisation that keeps usage history, request logs, Prometheus `/metrics`, OpenTelemetry traces and an embedded dashboard at `/admin/`. |

## Try it

Requires Docker. One container runs the gateway with its own PostgreSQL 17 and pgvector:

```bash
docker run -d --name ragmux \
  -p 127.0.0.1:8765:8765 \
  -e SECRET_KEY="$(openssl rand -hex 32)" \
  -v ragmux-data:/data \
  ragmux/ragmux:latest
```

Open <http://localhost:8765/admin/> and create the first administrator. Keep the
`SECRET_KEY` with your backups, and pin a version instead of `latest` in production. Images
are published to Docker Hub as `ragmux/ragmux` and mirrored to `ghcr.io/ragmux/ragmux`; the
gateway-only (`-app`) and ParadeDB (`-paradedb`) variants, Docker Compose and the first call
are in the [repository README](https://github.com/Ragmux/ragmux#readme).

## Getting involved

Issues and pull requests are welcome on [**Ragmux/ragmux**](https://github.com/Ragmux/ragmux).
Start with [CONTRIBUTING.md](https://github.com/Ragmux/.github/blob/main/CONTRIBUTING.md),
and please report security problems privately as described in
[SECURITY.md](https://github.com/Ragmux/.github/blob/main/SECURITY.md) — never in a public issue.

- 🐛 [Report a bug](https://github.com/Ragmux/ragmux/issues/new?template=bug_report.yml)
- 💡 [Request a feature](https://github.com/Ragmux/ragmux/issues/new?template=feature_request.yml)
- 📖 [Read the docs](https://github.com/Ragmux/ragmux#documentation) or the [wiki](https://github.com/Ragmux/ragmux/wiki)
- 📬 <contact@ragmux.com>

## About

Ragmux is a [**Tunedness**](https://tunedness.com) project, built by
[**Muhammet Şafak**](https://muhammetsafak.com/).

It is free software licensed under the **GNU Affero General Public License v3.0 or later**
(AGPL-3.0-or-later). The network-service clause applies: run a modified version as a service
that users reach over a network, and you must offer them the corresponding source.
