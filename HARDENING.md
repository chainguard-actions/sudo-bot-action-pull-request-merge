<!-- markdownlint-disable -->

# Hardening Report: sudo-bot--action-pull-request-merge/v2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **sudo-bot--action-pull-request-merge/v2** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yml uses a Docker image with a mutable ':latest' tag instead of a SHA digest. The reference 'docker://ghcr.io/sudo-bot/action-pull-request-merge:latest' can silently change to a different (potentially malicious) image at any time, creating a supply-chain risk. It should be pinned to a specific SHA digest, e.g. 'docker://ghcr.io/sudo-bot/action-pull-request-merge@sha256:<64-hex-char-digest>'.

Locations:

- `action.yml:33`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image reference in action.yml from the mutable 'docker://ghcr.io/sudo-bot/action-pull-request-merge:latest' to the immutable digest 'docker://ghcr.io/sudo-bot/action-pull-request-merge@sha256:5823f889428ed4db84e853000bd79ed23af0fb9b758d7b68457874b56a870597' with a '# latest' comment for readability.

