# Contributing to Ragmux

Thanks for taking the time. Bug reports, documentation fixes and pull requests are all
welcome on [Ragmux/ragmux](https://github.com/Ragmux/ragmux).

Please **do not** open a public issue for a security problem — follow
[SECURITY.md](SECURITY.md) instead.

## Before you start

- **Bugs:** open an issue with the version (`ragmux -version` or `/healthz`), the deployment
  shape (Docker Compose, bare binary, reverse proxy), the provider involved and the steps to
  reproduce. Logs and the exact error envelope help more than a description of them.
- **Features:** open an issue describing the problem before writing code. Something may be on
  the roadmap, deliberately out of scope, or solvable with existing configuration — a short
  conversation saves you an afternoon.
- **Small fixes** (typos, broken links, an obviously wrong default) need no issue. Send the
  pull request.

## Development setup

You need **Go 1.27+** and Docker for the database.

```bash
git clone https://github.com/Ragmux/ragmux.git && cd ragmux
make dev-db     # pgvector Postgres on localhost:5433 (docker-compose.dev.yml)
make test       # unit + end-to-end tests (mock upstream, real Postgres)
make run        # builds and runs on :8080 against the dev database
```

Tests read `TEST_DATABASE_URL` — the Makefile defaults it to the `make dev-db` instance — and
create a throwaway schema per test, so they run in parallel against one server. They are
**skipped** when the variable is unset, so check that your tests actually ran before claiming
they pass.

The binary is pure Go (`CGO_ENABLED=0`, `pgx`) and ships as a static executable on a
distroless base. Keep it that way: no cgo, no runtime dependency on a shell.

## What CI checks

Your pull request must pass the same gates that run locally:

```bash
gofmt -l .                  # must print nothing
go vet ./...
golangci-lint run ./...     # v2, config in .golangci.yml
govulncheck ./...
make test
```

## House style

- **Match the surrounding code.** Naming, error wrapping, comment density and package layout
  are consistent across the tree; follow what is already there rather than introducing a new
  idiom.
- **Schema changes** are embedded SQL files in `internal/store/migrations/`, applied at startup
  under an advisory lock. Add a new numbered file — never edit one that has shipped — and bump
  the expected schema version in the migration tests.
- **New behaviour comes with tests.** A provider adapter needs a mock-upstream test; a store
  change needs a test against real Postgres.
- **Document what users can see.** A new environment variable, endpoint, header or response
  field belongs in the matching page under `docs/` and in `CHANGELOG.md` under `Unreleased`.
- **Secrets never reach a log line or an API response.** Provider keys are encrypted at rest
  and stay server-side; project keys are shown once at creation.
- **Provider credentials in tests are fake.** Never commit a real key, a real `.env` or a
  database dump.

## Commits and pull requests

- Write commit subjects in the **imperative mood**, describing the change and not the file it
  touched: `Add summary comparison and breakdown options`, not `updated metrics.go`. The
  repository does not use Conventional Commits.
- Keep a pull request to one topic. Two unrelated fixes are two pull requests.
- Rebase on `main` rather than merging it back into your branch.
- Fill in the pull request template: what changed, why, how you tested it, and whether it
  breaks anything for an existing deployment.
- A pull request that changes the API surface, the schema or a default is expected to say so
  explicitly. Silent breaking changes are the one thing that will get a change reverted after
  it lands.

## Licensing

Ragmux is licensed under **AGPL-3.0-or-later**. By contributing you agree that your
contribution is licensed under the same terms. There is no CLA.

## Code of conduct

Participation is governed by the [Code of Conduct](CODE_OF_CONDUCT.md). Reports go to
<contact@ragmux.com>.
