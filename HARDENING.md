<!-- markdownlint-disable -->

# Hardening Report: sudo-bot--action-pull-request-merge/v1.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **sudo-bot--action-pull-request-merge/v1.1.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All 5 `uses:` references across the workflow files use mutable version tags instead of full 40-character SHA commit hashes, making them vulnerable to supply-chain attacks if the referenced tag is moved or the repository is compromised.

Failing references:
- `actions/checkout@v1` (build.yml)
- `actions/setup-node@v1` (build.yml)
- `actions/cache@v1.0.3` (build.yml)
- `sudo-bot/action-pull-request-lock@v1.0.5` (lock.yml)
- `sudo-bot/action-pull-request-merge@v1.1.0` (merge.yml)

Each should be pinned to a full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v1`.

Locations:

- `.github/workflows/build.yml:8`
- `.github/workflows/build.yml:9`
- `.github/workflows/build.yml:12`
- `.github/workflows/lock.yml:9`
- `.github/workflows/merge.yml:9`

### missing-permissions (severity: medium)

None of the three workflow files define a top-level `permissions:` block, and none of the individual jobs define their own `permissions:` block. Without explicit permissions, workflows run with the default (often broad) token permissions, violating the principle of least privilege. Each workflow should declare the minimal permissions required (e.g. `permissions: contents: read` or `pull-requests: write` as appropriate).

Locations:

- `.github/workflows/build.yml:1`
- `.github/workflows/lock.yml:1`
- `.github/workflows/merge.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 5 unpinned `uses:` references by pinning to full SHA hashes (with original tags as comments): actions/checkout@v1 → @50fbc622fc4ef5163becd7fab6573eac35f8462e, actions/setup-node@v1 → @f1f314fca9dfce2769ece7d933488f076716723e, actions/cache@v1.0.3 → @cffae9552bb9f84b9812c1ee9ea2e3c0a70a797e, sudo-bot/action-pull-request-lock@v1.0.5 → @875cc6a949fa9de15563404110fff799d65d4ac9, sudo-bot/action-pull-request-merge@v1.1.0 → @63e3b8fbc04081354c7de47a38d8d8edeefe4be0. Added minimal top-level permissions blocks to all three workflows: build.yml gets `contents: read`, lock.yml gets `pull-requests: write`, merge.yml gets `contents: write` and `pull-requests: write`.

