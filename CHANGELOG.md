# Changelog — webship/drupal-core-patches (`11.4.x`)

All notable changes on the `11.4.x` branch of [`webship/drupal-core-patches`](https://github.com/webship/drupal-core-patches), newest first.
Each release lists the commits — merged pull requests and the drupal.org issues they reference — since the previous release.
`#N` links to the pull request; 7-digit `#NNNNNNN` refs are drupal.org issues. Generated from git history.

## [Unreleased]

- ci: Fix the "Upload the install log" artifact name on PR runs -- `github.ref_name` resolves to `<PR>/merge` on a pull_request run, and the `/` made `actions/upload-artifact@v4` reject the name and fail the job `if: always()` even when every patch applied cleanly (that is what made #58-#61 report red). PR runs now use `pr-<number>`; branch pushes keep the readable `<branch>` name

## [11.4.0.4] - 2026-07-06

- task: Add a patch for Drupal Core on Issue #2701575: RequestContext throws error when current request is empty (#19)
- task: Change a patch for the Drupal Core module on Issue #3049332 (#17)
- task: Change a patch for the Drupal Core module on Issue #3101231 (#16)
- docs: Add `CHANGELOG.md` for the `11.4.x` branch (#10)
- task: patch drupal/core for #2741429 (EntityDisplayBase null mode entity, 11.4 install regression via drupal_cms_search recipe)

## [11.4.0.3] - 2026-07-01

- task: Update drupal-core-patches 11.4.x for Drupal 11.4.0 stable

## [11.4.0.2] - 2026-06-28

- task: keep it a pure Drupal core patches storage metapackage, not a Composer plugin

## [11.4.0.1] - 2026-06-28

- task: patch drupal/core for #3606822 (ClassResolver synthetic kernel on install)

## [11.4.0] - 2026-06-28

- Initial tracked release on the `11.4.x` branch.

