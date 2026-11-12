# ecom-ux

A canon of e-commerce UX/UI rules plus two agent skills that apply them. Read `DESIGN.md` before
changing anything about canon authority or what is published; it is the agreed design record and
it names what was already rejected.

## Agent skills

### Issue tracker

Issues and specs live as GitHub issues in this repo, driven with the `gh` CLI. See
`docs/agents/issue-tracker.md`.

### Triage labels

The five canonical triage roles, label strings equal to their names. See
`docs/agents/triage-labels.md`.

### Domain docs

Single-context: `GLOSSARY.md`, `DESIGN.md` and `docs/adr/` at the repo root. See
`docs/agents/domain.md`.

## Working discipline

- One article = one extraction unit. Synthesis and de-duplication is a separate step per domain.
- Stop at ~60% context fill and hand off. `PROGRESS.md` carries state across sessions.
- `research/raw/` never enters the main session — pass paths, not contents.
- Only derived rules are published: no source prose, no screenshots (ADR-0002).
