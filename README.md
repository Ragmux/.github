# .github

Organization-level defaults for the [**Ragmux**](https://github.com/Ragmux/ragmux) project.

This repository holds two kinds of files:

- **`profile/README.md`** — the page rendered at <https://github.com/Ragmux>.
- **Community health files** — `CODE_OF_CONDUCT.md`, `CONTRIBUTING.md`, `SECURITY.md`,
  `SUPPORT.md`, the issue forms and the pull request template. GitHub falls back to these
  for any repository in the organization that does not ship its own copy, so a policy
  written once here applies everywhere.

Nothing here is code, and nothing here is deployed. Editing a file in this repository
changes what contributors see on the organization page and in the issue and pull request
forms of [Ragmux/ragmux](https://github.com/Ragmux/ragmux).

## Layout

```
profile/README.md              the organization profile page
CODE_OF_CONDUCT.md             Contributor Covenant 2.1
CONTRIBUTING.md                how to build, test and submit changes
SECURITY.md                    how to report a vulnerability privately
SUPPORT.md                     where to ask questions
.github/PULL_REQUEST_TEMPLATE.md
.github/ISSUE_TEMPLATE/bug_report.yml
.github/ISSUE_TEMPLATE/feature_request.yml
.github/ISSUE_TEMPLATE/config.yml
```

A repository that needs different rules simply adds its own file with the same name; the
one closest to the code wins.

## About

Ragmux is a [Tunedness](https://tunedness.com) project, built by
[Muhammet Şafak](https://www.muhammetsafak.com.tr/en/), and is licensed under
AGPL-3.0-or-later. See [LICENSE](LICENSE).
