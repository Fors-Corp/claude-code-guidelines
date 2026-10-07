# Claude Code Guidelines

A consolidated, dated set of standing rules for working with [Claude Code](https://docs.anthropic.com/en/docs/claude-code) — the kind of file you drop into `~/.claude/CLAUDE.md` so every session starts with the same discipline instead of relearning it.

It was not written from first principles. It was **mined from practice**: ~25 real project `CLAUDE.md`/`AGENTS.md` files and ~60 session-memory entries from six weeks of shipping with Claude Code as the primary engineer — every rule here was either repeated across several repos or paid for by a concrete incident. Rules carry the date they were decided or the postmortem that created them, so a future session can resolve a conflict by recency instead of asking.

## What's inside

| File | Purpose |
|---|---|
| [`CLAUDE.md`](CLAUDE.md) | The global rule set. Copy to `~/.claude/CLAUDE.md`. |
| [`templates/repo-CLAUDE.md`](templates/repo-CLAUDE.md) | Per-repository template: ≤ 100 lines, non-negotiables, the gate command, a where-to-edit table, a before-you-finish checklist. |
| [`CHANGELOG.md`](CHANGELOG.md) | Versioned history of the rules (SemVer — a rule change that breaks an existing habit is a major). |

## The shape of it

1. **Session start** — fetch before planning, detect a shared checkout, check open PRs, verify git identity, know which hooks you'll meet.
2. **Context and test economy** — structure before source (code indexes before `grep`/`Read`), read only what you edit, own tests while iterating and the full gate once.
3. **Agents and workflows** — size the model per stage and say why; producer + independent verifier, prefer a deterministic oracle; every subagent prompt opens with a "settled" preamble; guard against placeholder results.
4. **Git, releases and PRs** — atomic Conventional Commits, SemVer + CHANGELOG in the same change, the repo's own merge method, auto-fix and auto-merge by default, never poll CI yourself, autonomy until told to stop.
5. **Security and automation hygiene** — dependency and code-scanning fixes pre-authorized; fix the cause never the signal; bounded effort; automation never edits its own controls; a check that cannot fail is not a gate.
6. **What correct code looks like** — KISS, no frozen stand-ins, unknown is a state, fail loud over fallback, one owner per invariant, append-only persisted data, a negative case for every heuristic.
7. **Product baseline** — privacy by default, humane tone, every string in every locale, WCAG AA with axe, tokens never raw hex.
8. **Definition of done** — run the real gate and quote it, verify on the real thing, report faithfully.
9. **Keeping the rules alive** — where a new rule goes, and when it gets promoted from one repo to global.

Two structural principles do most of the work:

- **The global file is a floor.** A repo's own `CLAUDE.md`/`AGENTS.md` may *add* rules; it may not subtract from the core sections. That is what stops two repos from drifting into contradictory copies of the same rule.
- **Every rule is dated or incident-backed.** "Never pipe the index tool through `head`" is a preference; "never pipe it through `head` — it truncated the one caller that mattered on 2026-09-16" is a rule a session will keep.

## Adopt it

```bash
git clone https://github.com/Fors-Corp/claude-code-guidelines.git
cp claude-code-guidelines/CLAUDE.md ~/.claude/CLAUDE.md
```

Then search the file for `<` — the handful of placeholders (`<your-publishing-email>`, `<your design system>`, the context-window figure) are the only lines that are specific to one setup. For each repository, start from `templates/repo-CLAUDE.md`; keep it under 100 lines and let it point at `docs/` rather than re-explain the code.

Some sections name tools from a particular environment — code indexes ([graft](https://github.com/trailhq/Graft), [CodeGraph](https://github.com/colbymchenry/codegraph)), the ECC GateGuard hook, the Claude Code desktop app's PR monitor. Where you don't run them, the rule still applies; swap the command.

## Contributing

Pull requests welcome, with three constraints that keep the file useful:

- **One statement per rule**, imperative, in the section that owns it.
- **Name the incident or measurement** that makes it a rule, with a date.
- **Don't add what the harness already enforces** (system prompt, hooks) or what a repo's own docs record.

## Origin and license

Written by [Marc Fors](https://marcfors.com) from his own Claude Code practice at Fors Corp; the consolidation itself was done by Claude Code analysing its own session history. MIT — see [LICENSE](LICENSE).
