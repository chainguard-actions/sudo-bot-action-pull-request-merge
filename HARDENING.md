<!-- markdownlint-disable -->

# Hardening Report: sudo-bot--action-pull-request-merge/v1.0.3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **sudo-bot--action-pull-request-merge/v1.0.3** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All three workflow files reference actions using mutable version tags instead of pinned 40-character SHA commit hashes, making them vulnerable to supply-chain attacks if the tag is moved. Failing references: build.yml uses actions/checkout@v1, actions/setup-node@v1, actions/cache@v1.0.3; lock.yml uses sudo-bot/action-pull-request-lock@v1.0.5; merge.yml uses sudo-bot/action-pull-request-merge@v1.0.3.

Locations:

- `.github/workflows/build.yml:9`
- `.github/workflows/build.yml:10`
- `.github/workflows/build.yml:13`
- `.github/workflows/lock.yml:11`
- `.github/workflows/merge.yml:11`

### missing-permissions (severity: medium)

None of the three workflow files define a top-level `permissions:` block, and no job within them defines a job-level `permissions:` block. Without explicit permissions, workflows run with the default (often broad) token permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/build.yml:1`
- `.github/workflows/lock.yml:1`
- `.github/workflows/merge.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 5 unpinned action references by resolving their full 40-character SHA commit hashes via lookup_action_sha and preserving the original tag as a comment. Added top-level `permissions: {}` to all three workflow files to deny all permissions by default, and added minimal job-level permissions where needed: lock.yml gets `pull-requests: write` for locking PRs, merge.yml gets `pull-requests: write` and `contents: write` for merging PRs, and build.yml requires no additional permissions.

