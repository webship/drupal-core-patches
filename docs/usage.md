# Usage & installation

You normally do **not** require this package directly — `webship/patches` requires it for you.

## Direct use

```bash
composer require webship/drupal-patches:~11.3.0
```

Composer selects the release whose `conflict` allows your installed `drupal/core` (e.g. on core 11.3 it
selects the `11.3.x` line). Ensure patching is enabled in the root project:

```json
{
  "config": { "allow-plugins": { "cweagans/composer-patches": true, "webship/patches": true } }
}
```

## What it provides

- `extra.patches."drupal/core"` — the curated core patch list for the matching core minor.
- `conflict."drupal/core"` — binds the package to that minor.
- `require.cweagans/composer-patches` — the patch applier.
