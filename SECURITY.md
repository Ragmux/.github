# Security policy

Ragmux sits between your users and your provider API keys, so we treat reports seriously and
fix them quickly. Thank you for helping keep it safe.

This is the organization-wide policy. [Ragmux/ragmux](https://github.com/Ragmux/ragmux) ships
its own [SECURITY.md](https://github.com/Ragmux/ragmux/blob/main/SECURITY.md) with the
supported versions, the exact scope and hardening pointers; that file wins for anything about
the gateway itself.

## Reporting a vulnerability

Please do **not** open a public issue or pull request for a security problem.
Use one of:

- **GitHub private vulnerability reporting** —
  <https://github.com/Ragmux/ragmux/security/advisories/new>
- **Email** — <security@ragmux.com>

Include:

- the affected version (`ragmux -version`, or the `version` field of `/healthz`)
- the deployment shape: Docker Compose, bare binary, reverse proxy, managed Postgres
- steps to reproduce, and the impact as you see it

Proof of concept code is welcome. Please keep your testing to systems you own or are
authorised to test, and do not access, modify or retain anyone else's data.

## What to expect

- **Acknowledgement within 3 business days.**
- A fix or a documented mitigation **within 30 days** for high and critical issues; lower
  severities are scheduled into the next release.
- Updates from us while the report is open, and a note when the fix ships.

## Disclosure

We follow coordinated disclosure: the fix is released first, then the advisory is published
with credit to the reporter in the release notes — unless you would rather stay anonymous.
Please give us the response window above before publishing details.

## Out of scope

- Vulnerabilities in third-party providers (OpenAI, Anthropic, Gemini, Ollama, …) or in the
  models themselves.
- Deployments that ignore the documented hardening: the gateway exposed without TLS or a
  reverse proxy, `ALLOW_PRIVATE_UPSTREAMS=true` on an untrusted network, a database role with
  more privileges than documented, secrets committed to a repository.
- Prompt injection inherent to LLMs, beyond the mitigations documented in
  [Retrieval (RAG)](https://github.com/Ragmux/ragmux/blob/main/docs/rag.md).
- Denial of service that requires a valid project API key and stays within the configured
  rate limits and budgets.
- Reports produced solely by an automated scanner, with no demonstrated impact.
