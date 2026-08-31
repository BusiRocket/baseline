# TODO

Active backlog for the `baseline` repo. Closed items move to `TODO_LOG.md`.

States: `[ ]` pending - `[~]` partial or unverified - `[!]` blocked - `[x]`
verified complete - `[-]` obsolete or superseded.

## Estate

- [~] Bring the rest of the estate up to the wiring the conformance check
  asserts. 2026-08-28 sweep ran `--fix` + installs across 19 consumers: matrix
  went from 23-of-24 repos failing (~77 red cells) to ~39 red cells, 2 fully
  wired. The 2026-08-31 pass took it to **10 of 24 fully wired** and ~25 red
  cells outside the four excluded `staffbase-*` widgets, and the `pins` column
  is green estate-wide. All changes are left uncommitted in each repo, as the
  2026-08-28 sweep left its own, for a per-repo review. What remains:

  - Lockfile sync: **done 2026-08-31.** 12 repos were stale (brain-capture,
    busirocket, contratos, dj-rocket, inbox-companion, livesalescoach,
    Mains.World, nubenode-web, pxpn, verticagtm, vexa-mail, Calculadora); all 12
    now pass `pnpm install --frozen-lockfile`. The changes are left uncommitted
    in each repo, alongside the 2026-08-28 sweep's, for a per-repo review.
  - [!] `pnpm run prepare` in pxpn still fails, and will until 2026-09-01
    ~10:18Z. Not a wiring problem: pxpn enforces pnpm's `minimumReleaseAge`, and
    the three packages released today sit inside the 24-hour cutoff -
    `ERR_PNPM_MINIMUM_RELEASE_AGE_VIOLATION ... @busirocket/eslint-config@0.8.0 was published at 2026-08-31T09:54:54.000Z`.
    The install itself succeeds; it is the policy verification that rejects it.
    This applies to every consumer enforcing the policy, so hold the remaining
    `--fix` adoptions (the `vers` column: brain, intelifactu,
    pridefamilymedicine, rocket-agents, tieneslavibra, vexa,
    vexa-insight-dashboard) until the cutoff passes rather than adding per-repo
    exclusions to a supply-chain gate.
  - Action pins (`pins` column): **done 2026-08-31.** 54 tag pins across
    busirocket, contratos, dj-rocket, Mains.World and vexa now carry commit SHAs
    with the tag kept as a trailing comment. Two of them were never tags at all:
    `denoland/setup-deno@v2` and `dtolnay/rust-toolchain@stable` are moving
    _branches_, so `git/ref/tags/<tag>` 404s and they have to be resolved
    through `git/ref/heads/<name>`. `actionlint` is clean in all five.
  - Coverage (`cov` column): **done in 8 repos 2026-08-31**, and it was not
    `--fix` material - `create-baseline --fix` reports "nothing was mechanically
    fixable" when the config has no `coverage:` key at all, which was the case
    everywhere. The block was added by hand (provider v8, `autoUpdate: true`,
    every floor at 0) to brain-capture, busirocket, dj-rocket, inbox-companion,
    livesalescoach, nubenode-web, tieneslavibra and verticagtm; the first run
    then ratcheted each floor to what the suite actually reaches (38.39 in
    livesalescoach, 89.79 in busirocket). Two remain: Mains.World has no `test`
    block in `vite.config.ts` at all, and pxpn's install is held by the
    release-age quarantine above.
  - [!] **8 repos' `test` script was broken and nobody noticed**: brain-capture,
    busirocket, dj-rocket, inbox-companion, livesalescoach, nubenode-web, pxpn
    and verticagtm all run `vitest run --coverage` without depending on
    `@vitest/coverage-v8`, so the script died on
    `MISSING DEPENDENCY  Cannot find dependency '@vitest/coverage-v8'` before
    running a single test. It predates this session - reproducible with the
    coverage config reverted. Fixed by adding the dependency in seven of them,
    all now green (55, 91, 79, 15, 27, 1027 and 142 test files). pxpn is the
    eighth and waits on the quarantine. Worth a conformance rule: a `test`
    script that passes `--coverage` should assert the provider is a dependency.
  - Coverage, still open: vexa and vexa-insight-dashboard have no `test` script
    at all.
  - CI wiring (`gates`): pxpn and pridefamilymedicine CI reaches no `check:*`
    entrypoint, so six gates sit dead; wiring the workflow is a human call.
  - intelifactu: hooks run through husky (`.husky/pre-commit`,
    `prepare: husky`); migrating to lefthook is a decision, WARN left standing.
  - The four `staffbase-*` widgets: untouched, as excluded - they predate
    `@busirocket/quality-config` entirely; all nine baseline packages missing. A
    real migration, not `--fix` material.
