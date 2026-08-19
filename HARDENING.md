<!-- markdownlint-disable -->

# Hardening Report: sudo-bot--action-pull-request-merge/v2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **sudo-bot--action-pull-request-merge/v2** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files use mutable tag or branch refs instead of pinned 40-character SHA commit hashes, making the action vulnerable to supply-chain attacks if the referenced tag is moved or overwritten.

build.yml:
- `actions/checkout@v6` (line 9)
- `dtolnay/rust-toolchain@stable` (line 11)
- `Swatinem/rust-cache@v2` (line 14)
- `docker/setup-qemu-action@v3` (line 24)
- `docker/setup-buildx-action@v4` (line 25)

lock.yml:
- `sudo-bot/action-pull-request-lock@v1.0.5` (line 14)

merge.yml:
- `sudo-bot/action-pull-request-merge@v1.2.0` (line 14)

release.yml:
- `actions/checkout@v6` (line 20)
- `docker/setup-qemu-action@v3` (line 23)
- `docker/setup-buildx-action@v3` (line 26)
- `docker/login-action@v3` (line 28)

action.yml:
- `runs.image: "docker://ghcr.io/sudo-bot/action-pull-request-merge:latest"` — uses a mutable `:latest` tag instead of a SHA digest (e.g., `@sha256:<64-hex-char-digest>`).

Locations:

- `.github/workflows/build.yml:9`
- `.github/workflows/build.yml:11`
- `.github/workflows/build.yml:14`
- `.github/workflows/build.yml:24`
- `.github/workflows/build.yml:25`
- `.github/workflows/lock.yml:14`
- `.github/workflows/merge.yml:14`
- `.github/workflows/release.yml:20`
- `.github/workflows/release.yml:23`
- `.github/workflows/release.yml:26`
- `.github/workflows/release.yml:28`
- `action.yml:32`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all mutable action references to full 40-character SHA commit hashes and the container image to its sha256 digest:
- build.yml: actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803, dtolnay/rust-toolchain@stable → @4cda84d5c5c54efe2404f9d843567869ab1699d4, Swatinem/rust-cache@v2 → @e18b497796c12c097a38f9edb9d0641fb99eee32, docker/setup-qemu-action@v3 → @c7c53464625b32c7a7e944ae62b3e17d2b600130, docker/setup-buildx-action@v4 → @bb05f3f5519dd87d3ba754cc423b652a5edd6d2c
- lock.yml: sudo-bot/action-pull-request-lock@v1.0.5 → @875cc6a949fa9de15563404110fff799d65d4ac9
- merge.yml: sudo-bot/action-pull-request-merge@v1.2.0 → @5b58b5cb1e46bda23160c3a6d56beeec7036c7e2
- release.yml: actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803, docker/setup-qemu-action@v3 → @c7c53464625b32c7a7e944ae62b3e17d2b600130, docker/setup-buildx-action@v3 → @8d2750c68a42422c14e847fe6c8ac0403b4cbd6f, docker/login-action@v3 → @c94ce9fb468520275223c153574b00df6fe4bcc9
- action.yml: ghcr.io/sudo-bot/action-pull-request-merge:latest → :latest@sha256:5823f889428ed4db84e853000bd79ed23af0fb9b758d7b68457874b56a870597 (docker:// scheme preserved)

