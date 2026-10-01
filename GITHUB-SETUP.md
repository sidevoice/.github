# GitHub setup for the sidevoice organisation (decided with the operator, 2026-10-01)

Status: **to configure** — nothing applied yet. Items marked *(verify)* depend on plan features to confirm before relying on them.

## Organisation level (sidevoice)

| What | Setting | Why |
|---|---|---|
| Ruleset for every repo's default branch | Require a pull request; block force-push and deletion of `main` | No direct pushes; history safe |
| Same ruleset | Required status check **"PR title is a conventional commit"** | Mechanical gate for conventional commits |
| Same ruleset | Allowed merge method: **squash only** *(verify: merge-method rule in org rulesets / plan)* | One commit per PR, message = PR title. PRs in sidevoice are OPENED with the operator's minimal token (pull requests only), so the squash commit is authored by the operator; the bot pushes, comments and merges |
| Actions may open PRs | "Allow GitHub Actions to create and approve pull requests" ON (org or per repo) — release-please cannot open its release PR otherwise | Found by the CI worker, 2026-10-01 |
| Actions billing | Spending limit sized for macOS jobs until the repos are public (public repos: standard runners free) | 2026-09-30 the free 2000 min ran out (macOS ×10) |
| Members' e-mail privacy | "Keep my email addresses private" + "Block command line pushes that expose my email" on the operator's and the bot's accounts | Audit found a personal e-mail in a merge made with GitHub's button |
| Commit identity | The agent commits as the operator's account (name + GitHub noreply); Daimonbot only assigns issues | Attribution to the operator |

Org rulesets for private repos may need the Team plan *(verify)*; once the repos are public they apply on Free.

## Repository level (each module: core, desktop, web, connector, relay)

| What | Setting |
|---|---|
| Merge buttons | Allow squash merging only; default squash message = PR title + description |
| PR title check | Workflow on `pull_request` (`opened`, `edited`, `synchronize`) validating the title against Conventional Commits (e.g. `amannn/action-semantic-pull-request`), named exactly as the required check |
| Local hook (convenience, not a gate) | `commit-msg` hook validating conventional commits (`pre-commit` / `lefthook`), documented in AGENTS.md |
| release-please | `release-please-action` on push to `main` + `release-please-config.json` / `.release-please-manifest.json`; release type per repo: core `python`, connector/web `node`, desktop `simple` or `rust` (bumps `tauri.conf.json` + `Cargo.toml` via extra-files) |
| Release workflow | On the release created by release-please (tag `vX.Y.Z`): build and attach assets — core: wheel + `models-catalog.json` + vectors; desktop: `.dmg`, Windows installer, `.deb`/`.AppImage`, `SHA256SUMS`; connector: `npm publish`; web: static bundle tarball + SHA-256 |
| CI trimmed | PRs: lint + unit tests on Linux; desktop's Apple-Silicon engine test only when engine/bridge/catalogue paths change; installers only on `main` / release / manual; `concurrency: cancel-in-progress` |

## The release flow (what each act means)

1. **PR** (opened with the operator's PR-only token) → fast checks + PR-title check. Squash-merged.
2. **Merge to `main`** → integrated; installers built as test builds, nothing versioned published (the green build replaces `nightly`, below). release-please updates the open "release X.Y.Z" PR (version from `feat`/`fix`, changelog from PR titles).
3. **Release = merging the release PR** (the operator's act). It tags, creates the GitHub Release (notes = that version's changelog section) and triggers the release workflow. Edit the changelog in the release PR right before merging (a later merge to `main` regenerates it); notes can be fixed on the Release afterwards.
4. **Nightly** → one fixed rolling pre-release per repo, tag `nightly`: every push to `main` whose CI passes moves the tag to that commit and replaces all its assets (core: wheel + catalogue + vectors; desktop: `.dmg`, Windows installer, `.deb`/`.AppImage`, `SHA256SUMS`). Pre-release, never latest; notes give the commit SHA and date and say it is not a versioned release; release-please ignores the tag. Actions artifacts are kept 7 days, for debugging only. (Container images on GHCR tagged `main`/`sha`: later, for web/relay.)
5. Versions are per module. Core on PyPI later: sidevoice/sidevoice-core#4.

Related: rubasace/sidevoice#118 (releases for every module), #115.
