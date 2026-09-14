# Dependency management policy

This repository's dependency surface is its workflow and action references,
template metadata, and the external documentation links used by community
files. It does not contain an application dependency graph or a compiled
release.

## Inventory and selection

- External actions and reusable workflows use full commit-SHA references with
  a reviewed version comment. Dependabot covers root workflows and copied
  workflow templates.
- A shared workflow or template change records caller impact, permission
  changes, and migration requirements in the pull request.
- New external tooling is selected for maintained upstream support, a clear
  source, compatible licensing, and a practical update path.

## Automated evaluation

The repository runs workflow syntax, security, metadata, and contract checks.
The dependency-review template is provided for caller repositories. GitHub's
dependency-review action is not run as a self-check here because this
repository has no GitHub-supported dependency manifest to compare. Its own
action references are checked by the shared validator, CodeQL, and Dependabot.

## Remediation and release gate

Malicious dependencies, known exploited vulnerabilities, high or critical SCA
findings, and prohibited licenses block any future packaged release. Lower
severity findings are resolved before release unless a maintainer records a
time-bounded, non-exploitable exception in `security/vex.json` with an owner,
scope, compensating controls, and review date.

Template and shared-action changes are reviewed in a representative caller
before publication. A release must not introduce a mutable action reference,
an unbounded permission, or an undocumented caller migration.
