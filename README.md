# nix-forge community files

Organization workflow templates call the pinned release in [nix-forge/ci](https://github.com/nix-forge/ci). Choose a template in the Actions tab and select the systems your repository supports. Template edits do not update existing copies; Dependabot updates the shared workflow references. The complete repository map and shared security contract are in [PROJECTS.md](PROJECTS.md).

The shared CI library owns validation and queue policy. This repository validates its own workflows and templates with that library's syntax, security and contract checks. Each template has matching metadata with a name and description. Keep all shared references on one reviewed release commit.

Release-producing repositories use the pinned reusable SLSA builders in
[`nix-forge/ci`](https://github.com/nix-forge/ci). See [docs/slsa.md](docs/slsa.md)
for the organization scope and why source-only repositories do not attest
routine CI output.

The Nix template retains repository-owned build definitions. Repositories using a merge queue must configure required checks and validate both PR and merge-group events. Metadata automation must execute pinned shared actions without checking out PR code. See the [shared design and migration guide](https://github.com/nix-forge/ci/blob/main/docs/architecture.md).

Dependabot covers both root workflows and `/workflow-templates`, grouping each
action dependency across those directories. The root location alone only covers
`.github/workflows` and root action metadata. Explicit template coverage prevents
runtime and onboarding pins from drifting. See the
[Dependabot directory and grouping reference](https://docs.github.com/en/code-security/reference/supply-chain-security/dependabot-options-reference#directories-or-directory).

The Nix starter discovers lockfiles and nested partitions. Flake checks follow
the repository's declared outputs. Protect the stable `Flake lock health` gate
instead of matrix jobs named after paths; its success requires every discovered
lockfile to pass. The shared validator discovers nested composite actions using
either YAML extension.
