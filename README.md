# Drupal core patch files

> **Why this package:** `webship/drupal-patches` is required by [`webship/patches`](https://github.com/webship/patches) so that [Webship](https://www.drupal.org/project/webship) can upgrade to the latest Drupal core versions. It maintains the right set of working Drupal **core** patches **per Drupal core version** (one branch per major.minor), so each Webship line automatically gets the patches that apply to its Drupal core.

Flat store of the Drupal **core** `.patch` files used by Webship, kept on this `patches`
branch and referenced by raw URL from the per-core-minor branches (`11.3.x`, `10.6.x`, …):

```
https://raw.githubusercontent.com/webship/drupal-patches/refs/heads/patches/<file>.patch
```
