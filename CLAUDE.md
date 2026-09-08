# Fork conventions

This repository is a fork of `immich-app/immich`. Fixes are developed here and
mirrored to upstream by `.github/workflows/upstream-pr.yml`. Fork-only files
(this file and that workflow) must never appear in an upstream pull request.

## Branching

Base every feature branch on **upstream main**, never on this fork's `main`.
Fork `main` carries the fork-only files, so a branch cut from it would add them
to the upstream diff.

```sh
git fetch https://github.com/immich-app/immich main
git checkout -B <branch> FETCH_HEAD
```

If a session pre-created the branch from fork `main` and it has no commits of
its own yet, reset it with the commands above and push with `--force-with-lease`.

## Picking issues

Issues live upstream at `immich-app/immich`. Before starting one, confirm no
open upstream pull request already addresses it and nobody is assigned.

## Commits

Never include a Claude Code session URL in a commit message. In particular, do
not add a `Claude-Session:` trailer. A `Co-Authored-By:` trailer is fine.

## Pull requests

- Open the PR against this fork's `main`, using `.github/pull_request_template.md`.
- Never put a Claude Code session URL, or any other session link, in a PR title
  or body. The cloud harness appends a session-link footer when a PR is
  created, so immediately after creating a PR, read its body back and, if a
  footer was added, update the PR with the intended body. Updates do not get
  the footer re-appended.
- Before opening, verify every item in the template checklist and check every
  box. If an item cannot honestly be checked, fix that first rather than opening
  the PR with unchecked boxes. Items that do not apply to the change, such as
  the `src/services/` and `src/repositories/` rules for a web-only change, count
  as satisfied.
- Fill in the LLM-usage section truthfully.
- After opening, add exactly one `changelog:*` label. Upstream's label
  validation runs in this fork and fails without it.
- When the change is meant for upstream, also add the `upstream` label. The
  workflow opens the upstream PR, or syncs the title and body if one already
  exists, and comments the URL on the fork PR. Remove and re-add the label to
  sync again after editing the fork PR.
- Fork-only changes never get the `upstream` label.
