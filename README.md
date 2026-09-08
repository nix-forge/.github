# nix-forge community files

Organization workflow templates call the pinned release in [nix-forge/ci](https://github.com/nix-forge/ci). Choose a template in the Actions tab and select the systems and checks your repository supports. Template edits do not update existing copies; Dependabot updates the shared workflow references.

The shared CI library owns validation and queue policy. This repository validates its own workflows and templates with that library's syntax, security and contract checks. Each template has matching metadata with a name and description. Keep all shared references on one reviewed release commit.

The Nix template retains repository-owned build definitions. Repositories using a merge queue must configure required checks and validate both PR and merge-group events. Metadata automation must execute pinned shared actions without checking out PR code. See the [shared design and migration guide](https://github.com/nix-forge/ci/blob/main/docs/architecture.md).
