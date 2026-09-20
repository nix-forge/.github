# Governance

The nix-forge organization maintains this repository as the source for public
community files, workflow templates, and organization defaults.

The current organization owner with access to sensitive resources is
[@IanHollow](https://github.com/IanHollow). Additional maintainers are listed
and reviewed before access is granted.

## Roles

The organization owner is responsible for repository administration,
organization-wide security settings, Actions policy, Pages, and release
decisions. Maintainers review changes to templates, community-health files,
and defaults before they affect other repositories. Contributors propose
changes and provide the affected-repository test evidence.

Sensitive access is granted only after review of a contributor's history,
intended responsibility, and need for access. New maintainers receive the
narrowest role needed. Changes that alter organization-wide permissions,
workflow trust, moderation, or security defaults need a documented maintainer
decision. Seek independent review when another maintainer with the needed
access is available.

## Changes

Changes use pull requests, the DCO, required status checks, and protected main.
Template changes explain which existing repositories are affected.
Organization-wide settings are changed separately through GitHub administration
and recorded in the pull request when relevant to a template or default.

## Solo maintainer review and automation

The organization currently has one maintainer. GitHub cannot count an author's
own approval, so `main` requires no approving review while that remains true.
Pull requests, required status checks, the merge queue, DCO, conversation
resolution, and protection against force pushes and deletion remain in force.
The maintainer decides when a human-authored PR is ready. An AI agent may review
and merge on the maintainer's authorization, recording material findings and
fixes in the PR; its review is decision support, not an independent GitHub
approval. Security and privileged automation changes require deliberate
maintainer admission.

The shared queue reconciler may admit trusted, same-repository Dependabot PRs
and explicitly opted-in updater PRs after required checks pass. It refuses
drafts, forks, and changes to workflows, actions, scripts, or workflow
templates. Those changes wait for maintainer admission. When another maintainer
is available, revisit the GitHub approval requirement and independent review
for sensitive changes.
