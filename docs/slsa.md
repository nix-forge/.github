# SLSA scope and adoption plan

Reviewed 21 September 2026 against the
[approved SLSA 1.2 specification](https://slsa.dev/spec/v1.2/). This page records
each repository's assessed scope and next steps. No repository-wide SLSA level
is claimed.

SLSA has separate [Build](https://slsa.dev/spec/v1.2/build-track-basics) and
[Source](https://slsa.dev/spec/v1.2/source-requirements) tracks. Build levels apply to
identified distributed artifact bytes. Build L3 requires a hosted, hardened builder that
isolates runs and keeps provenance signing material outside build steps, on top of signed
provenance and consumer verification. Source L3 applies to identified source revisions on
protected references. It requires the source control system to enforce and attest the
organization's declared technical controls. A branch rule or green CI run alone is not a
Source L3 attestation. Neither track rates a GitHub repository as a whole, and a build
level does not flow through to dependencies or consumer builds.

[GitHub's guidance](https://docs.github.com/en/actions/how-tos/secure-your-work/use-artifact-attestations/increase-security-rating)
describes reusable workflows plus artifact attestations as a route to SLSA v1.0 Build
L3. It does not assert conformance to the newer 1.2 specification, which needs its own
assessment. The reusable workflow must produce the distributed bytes and the attestation. The publisher
and consumer must verify the subject digest and expected signer identity. A badge claim
needs a published, independently verifiable example, not just workflow YAML.

## Current assessment and next gate

| Repository | Distributed output in scope | Current evidence | Next gate before a Level 3 claim |
| --- | --- | --- | --- |
| [`ci`](https://github.com/nix-forge/ci) | Tagged source archive | The v2.8.0 archive has a portable provenance bundle and its attestation verifies against the pinned `slsa-source-release.yml` builder at `2705c51e254ef3f43e90da1ab8fc717a54991487`. This is a Build L3 candidate for that archive only; the signer and subject have been verified, while the builder trust assessment remains a separate decision. | Keep release verification and the builder pin synchronized for every later tag. Add a release verification record for each published artifact. |
| [`nix-config-framework`](https://github.com/nix-forge/nix-config-framework) | Tagged source archive | The release workflow calls a pinned source builder and verifies its output before publication. No published release asset was available at review time. | Publish a reviewed release, download its archive and bundle, and verify digest, source commit, signer workflow, and pinned builder commit. Then scope the Build L3 claim to that archive. |
| [`nix-seal`](https://github.com/nix-forge/nix-seal) | Platform executables and release metadata | The workflow calls a pinned hosted builder and attests staged assets, but no published release was available at review time. `nix build` currently permits binary substitution, so the workflow alone does not establish that the executable was compiled in the attested job. | Define and test a trusted build or verified substitution policy, record dependency/cache identities, exercise each supported platform, and verify actual release bytes and attestations after the independent audit and release gates. Do not claim Build L3 for an executable until this is complete. |
| [`vpn-confinement`](https://github.com/nix-forge/vpn-confinement) | Git source and generated documentation | No separate tagged, attested release artifact. | Decide whether to distribute a versioned source archive or documentation bundle. If so, use a pinned reusable builder and verify its release. Otherwise focus on source controls and avoid a Build level claim for the flake. |
| [`nix-homelab`](https://github.com/nix-forge/nix-homelab) | Git source and generated handbook | No separate tagged, attested release artifact. | Apply the same release decision as `vpn-confinement`; test any new archive against the flake's documented consumer path. |
| [`nixpkgs-personal`](https://github.com/nix-forge/nixpkgs-personal) | Package recipes and consumer-built outputs | No single repository-wide binary release. Packages have distinct upstream sources and build paths. | Inventory packages actually distributed by this organization. Attest each selected output at its distribution boundary with a trusted builder. Do not apply one Build level to the package catalog, third-party downloads, NUR metadata, or a consumer's Nix build. |
| [`nix-conf`](https://github.com/nix-forge/nix-conf) | Git configuration and guide | No distributable NixOS system release. Local and remote host closures include machine-specific inputs and deployment steps. | Keep host builds separate from a public artifact claim. If the guide or starter becomes a versioned download, build, attest, publish, and verify those exact bytes. |
| [`.github`](https://github.com/nix-forge/.github) | Organization policy and workflow templates | No software release artifact. Templates call pinned `ci` workflows but are source consumed by other repositories. | Keep template pins, callers, and contract tests synchronized. Assess the Source track; no Build L3 claim is applicable without a defined distributed artifact. |

The `ci` verification result above comes from downloading `nix-forge-ci-v2.8.0.tar.gz`
from the [v2.8.0 release](https://github.com/nix-forge/ci/releases/tag/v2.8.0) and
running:

```console
gh attestation verify nix-forge-ci-v2.8.0.tar.gz \
  --repo nix-forge/ci \
  --signer-workflow nix-forge/ci/.github/workflows/slsa-source-release.yml \
  --signer-digest 2705c51e254ef3f43e90da1ab8fc717a54991487
```

## Organization rollout

1. **Name the subjects.** For each release-producing repository, list exact output names,
   platforms, consumers, and distribution channels. Treat a tagged source archive,
   executable, generated site, Nix store path, and consumer-built closure as different
   subjects. Document which are intentionally outside the release boundary.
2. **Prove Build L3 per release.** Keep build and provenance generation in an immutable,
   organization-owned reusable workflow on a GitHub-hosted runner. Pin the builder and
   actions to reviewed commits. Remove release-write access and long-lived signing keys
   from builder jobs. Publish only the builder's verified bytes through a protected
   publisher. Attach the portable `*.intoto.jsonl` provenance bundle beside every
   downloadable release artifact before publishing the draft as an immutable release.
   Check the subject digest, source revision, predicate, signer workflow, and
   builder commit using a fresh download of the published asset. Record failures as
   release blockers. See the [SLSA verification requirements](https://slsa.dev/spec/v1.2/verifying-artifacts) and [GitHub's attestation verification guidance](https://docs.github.com/en/actions/how-tos/secure-your-work/use-artifact-attestations/increase-security-rating).
3. **Address Nix substitution before binary claims.** For `nix-seal` and any future
   package release, decide whether to compile the output within the trusted build or
   accept only explicitly trusted substituters with independently verified artifact
   provenance. Test the selected policy on Linux and macOS and document the exact Nix
   flags, substituter configuration, cache keys, and remaining trust assumptions. An
   attestation over a copied executable identifies the copy; it cannot by itself prove
   where substituted bytes were compiled.
4. **Assess Source L3 separately.** Inventory protected branches and tags in all eight
   repositories. Check access controls, change history, required checks, bypass paths, and
   organization policy. Determine whether the source control system can issue source
   provenance and a verification summary attestation that proves the declared controls for
   each revision, as [Source L3 requires](https://slsa.dev/spec/v1.2/source-requirements).
   Until that evidence exists, report controls individually rather than claiming Source
   L3. Preserve Source L4 as a separate two-person review target.
5. **Maintain the claims.** For each claimed release, keep a verification command and
   record tied to the tag and builder commit. Reassess when the builder, release workflow,
   runner, artifact set, branch rules, or distribution channel changes. Use a level badge
   only if it names the Build or Source track and specification version and links to
   verified subjects and evidence for the current release. A workflow status badge
   reports whether CI passed; it does not verify a SLSA level.

This plan describes provenance and release integrity. It does not replace vulnerability
management, dependency review, reproducibility checks, or the security audit required for
`nix-seal` 1.0.
