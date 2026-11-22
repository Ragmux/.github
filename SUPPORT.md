# Support

Where to go, depending on what you need.

## Documentation first

Most questions are answered in the docs that ship with the gateway:

| Page | Contents |
|---|---|
| [README](https://github.com/Ragmux/ragmux#readme) | features, quick start, which image to choose, Docker Compose, upgrading |
| [Configuration](https://github.com/Ragmux/ragmux/blob/main/docs/configuration.md) | every environment variable and default, flags, subcommands, Compose variables, secret key sources, reverse-proxy and private-upstream notes |
| [API reference](https://github.com/Ragmux/ragmux/blob/main/docs/api.md) | authentication, roles per endpoint, the `/v1` surface including `/v1/messages`, `/v1/moderations` and `/v1/feedback`, the MCP endpoint, guardrails, the error envelope |
| [Retrieval (RAG)](https://github.com/Ragmux/ragmux/blob/main/docs/rag.md) | formats, chunking, hybrid search, metadata filters, reranking, context placement and format |
| [Users, roles and limits](https://github.com/Ragmux/ragmux/blob/main/docs/users-and-limits.md) | roles, login protection, two-factor login, anonymisation, network allowlists, audit log, rate limits, budgets, limit alerts, end users, tool governance |
| [Providers](https://github.com/Ragmux/ragmux/blob/main/docs/providers.md) | provider types and presets, translation details, reasoning effort, routing, retry and fallback |
| [Backup and restore](https://github.com/Ragmux/ragmux/blob/main/docs/backup-restore.md) | what to back up, the scripts, scheduled backups, the restore runbook |
| [Scaling](https://github.com/Ragmux/ragmux/blob/main/docs/scaling.md) | several replicas, shared state, rolling restarts, rolling back |
| [Dashboard](https://github.com/Ragmux/ragmux/blob/main/docs/dashboard.md) | every screen of the embedded dashboard |
| [Observability](https://github.com/Ragmux/ragmux/blob/main/docs/observability.md) | `/metrics`, `/readyz` vs `/healthz`, tracing |
| [Changelog](https://github.com/Ragmux/ragmux/blob/main/CHANGELOG.md) | what changed in each release |
| [Wiki](https://github.com/Ragmux/ragmux/wiki) | the developer guide: local loop, tests, schema contract |

The project website is <https://ragmux.com>.

## Questions and help

Search the [existing issues](https://github.com/Ragmux/ragmux/issues?q=is%3Aissue) first —
deployment and provider questions tend to have been asked before. If nothing matches, write to
<contact@ragmux.com> with your version, the deployment shape and the relevant part of your
configuration with secrets removed.

## Bugs and feature requests

Open an [issue](https://github.com/Ragmux/ragmux/issues/new/choose). The forms ask for the
version, the deployment shape and the steps to reproduce — filling them in properly is the
difference between a fix this week and a week of back-and-forth.

## Security problems

Never in a public issue. Follow [SECURITY.md](SECURITY.md): GitHub private
vulnerability reporting, or an email to `info@muhammetsafak.com` with the subject
`[SECURITY] <repository name>`.

## Anything else

<contact@ragmux.com>.

## What is not supported

There is no SLA, no paid support tier and no guarantee that a given deployment will be
debugged for you. Ragmux is free software maintained by
[Muhammet Şafak](https://muhammetsafak.com/) as a [Tunedness](https://tunedness.com)
project; help is offered as time allows, and a clear, reproducible report gets it fastest.
