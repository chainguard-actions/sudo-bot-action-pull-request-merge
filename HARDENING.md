<!-- markdownlint-disable -->

# Hardening Report: sudo-bot--action-pull-request-merge/v1.2.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **sudo-bot--action-pull-request-merge/v1.2.0** was hardened automatically. 6 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### missing-permissions (severity: medium)

build.yml has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions.

Locations:

- `.github/workflows/build.yml:1`

### missing-permissions (severity: medium)

lock.yml has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions.

Locations:

- `.github/workflows/lock.yml:1`

### missing-permissions (severity: medium)

merge.yml has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions.

Locations:

- `.github/workflows/merge.yml:1`

### unpinned-uses (severity: high)

build.yml references three actions by mutable version tags instead of full 40-character commit SHAs: `actions/checkout@v3` (line 8), `actions/setup-node@v3` (line 9), `actions/cache@v3` (line 12). These can be silently updated to include malicious code.

Locations:

- `.github/workflows/build.yml:8`
- `.github/workflows/build.yml:9`
- `.github/workflows/build.yml:12`

### unpinned-uses (severity: high)

lock.yml references `sudo-bot/action-pull-request-lock@v1.0.5` by a mutable version tag instead of a full 40-character commit SHA. This reference can be silently updated to include malicious code.

Locations:

- `.github/workflows/lock.yml:11`

### unpinned-uses (severity: high)

merge.yml references `sudo-bot/action-pull-request-merge@v1.2.0` by a mutable version tag instead of a full 40-character commit SHA. This reference can be silently updated to include malicious code.

Locations:

- `.github/workflows/merge.yml:11`

## Iteration Notes

### Iteration 1

**Fixes applied:** missing-permissions, unpinned-uses

**Notes:**

Fixed all 6 findings across 3 workflow files:

1. build.yml: Added `permissions: {}` top-level block; pinned actions/checkout@v3 to SHA a37ce9120846195fa4ece8f58b268e6043cb2f26, actions/setup-node@v3 to SHA 3235b876344d2a9aa001b8d1453c930bba69e610, and actions/cache@v3 to SHA 6f8efc29b200d32929f49075959781ed54ec270c.

2. lock.yml: Added `permissions: {}` top-level block; pinned sudo-bot/action-pull-request-lock@v1.0.5 to SHA 875cc6a949fa9de15563404110fff799d65d4ac9.

3. merge.yml: Added `permissions: {}` top-level block; pinned sudo-bot/action-pull-request-merge@v1.2.0 to SHA 5b58b5cb1e46bda23160c3a6d56beeec7036c7e2.

All original version tags are preserved as inline comments for readability.

