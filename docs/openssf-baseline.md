# OpenSSF baseline policy

This repository follows the [OSPS Baseline](https://baseline.openssf.org/versions/2026-08-28)
version 2026.08.28. The policy covers organization community files, workflow
templates, repository defaults, documentation, and CI.

## Project scope and releases

.github publishes community-health files, issue and pull-request templates,
workflow templates, and organization documentation. It does not publish a
software release, compiled asset, or package. Changes are consumed by copying
templates or by GitHub organization defaults. Future changes to shared workflow
contracts must be reviewed against the caller repositories.
The SLSA scope and the trusted-builder policy are documented in
[docs/slsa.md](slsa.md).

The related repositories and their common security contract are listed in
[`PROJECTS.md`](../PROJECTS.md). Template changes are reviewed with the
affected repositories so their security requirements remain at least as strict
as this project.

## Change and build controls

Every commit must carry a matching Signed-off-by trailer. The DCO file defines
the certificate and .github/workflows/dco.yml checks proposed non-merge commits
on pull requests and merge-group refs.

All workflows start with empty default permissions. Jobs grant only the scopes
they need, checkout does not persist credentials, and actions use full commit
SHAs. Pull requests and merge groups run workflow and template validation,
CodeQL for workflow files, and the repository test suite before protected main
can advance. The dependency-review template remains available for caller
repositories, but this repository has no GitHub-supported dependency manifest
for the action to compare. Its own action references are checked by the
workflow contract validator, Dependabot, CodeQL, and the template checks.

The normal evidence set is the shared workflow validator from nix-forge/ci and
the repository's own CI workflow. Template changes include metadata checks and
a representative caller review. No workflow template may request secrets or
broad permissions by default.

## Dependency and future release controls

Workflow pins, template metadata, and shared release references are reviewed
with their security and compatibility impact. Caller repositories use the
dependency-review template to block new low-or-higher severity
vulnerabilities. This repository's action references are checked by the
workflow contract validator, Dependabot, and CodeQL. SCA findings must be
fixed before any future packaged release unless a reviewed suppression records
why the finding is not exploitable.

This repository has no software release or compiled release asset. If that
changes, a release must use a unique tag, scoped change log, integrity
evidence, a security assessment, release identity and verification instructions,
and a support window. Shared workflow design and caller migrations must be
reviewed before the release.

The [dependency management policy](dependency-management.md) defines how
workflow and template dependencies are selected, pinned, reviewed, and
updated. The [secret management policy](secret-management.md) defines how
organization credentials are stored, accessed, rotated, and revoked. The
organization-wide repository contract is recorded in
[PROJECTS.md](../PROJECTS.md).

## Governance and vulnerability response

Organization administration and repository settings are controlled by the
organization owner. Template and default changes require maintainer review.
Access to sensitive resources is granted after review of the contributor's
history and intended responsibility.

Report vulnerabilities through [SECURITY.md](../SECURITY.md) or GitHub private
vulnerability reporting. The maintainer acknowledges reports within three
business days and provides an initial assessment within seven days. Public
disclosure follows a fix or documented mitigation. [security/vex.json](../security/vex.json)
records reviewed non-affectability statements. Support rules are in
[SUPPORT.md](../SUPPORT.md).

## Control evidence

| Control area | Evidence |
| --- | --- |
| Least-privilege CI and trusted inputs | Empty defaults, job scopes, pinned actions, template validation, and no template secrets |
| Releases and change logs | This release policy and caller migration review |
| Dependencies | Template pins, the caller dependency-review template, Dependabot, and CodeQL |
| Build and test instructions | [CONTRIBUTING.md](../CONTRIBUTING.md) and the shared validator |
| Governance | [GOVERNANCE.md](../GOVERNANCE.md) |
| Contributor legal agreement | [DCO](../DCO) and .github/workflows/dco.yml |
| Security assessment | [THREAT_MODEL.md](../THREAT_MODEL.md) |
| Vulnerability response | [SECURITY.md](../SECURITY.md), private reporting, advisories, and [security/vex.json](../security/vex.json) |
| Public interfaces and release identity | Template metadata, workflow contracts, reviewed commits, and future signed manifests |
| Support lifecycle | [SUPPORT.md](../SUPPORT.md) |

Review this policy when a template, organization default, workflow reference,
permission, or security process changes.
