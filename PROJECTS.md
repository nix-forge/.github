# nix-forge project scope

The nix-forge organization maintains the following public repositories as one
related open source project. Each repository owns its source, releases, and
security decisions; shared organization files do not replace repository-level
review.

| Repository | Responsibility |
| --- | --- |
| [.github](https://github.com/nix-forge/.github) | Organization community files, workflow templates, and defaults |
| [ci](https://github.com/nix-forge/ci) | Reusable CI workflows, actions, and queue contracts |
| [nix-conf](https://github.com/nix-forge/nix-conf) | Reusable NixOS, nix-darwin, and Home Manager modules plus deployed examples |
| [nix-config-framework](https://github.com/nix-forge/nix-config-framework) | Convention-based target discovery and module composition |
| [nix-seal](https://github.com/nix-forge/nix-seal) | Secret-management CLI and Nix integration |
| [nix-homelab](https://github.com/nix-forge/nix-homelab) | Reusable homelab service modules and deployment examples |
| [nixpkgs-personal](https://github.com/nix-forge/nixpkgs-personal) | Maintained package expressions, overlays, and NUR metadata |
| [vpn-confinement](https://github.com/nix-forge/vpn-confinement) | Fail-closed VPN namespaces, routing, DNS, and firewall modules |

The minimum security contract for every repository is protected `main`,
two-factor authentication for organization members, signed-off contributions,
least-privilege CI, dependency and code scanning appropriate to its dependency
surface, published OpenSSF Scorecard results for eligible public repositories,
private vulnerability reporting, and a documented release/support policy. A
repository may add stricter controls for its runtime, packaging, or workflow
role.

Changes to shared templates or the CI library require a caller impact review.
Changes to organization settings are recorded separately from source changes.

## Organization settings

The organization requires two-factor authentication for members. GitHub Actions
is enabled for all repositories, uses read-only default workflow permissions,
cannot approve pull requests, and requires every action and reusable workflow
reference to use a full commit SHA. The protected `main` branches require the
repository's required checks, one approving review, approval of the latest
push, linear history, a merge queue, and no force-push or deletion access.

Because the organization currently has one member, `IanHollow` is the explicit
pull-request-only bypass actor for the review and merge-queue rules. This lets
the maintainer merge fully green maintenance changes without removing review
protection for other contributors. Remove this exception when an independent
maintainer is available.

Repositories that publish release archives or executable assets use the
reviewed reusable SLSA builders in [nix-forge/ci](https://github.com/nix-forge/ci).
The builder creates and attests the exact release bytes without release-write
access; a protected publisher verifies the signer workflow and then publishes
an immutable release. Source-only repositories do not claim SLSA Build Level 3
for routine CI output, documentation, or a flake that is consumed directly.
