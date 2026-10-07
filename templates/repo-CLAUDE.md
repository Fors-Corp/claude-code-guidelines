# <Project> — CLAUDE.md

<!-- Target: ≤ 100 lines. Global rules live in ~/.claude/CLAUDE.md and are not repeated here.
     Cross-tool rules (other coding agents) live in AGENTS.md; this file adds only what is
     Claude-specific. Every rule below names the incident or measurement that created it. -->

Follow **AGENTS.md**. Architecture: `docs/architecture.md`. Plan and status: `docs/ROADMAP.md`
(source of truth on resume — not conversation memory). ADRs: `docs/adr/`.

## Non-negotiables

1. <The one invariant that, if broken, is a data-loss or privacy incident. Name its owner module.>
2. <The egress rule: which single file may do network I/O.>
3. <The locale list and where strings live.>
4. <What a click/drag/scroll must never be mistaken for; what silence means in this domain.>
5. <Anything a dependency bump may never change here.>

## Gate (the only definition of "correct")

```bash
<one command: format-check && lint && typecheck && build && test — identical to CI>
```

CI required checks as of <date>: `<list>`. Read the live list with
`gh api repos/<o>/<r>/branches/main/protection/required_status_checks` rather than trusting this line.
Merge method here: <rebase | squash | merge-commit> (`gh api repos/<o>/<r>` confirms).
Release: <changesets | manual bump>; tags `vX.Y.Z`; <who pushes tags>.

## Code navigation

Indexes present: <none | which>. <If a structural index and a call-graph tool both exist: the
index for API/occurrences/callers, the call graph for flows and blast radius.>
Run from a worktree; the main checkout may be in use by another session.

## Where to edit

| Need | Place | Not |
|---|---|---|
| <a new UI string> | `src/i18n.ts` (all locales) | component files |
| <a new component> | `<design system>` if generic | app-local copy |
| <a derived value> | `<owner module>` | re-derived in views |

## Out of scope unless asked

- <framework majors, new providers, schema changes, settings UI, …>
- <services never to restart / deploys never to trigger from a session>

## Before you finish

- [ ] Gate ran; command and output quoted in the reply.
- [ ] Verified on the real app/service (right port, real data volume), not only the harness.
- [ ] Every new string in every locale; axe clean; no raw hex.
- [ ] Regression test for every fix, in the same PR; negative case for every heuristic.
- [ ] Version + CHANGELOG bumped if behaviour changed; one version in every manifest.
- [ ] PR opened, CI monitor bound with auto-fix, auto-merge armed only if gates are green.
- [ ] This file updated if the session revealed a rule a future session would otherwise relearn.

## Decisions already made (do not re-litigate)

| Date | Decision | Why |
|---|---|---|
| <YYYY-MM-DD> | <…> | <measurement or incident> |
