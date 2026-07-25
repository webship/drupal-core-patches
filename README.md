# Drupal core patches

[![Test patches (11.4.x)](https://github.com/webship/drupal-patches/actions/workflows/test-patches.yml/badge.svg?branch=11.4.x)](https://github.com/webship/drupal-patches/actions/workflows/test-patches.yml?query=branch%3A11.4.x)

> **Why this package:** `webship/drupal-patches` is required by [`webship/patches`](https://github.com/webship/patches) so that [Webship](https://www.drupal.org/project/webship) can upgrade to the latest Drupal core versions. It maintains the right set of working Drupal **core** patches **per Drupal core version** (one branch per major.minor), so each Webship line automatically gets the patches that apply to its Drupal core.

Curated **Drupal core** patches used by [Webship](https://www.drupal.org/project/webship),
delivered as a Composer **metapackage** with **one git branch per Drupal core MAJOR.MINOR**
version (e.g. `11.3.x`, `10.6.x`). Consumed by
[`webship/patches`](https://github.com/webship/patches) so that core patches are
versioned and resolved independently of the Webship line.

- Patches are declared under `extra.patches."drupal/core"` and applied by
  [`cweagans/composer-patches`](https://github.com/cweagans/composer-patches) via the
  Webship Patches plugin (which allowlists this package).
- Each core-minor branch carries **only** the patches valid for that exact Drupal core minor and
  uses `conflict: { "drupal/core": "<minor.0 || >=next.0" }` to bind itself to that minor, so
  Composer always selects the release matching the installed core.
- The actual `.patch` files live on the **`patches`** branch and are referenced by raw URL
  (the same model `patches` uses for its patch files).

## Usage

```bash
composer require webship/drupal-patches:~11.3.0
```

`patches` does this for you. To allow Composer to pick the release matching the site's core,
it requires a range that spans the supported majors:

| patches branch | Drupal core | requires |
|---|---|---|
| 9.1.x, 9.2.x, 10.0.x | ~10.6 | `webship/drupal-patches: ~10 \|\| ~11 \|\| ~12` |
| 10.1.x, 11.0.x | ~11.3 | `webship/drupal-patches: ~11 \|\| ~12` |

## Branch per Drupal core major.minor

**Policy (2026-07-14):** only the Drupal core minors currently supported by the Drupal Core team are
actively maintained here — see [#79](https://github.com/webship/drupal-patches/issues/79). EOL
branches stay in git (nothing is deleted) but no longer receive new patches, re-rolls, or CI fixes.

| Drupal core | Branch    | Patch count | Status |
|-------------|-----------|-------------|--------|
| ~12.0.0 | `12.0.x` | 0 | Upcoming — forward-compat placeholder, no patches yet |
| ~11.4.0 | `11.4.x` | 22 | **Supported** (bugfix + security) |
| ~11.3.0 | `11.3.x` | 20 | **Supported** (security-only) |
| ~10.6.0 | `10.6.x` | 17 | **Supported** (security-only, final Drupal 10 minor) |
| ~11.2.0 | `11.2.x` | 21 | **EOL — not actively maintained here** (see [#79](https://github.com/webship/drupal-patches/issues/79)) |
| ~11.1.0 | `11.1.x` | 20 | **EOL — not actively maintained here** (see [#79](https://github.com/webship/drupal-patches/issues/79)) |
| ~10.5.0 | `10.5.x` | 20 | **EOL — not actively maintained here** (see [#79](https://github.com/webship/drupal-patches/issues/79)) |
| ~10.4.0 | `10.4.x` | 20 | **EOL — not actively maintained here** (see [#79](https://github.com/webship/drupal-patches/issues/79)) |
| (files) | `patches` | shared `.patch` file store | active |

Add a new branch (e.g. the next Drupal core minor) when supporting a new Drupal core minor — see
[docs/adding-a-core-version.md](docs/adding-a-core-version.md). Adding a branch for an EOL minor is
out of scope per #79.

## Documentation

- [Architecture](docs/architecture.md)
- [Usage & installation](docs/usage.md)
- [Adding a Drupal core version](docs/adding-a-core-version.md)
- [Releasing](docs/releasing.md)
- [Troubleshooting](docs/troubleshooting.md)
