<!-- markdownlint-disable -->

# Hardening Report: itsmeow--curseforge-upload/v2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **itsmeow--curseforge-upload/v2** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file .github/workflows/test.yml references two actions by mutable tag/branch instead of a full 40-character commit SHA:
- `uses: actions/checkout@v1` — `v1` is a mutable tag; a supply-chain attacker could push a new commit to that tag.
- `uses: itsmeow/curseforge-upload@master` — `master` is a mutable branch ref.
Both should be pinned to a full SHA (e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v1`).

Locations:

- `.github/workflows/test.yml:11`
- `.github/workflows/test.yml:13`

### missing-permissions (severity: medium)

The workflow file .github/workflows/test.yml has no top-level `permissions:` key and the only job (`test`) also has no `permissions:` key. Without explicit permissions, the workflow inherits the default repository token permissions, which may be broader than necessary. A minimal `permissions: {}` or specific scopes (e.g. `contents: read`) should be declared.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/test.yml: (1) Pinned `actions/checkout@v1` to `actions/checkout@50fbc622fc4ef5163becd7fab6573eac35f8462e # v1`; (2) Pinned `itsmeow/curseforge-upload@master` to `itsmeow/curseforge-upload@1493c4408b462f2ad8beb600f09c505e0c158397 # master`; (3) Added top-level `permissions: {}` to restrict the workflow token to no permissions.

