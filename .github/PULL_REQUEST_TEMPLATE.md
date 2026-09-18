## What this changes

<!-- One paragraph: the behaviour before, and after. -->

## Why

<!-- The problem being solved. Link the issue: "Fixes #123" or "Part of #123". -->

## How it was tested

<!--
The commands you ran and what they covered. Remember that the Go tests are SKIPPED when
TEST_DATABASE_URL is unset — make sure they actually ran.
-->

```
make test
```

## Impact on existing deployments

<!-- Delete the lines that do not apply. -->

- [ ] No impact: behaviour is unchanged for anyone upgrading.
- [ ] Adds a migration in `internal/store/migrations/` (new numbered file, schema version bumped in the tests).
- [ ] Adds or changes an environment variable or default.
- [ ] Changes the `/v1` or `/admin/api` surface (endpoint, field, header, error code).
- [ ] **Breaking change** — described below, with the upgrade path.

## Checklist

- [ ] `gofmt -l .` prints nothing, `go vet ./...` and `golangci-lint run ./...` are clean.
- [ ] `make test` passes against a real Postgres.
- [ ] New behaviour is covered by tests.
- [ ] User-visible changes are documented under `docs/` and added to `CHANGELOG.md` under `Unreleased`.
- [ ] No secrets, real provider keys, `.env` files or database dumps are included.
- [ ] I agree to license this contribution under AGPL-3.0-or-later.

## Anything reviewers should know

<!-- Trade-offs you made, things you deliberately left out, parts you are unsure about. -->
