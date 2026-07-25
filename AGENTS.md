# CLAUDE.md — webship/drupal-core-patches

Working notes.

- **Purpose**: hold Drupal **core** patches for Webship, one git branch per Drupal core MAJOR.MINOR.
- **Type**: Composer `metapackage` (no code). Patches declared in `extra.patches."drupal/core"`.
- **Branches**: `11.3.x`, `10.6.x` (core-minor); `patches` (flat `.patch` file store, no composer.json).
- **Binding**: each core-minor branch sets `conflict: {"drupal/core": "<minor.0 || >=next.0"}` so Composer
  selects the release matching the installed core. Consumers require `~10 || ~11 || ~12` (or `~11 || ~12`).
- **Patch files**: stored on the `patches` branch; referenced by raw URL
  `https://raw.githubusercontent.com/webship/drupal-core-patches/refs/heads/patches/<file>`.
- **Consumed by**: `webship/webship-patches` (allowlists this package so its patches apply).
- **Releasing**: tag semver within the minor; **never move a tag** (Packagist fails). See docs/releasing.md.
- Commit author: Rajab Natshah <rajabn@gmail.com>. Disclose AI use.

### Issue / PR titles

Every patch issue and its PRs share ONE title, in this grammar (proper names Capitalized, no trailing period):

`<Action> a patch for the <Target> on <ref>[ -- <reason>]`

- **Action** — `Add` · `Change` · `Remove` · `Update` · `Revert -`. Use `Remove all patches for …` when dropping every patch for a target.
- **Target** — usually `Drupal Core`; occasionally a `<machine> recipe` or a `<vendor/lib> library`.
- **ref** — the upstream change: `fix: #3607821 <summary>` (current commit-type form) or `Issue #3607821: <summary>` (legacy form).
- **reason** (optional) — why now: `-- after Inline Entity Form 3.0.0 was released`.

Rules:

- **A re-roll or a correction of an existing patch is a `Change`** — never `fix: Re-roll…` or any ad-hoc `{type}:` prefix. Keep the upstream type and issue title; the "why now" goes in the `-- <reason>` suffix.
- **A patch change split across branches shares ONE canonical title** — the issue, the `patches`-branch file PR and the version-branch wiring PR all carry the same title.
- **A change ported to several core-minor branches keeps that one title plus a `- for Drupal <x.y.z>` (or `- for Webship <x.y.x>`) suffix per PR** — never a trailing `(<branch>)` tag, never an ad-hoc `ci: #<n> …` prefix. This holds for infrastructure changes (CI workflows, tests, docs) too.
- **Infrastructure / branch issues drop the "patch for" grammar** and state the action directly, e.g. `Add a no-patches branch - to let developers manage their list of patches in the root composer.json`.
- **The patch file name follows the same source of truth as the title.** A corrected or re-rolled file is a NEW dated file (dated files are immutable), named `<package>--YYYY-MM-DD--<issue>--mr-<n>.patch` and dated the day it was cut. Never keep an ad-hoc descriptive slug once the Drupal.org issue and MR numbers are known — that form is only for a fix with no upstream issue/MR to cite. The `extra.patches` key quotes the upstream issue the same way on every branch (`"Issue #3507495: <full upstream title>"`), so one patch reads identically everywhere.

## Never duplicate the community's work — and test before you port

Every patch here comes from somebody else's unpaid work. Before you file an issue or open a
merge request on drupal.org, assume they already found it.

1. **Search the project's issue queue** — by symptom, by the error text, by the class/method in
   the trace, by the PHP/Drupal version. If an open issue covers it, **reuse it**. Never file a
   duplicate. (Closed/Fixed → file a fresh issue; never comment on or MR against a closed one.)

2. **Read every MR on that issue, including MRs against other branches — then TEST.** Ask the
   only question that matters: *does that MR's diff already apply to the branch/version we
   need?*

   ```bash
   curl -sL https://git.drupalcode.org/project/<project>/-/merge_requests/<id>.diff -o mr.diff
   patch -p1 --dry-run < mr.diff     # against a PRISTINE copy of the exact release
   ```

   - **It applies →** there is nothing to port. **Do not open another MR.** Use that MR's diff as
     the patch, credit that MR in the patch name and the PR, and if a maintenance branch really
     needs a backport, say so in a comment on the issue and let the maintainers decide.
     **Backporting is their call.**
   - **It genuinely does not apply →** only then is a branch-port MR justified, and say plainly in
     its description that it is a port of MR !NNNN, why the original does not apply, and what
     changed.

3. **A different target branch is not, on its own, a reason for a new MR.** Two MRs whose diffs
   are byte-identical are one MR and one piece of noise. If you have already opened one, close it
   with an apology and point reviewers at the original.

This happened: an agent opened `drupal/ai` MR !1809 as a `1.4.x` port of !1799. The diffs were
byte-identical and !1799 applied cleanly to 1.4.4. It was closed as a duplicate.

**Be a good citizen.** Follow the [Drupal Code of Conduct](https://www.drupal.org/dcoc), the
project's [documented processes](https://www.drupal.org/docs) and the
[site terms](https://www.drupal.org/terms): be respectful, assume good faith, be brief, credit the
person whose work you are building on by name and issue/MR number, and never present someone
else's fix as your own.
