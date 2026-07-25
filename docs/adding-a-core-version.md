# Adding a Drupal core version

When Webship starts supporting a new Drupal core minor (e.g. `11.4`):

1. **Branch**: create `11.4.x` from the closest existing branch (`11.3.x`).
2. **composer.json**: set `conflict."drupal/core"` to `"<11.4.0 || >=11.5.0"` and the branch-alias to
   `{ "dev-11.4.x": "11.4.x-dev" }`.
3. **Patches**: re-roll each core patch for 11.4, commit the `.patch` files to the **`patches`** branch,
   and point the URLs in `11.4.x` composer.json to
   `https://raw.githubusercontent.com/Webship/drupal-patches/refs/heads/patches/<file>`. Drop patches
   fixed in 11.4 core; add any new ones.
4. **Release**: tag `11.4.0` on the `11.4.x` branch (see [releasing.md](releasing.md)).
5. **Consumers**: the `webship/patches` branches already require `~11 || ~12`, so no change is needed for
   them to pick up `11.4.0`.
