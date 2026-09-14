# Threat model

## Scope

This model covers community files, workflow templates, organization defaults,
documentation, and repository automation. It does not cover a caller
repository's application code or private credentials.

## Assets and actors

Assets include workflow templates, issue forms, community policy, shared action
references, organization defaults, and repository administration. Contributors
and pull requests are untrusted. Maintainers review changes. The organization
owner controls sensitive settings. Caller repositories consume copies of the
templates and must review local permissions.

## Trust boundaries

The template repository, GitHub template-copy process, caller repository,
Actions runner, and organization settings are separate boundaries. Templates
must not embed secrets. Metadata jobs must not execute pull-request code.

## Main threats and controls

| Threat | Control |
| --- | --- |
| A template grants unsafe permissions to many repositories | Empty defaults, explicit job permissions, pinned actions, and validation |
| A copied workflow drifts from the documented contract | Template metadata, shared contract checks, and caller migration review |
| A pull request changes organization defaults unnoticed | Protected main, DCO, required checks, and maintainer review |
| A workflow reference is compromised | Full commit SHAs, dependency review, CodeQL, and release review |

## Assessment cadence

Before changing a shared template, organization default, or workflow reference,
maintainers review the affected caller repositories, external interfaces, and
critical paths above. The pull request records the security impact, required
caller migration, and any limitation on the resulting control.

Review this model when a template, organization setting, shared workflow
reference, or permission default changes.
