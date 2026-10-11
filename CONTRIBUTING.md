# Contributing to Ragmux

Thank you for your interest in contributing. This guide explains how to propose changes to any repository in the [Ragmux](https://github.com/Ragmux) organization.

## Before You Start

- Small fixes (typos, broken links, obvious bugs) can be sent directly as a pull request.
- For a new feature or a change in behavior, open an issue first so the approach can be discussed before you write code.
- Opening a pull request does not guarantee that it will be accepted.
- Do not report security vulnerabilities in issues or pull requests; follow the [security policy](SECURITY.md).

## Development Setup

Requirements and setup commands differ per repository. For the main project, see [CONTRIBUTING.md in Ragmux/ragmux](https://github.com/Ragmux/ragmux/blob/main/CONTRIBUTING.md).

## Running Tests

The test and lint commands are the same ones CI runs, and they are listed in each repository's own contributing guide. For the main project, see [CONTRIBUTING.md in Ragmux/ragmux](https://github.com/Ragmux/ragmux/blob/main/CONTRIBUTING.md). Run them before opening a pull request.

## Commit Messages

Every repository in this organization follows [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/):

```text
<type>(<scope>)!: <description>

<body>
```

- **Types:** `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`.
- **Scope** is optional, lowercase kebab-case, and names a module or area: `feat(auth): ...`.
- **Description** is in English, imperative mood, starts with a lowercase letter, has no trailing period and is at most 72 characters.
- **Body** is optional and explains why the change was made. Wrap lines at 72 characters.
- Mark a breaking change only with `!` after the type or scope, and describe it in the body.
- Do not add footers or trailers (`BREAKING CHANGE:`, `Refs:`, `Closes #12`, `Co-Authored-By:`, `Signed-off-by:` or any tool attribution). Link issues in the pull request description instead.
- Keep one logical change per commit.

Example:

```text
fix(api): return 404 for unknown project slug
```

## Pull Requests

1. Create a branch from `main` named `<type>/<short-kebab-description>`, for example `feat/token-refresh` or `fix/123-null-slug-404`.
2. Write the pull request title in Conventional Commits format. Pull requests are squash merged, so the title becomes the commit message on `main`.
3. If the change affects users, add an entry under `## [Unreleased]` in the repository's `CHANGELOG.md`.
4. Fill in the pull request template and link the related issue with `Closes #<number>`.
5. Make sure CI passes. A maintainer reviews the pull request and may ask for changes before merging.

By contributing, you agree that your contribution is licensed under the license of the repository you contribute to. There is no CLA.

## Code of Conduct

Every repository in this organization is governed by the [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you agree to uphold it.
