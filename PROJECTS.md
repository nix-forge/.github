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
