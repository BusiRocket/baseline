# TODO

Active backlog for the `baseline` repo. Closed items move to `TODO_LOG.md`.

States: `[ ]` pending - `[~]` partial or unverified - `[!]` blocked - `[x]`
verified complete - `[-]` obsolete or superseded.

## Estate

- [~] Bring the rest of the estate up to the wiring the conformance check
  asserts. 2026-08-28 sweep ran `--fix` + installs across 19 consumers: matrix
  went from 23-of-24 repos failing (~77 red cells) to ~39 red cells, 2 fully
  wired (baseline, calculadora). What remains needs a per-repo decision, except
  the lockfiles, which the 2026-08-31 release unblocked:

  - Lockfile sync in 13 repos: unblocked as of 2026-08-31, the packages the
    lockfiles could not resolve are published. Re-run `pnpm install` per repo,
    plus `pnpm run prepare` in pxpn.
  - Action pins (`pins` column): tag-pinned actions in busirocket, contratos,
    dj-rocket, Mains.World, vexa - repin to commit SHAs, per repo.
  - Coverage (`cov` column): vitest configs without a `coverage:` block the
    auto-fix can patch (brain-capture, busirocket, dj-rocket, inbox-companion,
    livesalescoach, Mains.World, nubenode-web, pxpn, tieneslavibra, verticagtm);
    vexa and vexa-insight-dashboard have no `test` script at all.
  - CI wiring (`gates`): pxpn and pridefamilymedicine CI reaches no `check:*`
    entrypoint, so six gates sit dead; wiring the workflow is a human call.
  - intelifactu: hooks run through husky (`.husky/pre-commit`,
    `prepare: husky`); migrating to lefthook is a decision, WARN left standing.
  - The four `staffbase-*` widgets: untouched, as excluded - they predate
    `@busirocket/quality-config` entirely; all nine baseline packages missing. A
    real migration, not `--fix` material.
