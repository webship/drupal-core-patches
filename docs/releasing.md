# Releasing

Each core-minor branch is released with semver tags **within its minor** (`11.3.0`, `11.3.1`, … on
`11.3.x`; `10.6.0`, … on `10.6.x`).

1. Land changes on the core-minor branch (via PR).
2. **Never move an existing tag** — Packagist rejects moved tags ("last update failed"). Always cut a new
   patch tag (e.g. `11.3.1`) instead of re-pointing `11.3.0`.
3. Tag and push:
   ```bash
   git checkout 11.3.x && git tag -a 11.3.1 -m "Drupal core patches 11.3.1" && git push origin 11.3.1
   ```
4. Packagist auto-updates via the GitHub webhook; verify the new version at
   https://packagist.org/packages/webship/drupal-patches .

The `patches` branch has **no `composer.json`**, so Packagist ignores it (it is a file store only).
