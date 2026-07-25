# Troubleshooting

## Packagist: "The last update failed"
Almost always caused by a **moved/force-updated tag**. Packagist treats tags as immutable. Fix: delete the
moved tag and cut a new patch version (`11.3.1`) instead. Never `git tag -f` a released tag.

## Core patches are not applied
- Ensure `webship/drupal-patches` is in the consuming plugin's `allowed-dependency-patches`
  (`webship/patches` includes it by default).
- Ensure `cweagans/composer-patches` and `webship/patches` are allowed plugins in the root project.

## Composer cannot resolve `~11.3.0`
A stable tag must exist on the matching branch. With only a dev branch, require `11.3.x-dev` (or use
`minimum-stability: dev`). Releases provide the stable tags.

## Wrong patch set selected for the installed core
Each branch's `conflict."drupal/core"` binds it to one minor. If a patch was selected for the wrong core,
check that branch's `conflict` range and the patch URL points to the correct re-rolled file.
