# Lockfile Regeneration

General pattern: resolve the manifest file first (merge dependency entries from both sides by hand if it's also conflicted), then regenerate the lockfile from the resolved manifest rather than hand-merging lockfile conflict markers.

| Ecosystem | Manifest | Lockfile | Regenerate |
|---|---|---|---|
| npm | package.json | package-lock.json | resolve package.json, then `npm install` |
| Yarn | package.json | yarn.lock | resolve package.json, then `yarn install` |
| pnpm | package.json | pnpm-lock.yaml | resolve package.json, then `pnpm install` |
| Cargo | Cargo.toml | Cargo.lock | resolve Cargo.toml, then `cargo build` (Cargo rewrites the lockfile to match) |
| Bundler | Gemfile | Gemfile.lock | resolve Gemfile, then `bundle install` |
| Poetry | pyproject.toml | poetry.lock | resolve pyproject.toml, then `poetry lock` |
| Go modules | go.mod | go.sum | resolve go.mod, then `go mod tidy` |
| Composer | composer.json | composer.lock | resolve composer.json, then `composer update --lock` (updates the lock hash without bumping dependency versions) |

Verify the exact command against the project's actual package manager version before running — flags and defaults can change between major versions.

## Conflict classification edge cases

- **Composable, non-conflicting edits that look like a logic conflict** — e.g. one side renamed a variable, the other added a line using the old name in the same hunk. Check whether the two changes can be composed (apply the rename, then add the line) before declaring it a true logic conflict.
- **Rebase swaps ours/theirs** — during a rebase, "ours" is the branch being replayed onto (typically main) and "theirs" is the commit being replayed (the feature branch commit) — the opposite of a merge. Confirm which side is which with `git log` before trusting any `--ours`/`--theirs` shortcut.
- **Conflicted file with no `<<<<<<<` markers** — `git diff --diff-filter=U` can list a file as conflicted due to a delete/modify or rename conflict rather than a text conflict. Handle these with `git rm` or `git add` based on the intended resolution, not as a text-merge case.
- **Binary files** — never attempt a text merge; confirm with the user which version to keep (`git checkout --ours/--theirs -- <file>`).

## Tip: git rerere

For feature branches that sync with main repeatedly, `git config rerere.enabled true` makes git remember and automatically replay resolutions it has already seen for identical conflict hunks, cutting down repeat manual work across syncs.
