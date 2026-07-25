# Changelog — webship/drupal-core-patches (`12.0.x`)

All notable changes on the `12.0.x` branch of [`webship/drupal-core-patches`](https://github.com/webship/drupal-core-patches), newest first.
Each release lists the commits — merged pull requests and the drupal.org issues they reference — since the previous release.
`#N` links to the pull request; 7-digit `#NNNNNNN` refs are drupal.org issues. Generated from git history.

## [Unreleased]

- ci: Fix the "Upload the install log" artifact name on PR runs -- `github.ref_name` resolves to `<PR>/merge` on a pull_request run, and the `/` made `actions/upload-artifact@v4` reject the name and fail the job `if: always()` even when every patch applied cleanly (that is what made #58-#61 report red). PR runs now use `pr-<number>`; branch pushes keep the readable `<branch>` name

## [12.0.0.2] - 2026-07-06

- docs: Add `CHANGELOG.md` for the `12.0.x` branch (#11)

## [12.0.0.1] - 2026-06-28

- task: keep it a pure Drupal core patches storage metapackage, not a Composer plugin

## [12.0.0] - 2026-06-28

- Initial tracked release on the `12.0.x` branch.

