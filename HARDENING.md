<!-- markdownlint-disable -->

# Hardening Report: itsmeow--curseforge-upload/v3.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **itsmeow--curseforge-upload/v3.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file .github/workflows/test.yml contains two unpinned `uses:` references that use mutable tags/branches instead of full 40-character commit SHA digests, making the action vulnerable to supply-chain attacks:
- `actions/checkout@v1` (mutable tag)
- `itsmeow/curseforge-upload@master` (mutable branch)

Locations:

- `.github/workflows/test.yml:11`
- `.github/workflows/test.yml:13`

### missing-permissions (severity: medium)

The workflow file .github/workflows/test.yml has no top-level `permissions:` key and the single job `test` also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the default (potentially broad) repository permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/test.yml: (1) Pinned `actions/checkout@v1` to full SHA `50fbc622fc4ef5163becd7fab6573eac35f8462e` and `itsmeow/curseforge-upload@master` to full SHA `1493c4408b462f2ad8beb600f09c505e0c158397`, preserving original refs as comments. (2) Added top-level `permissions: {}` to enforce least-privilege — the workflow only uploads to CurseForge via a secret token and requires no GitHub API permissions.

