<!-- markdownlint-disable -->

# Hardening Report: itsmeow--curseforge-upload/v3.1.2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **itsmeow--curseforge-upload/v3.1.2** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file uses action references pinned to mutable tags rather than immutable full-length commit SHAs. This exposes the workflow to supply-chain attacks if the upstream tag is moved or the repository is compromised.

Failing references:
- `uses: actions/checkout@v2` (line 14) — should be pinned to a full 40-character SHA
- `uses: actions/setup-node@v4` (line 16) — should be pinned to a full 40-character SHA

Locations:

- `.github/workflows/check-dist.yml:14`
- `.github/workflows/check-dist.yml:16`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and the only job (`check-dist`) also has no job-level `permissions:` block. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (e.g., write access to contents). A minimal explicit permissions block (e.g., `permissions: contents: read`) should be added.

Locations:

- `.github/workflows/check-dist.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/check-dist.yml: (1) Added top-level `permissions: contents: read` block to restrict the default token to the minimum needed for a read-only dist-check workflow. (2) Pinned `actions/checkout@v2` to full SHA `ee0669bd1cc54295c223e0bb666b733df41de1c5 # v2`. (3) Pinned `actions/setup-node@v4` to full SHA `49933ea5288caeca8642d1e84afbd3f7d6820020 # v4`. SHAs were resolved via lookup_action_sha.

