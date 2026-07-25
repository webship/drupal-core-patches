# Architecture

## Model

`webship/drupal-patches` is a **metapackage** (no source code, never installed to disk). Its only
job is to declare Drupal core patches and bind them to a Drupal core minor.

```
11.3.x   composer.json  -> extra.patches."drupal/core" (URLs to the patches branch), conflict drupal/core <11.3||>=11.4
10.6.x   composer.json  -> extra.patches."drupal/core",                               conflict drupal/core <10.6||>=10.7
patches  *.patch        -> flat store of the actual patch files (raw-URL referenced)
```

## Why one branch per Drupal core major.minor

A given Drupal core patch is usually valid for one core minor only (it is re-rolled per minor). Keeping
one branch per minor lets each branch carry exactly the right patch revisions, and the per-branch
`conflict` on `drupal/core` means Composer can only select the branch/release that matches the installed
core. Consumers therefore require a broad range (`~10 || ~11 || ~12`) and Composer resolves to the single
compatible release.

## Why a metapackage + a separate `patches` branch

- **metapackage**: nothing is installed to disk, so patches must be referenced by URL. The composer.json
  lists the patch URLs; `cweagans/composer-patches` downloads and applies them.
- **`patches` branch**: the `.patch` files are stored once on a dedicated branch and referenced by raw
  URL (`https://raw.githubusercontent.com/webship/drupal-patches/refs/heads/patches/<file>`), mirroring
  how `patches` stores its files. This keeps the per-core branches to just a `composer.json`.

## How the patches get applied

`webship/patches` is a `cweagans/composer-patches` plugin. It gathers `extra.patches` from packages
in its **`allowed-dependency-patches`** allowlist. `webship/drupal-patches` is on that allowlist, so the
core patches it declares are merged into the patch set and applied to `drupal/core`.
