# Secret management policy

This repository contains public templates and organization documentation. It
must not contain credentials, tokens, private configuration, or incident
details.

## Storage and access

- Templates default to empty workflow permissions and never request secrets by
  default. Caller repositories are responsible for granting only the
  documented job permissions.
- Organization or repository credentials are stored only in GitHub's protected
  secret or environment facilities. Short-lived OIDC credentials are preferred
  over long-lived keys.
- Pull-request and template validation jobs do not check out or execute
  untrusted code in privileged contexts, and workflows must not print secret
  values or place them in artifacts.

## Rotation and response

Each credential has an owner, purpose, and review date. Maintainers rotate it at
least annually and whenever a maintainer, provider, or trust boundary changes.
Suspected exposure triggers immediate revocation, replacement, and review of
logs and artifacts. Report exposure through [SECURITY.md](../SECURITY.md), not
a public issue.

Changes to organization-wide permissions, template secret access, or release
credentials require a pull request and an independent review when another
maintainer is available.
