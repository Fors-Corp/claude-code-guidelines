# Claude Code Guidelines

A consolidated, dated set of standing rules for working with [Claude Code](https://docs.anthropic.com/en/docs/claude-code) — the kind of file you drop into `~/.claude/CLAUDE.md` so every session starts with the same discipline instead of relearning it.

It was not written from first principles. It was **mined from practice**: ~25 real project `CLAUDE.md`/`AGENTS.md` files and ~60 session-memory entries from six weeks of shipping with Claude Code as the primary engineer — every rule here was either repeated across several repos or paid for by a concrete incident. Rules carry the date they were decided or the postmortem that created them, so a future session can resolve a conflict by recency instead of asking.

## What's inside

| File | Purpose |
|---|---|
| [`CLAUDE.md`](CLAUDE.md) | The global rule set. Goes to `~/.claude/CLAUDE.md` — see [Install with one prompt](#install-with-one-prompt). |
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

## Install with one prompt

Paste this into Claude Code, from any directory:

```text
Install the Claude Code guidelines from https://github.com/Fors-Corp/claude-code-guidelines :
1. Fetch https://raw.githubusercontent.com/Fors-Corp/claude-code-guidelines/main/CLAUDE.md
   and https://raw.githubusercontent.com/Fors-Corp/claude-code-guidelines/main/templates/repo-CLAUDE.md
2. If ~/.claude/CLAUDE.md does not exist, write the first file there. If it does, back it up
   beside itself as CLAUDE.md.bak-<YYYYMMDD-HHMMSS>, then merge: keep every rule I already
   have, add the sections and rules I am missing, and list every place where my existing
   rules and the new ones contradict each other so I can decide.
3. Save the template to ~/.claude/repo-CLAUDE-template.md.
4. For each <placeholder> left in ~/.claude/CLAUDE.md, ask me for the value — one question
   each, with a recommended default.
5. Show me the final diff against the backup before you finish. Do not touch any other file.
```

The rules take effect in the next session (`CLAUDE.md` is read at startup). Expect roughly
3.5k tokens of context per session for the full file; trim sections you don't need.

### Or by hand

```bash
git clone https://github.com/Fors-Corp/claude-code-guidelines.git
cp claude-code-guidelines/CLAUDE.md ~/.claude/CLAUDE.md
cp claude-code-guidelines/templates/repo-CLAUDE.md ~/.claude/repo-CLAUDE-template.md
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
