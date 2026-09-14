# Contributing to nix-forge

The `nix-forge/.github` repository contains organization-wide community files,
shared defaults, and the public landing page. Changes here can affect every
repository in the organization, so keep pull requests focused and explain
cross-repository impact.

Before a substantial change, open an issue or discussion describing the goal,
the affected repositories, and the rollout plan. Use the repository-specific
`CONTRIBUTING.md` for code and configuration changes in another project.

Validate documentation and workflows locally where practical. Do not commit
credentials, tokens, private configuration, or generated output that is not
intended for publication. Security vulnerabilities should be reported through
the private security channel described in `SECURITY.md`.

## Testing policy

Pull requests and merge groups run workflow syntax and security validation,
CodeQL, repository tests, and the template contract checks. Run the applicable
shared CI checks locally before requesting review and include affected-repository
evidence for organization-wide template changes.

Every major change to a community file, workflow template, organization
default, or security setting must add or update an automated regression check.
If an automated test is not practical, record the reason, manual evidence, and
a follow-up plan in the pull request.
