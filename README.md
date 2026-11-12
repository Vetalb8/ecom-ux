# ecom-ux

A canon of e-commerce UX/UI rules plus two agent skills that apply them — one while you build,
one that reviews what you built.

Built for Claude Code and Codex. Stack-agnostic; each rule describes observable behaviour, and
stack-specific recipes live in adapters.

## Status

Pre-pilot. The canon is being extracted from a 43-article corpus; see `DESIGN.md` for the
agreed design and `PROGRESS.md` for current state.

## Skills

| Skill | Invocation | Purpose |
| --- | --- | --- |
| `ecom-ux` | automatic | Consult the canon while specifying or building e-commerce UI |
| `ecom-ux-review` | explicit only | Review a target against the canon in a fresh context |

## Install

Not yet published. Planned, mirroring `mattpocock/skills`:

```bash
claude plugin install ecom-ux@ecom-ux
codex plugin marketplace add <owner>/ecom-ux
codex plugin add ecom-ux@ecom-ux
```

## Layout

```
DESIGN.md                  agreed design record
GLOSSARY.md                project vocabulary
docs/adr/                  decisions with real alternatives
skills/ecom-ux/            consultant skill: SKILL.md, references, scripts
skills/ecom-ux-review/     reviewer skill
research/raw/              extracted source text (git-ignored, never published)
research/notes/            structured per-article notes
demo/                      reference storefront used for validation
```

## Licence

MIT. Derived rules only; no source text or images are redistributed.
