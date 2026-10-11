# Changelog

All notable changes to these guidelines are documented here. The format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and the versioning follows
[Semantic Versioning](https://semver.org/spec/v2.0.0.html): a rule change that breaks an
existing habit (reverses or removes a rule) is a MAJOR; a new rule is a MINOR; a wording or
provenance fix is a PATCH.

## [1.0.1] — 2026-10-11

### Added

- README "Install with one prompt": a prompt to paste into Claude Code that installs the
  rules, or merges them into an existing `~/.claude/CLAUDE.md` with a backup and a list of
  contradictions, then asks for each placeholder value.

## [1.0.0] — 2026-10-08

### Added

- Global rule set `CLAUDE.md`, consolidated 2026-10-07 from ~25 repository
  `CLAUDE.md`/`AGENTS.md` files and ~60 session memories: session start, context and test
  economy, agents and workflows, git/releases/PRs, security and automation hygiene, what
  correct code looks like, product baseline, definition of done, rule maintenance.
- Per-repository template `templates/repo-CLAUDE.md`.
- README explaining the floor/add-only principle and the dated, incident-backed rule style.

[1.0.1]: https://github.com/Fors-Corp/claude-code-guidelines/compare/v1.0.0...v1.0.1
[1.0.0]: https://github.com/Fors-Corp/claude-code-guidelines/releases/tag/v1.0.0
