# Security Policy

This is the organization-wide default policy. A repository that ships its own `SECURITY.md` follows that file instead; for example, [Ragmux/ragmux](https://github.com/Ragmux/ragmux/blob/main/SECURITY.md) documents the gateway itself.

## Supported Versions

Only the latest minor version of each project receives security fixes. While a project is at `0.y.z`, only its latest release is supported.

| Version | Supported |
|---|---|
| Latest release | Yes |
| Older versions | No |

## Reporting a Vulnerability

Do not report security vulnerabilities through public issues, pull requests or discussions.

Report vulnerabilities privately through GitHub Private Vulnerability Reporting on the affected repository: open the repository's `security/advisories/new` page, for example [Ragmux/ragmux](https://github.com/Ragmux/ragmux/security/advisories/new).

If you cannot use GitHub, send an email to `info@muhammetsafak.com` with the subject line `[SECURITY] <repository name>`.

Please include:

- the affected version or versions,
- steps to reproduce the issue,
- the impact of the vulnerability,
- a suggested fix, if you have one.

Please keep your testing to systems you own or are authorized to test, and do not access, modify or retain anyone else's data.

## Response Process

- You will receive a response within 7 days of your report.
- The report is assessed and you are informed of the result.
- After a fix is released, a GitHub Security Advisory is published.
- If you wish, you are credited for the report in the advisory.

## Scope

The following are out of scope for this policy:

- Vulnerabilities in third-party dependencies (report them to their maintainers)
- Vulnerabilities in third-party providers or in the models themselves
- Reports produced solely by an automated scanner, with no demonstrated impact
