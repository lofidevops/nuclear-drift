# Security Policy

Nuclear Drift is an OSTree container image that users rebase their host
onto, so the integrity of published images matters.

## Reporting a Vulnerability

Please report security issues privately rather than as a public issue.

Use [GitHub Security Advisories](https://github.com/lofidevops/nuclear-drift/security/advisories/new)
("Report a vulnerability") to disclose responsibly. You can also email the
maintainers listed in `.github/CODEOWNERS`.

Include:

- A description of the issue and its impact.
- Steps to reproduce (build config, image tag, commands run).
- The affected image digest (`skopeo inspect docker://ghcr.io/lofidevops/nuclear-drift:latest`)
  if applicable.

We will acknowledge reports within a reasonable timeframe and coordinate a
fix and disclosure.

## Image Signing

Image signing is not yet enabled. Builds currently use `--no-sign`, and
`cosign.pub` is staged in the repository for future use. Once signing is
enabled, users should verify the image signature with the published public
key before rebasing.
