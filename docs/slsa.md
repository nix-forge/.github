# SLSA build scope

This repository contains organization community-health files, workflow
templates, and policy documentation. It does not publish software, packages,
or compiled release assets, so there is no SLSA Build Level 3 artifact to
attest here.

The release-producing repositories use the pinned reusable builders in
`nix-forge/ci`. Their builders create the distributable bytes and provenance in
an isolated GitHub-hosted job; a separate protected publisher verifies the
result before release. Every artifact-bearing GitHub release must attach the
portable `*.intoto.jsonl` provenance bundle before the draft release is
published and made immutable. Changes to those builder contracts and their
caller pins must be reviewed together.

SLSA Build Level 3 is a claim about a named distributed artifact and its
trusted builder. It is not a claim about source files, documentation, or
routine CI output. See the [SLSA Build specification](https://slsa.dev/spec/v1.2/)
and [GitHub's artifact-attestation guidance](https://docs.github.com/en/actions/concepts/security/artifact-attestations)
for the model.
