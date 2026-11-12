# ecom-ux — design record

Decisions agreed with the user before any code was written. Each entry is a decision, not a
proposal. Rejected alternatives are listed only where they were seriously considered, so that
they are not rediscovered as "new ideas" later.

## Goal

Turn the UX/UI best-practice corpus at hardclient.com (43 articles, ~122k words, one author,
Russian) into a tool that makes AI coding agents (Claude Code, Codex) build e-commerce
interfaces correctly — at the spec stage, while writing code, and at review.

## Form

Two skills sharing one canon, packaged as a public MIT repo:

- `ecom-ux` — consultant. Model-invoked. Loads a short domain router, then the domain
  sub-index, then rule bodies.
- `ecom-ux-review` — reviewer. User-invoked only, fresh context. Receives selected rules and
  checkable artifacts, not the author's justifications.

Packaging follows `mattpocock/skills`: one `SKILL.md` per skill, no per-harness duplication,
`.claude-plugin/plugin.json` read by both harnesses (Codex falls back to `.claude-plugin/`),
`agents/openai.yaml` carrying `policy.allow_implicit_invocation` kept in sync with
`disable-model-invocation`. Reference material lives inside the owning skill folder; skills
never link across skill folders.

Rejected: one skill with modes via `argument-hint`. It is an argument hint, not a context or
permission boundary, and the reviewer needs a context with no build history in it.

## A rule

One file per rule. YAML head plus six sections.

```yaml
id: UX-CHECKOUT-014          # immutable, never reused, tombstones stay
title: Delivery cost and date visible before the payment step
platforms: [web]             # web | ios | android
tier: floor                  # floor | reflex | finish
check: [dom, judge]          # array: static | dom | judge
applies_to: [checkout, cart]
status: active               # active | superseded | retired
supersedes: null
confidence: high             # high | medium | opinion
counterevidence: []          # links to sources that contradict, if any
```

Sections: `Rule` (one imperative statement), `Why` (mechanism, not opinion), `How` (observable
behaviour; stack examples live in an adapter, not here), `Verify` (concrete check),
`Anti-pattern`, `Evidence` (source slug + item number + source date).

`tier: floor` is reserved for narrow invariants with explicit applicability. Anything
contested is `reflex` or `finish`. Floor rules cannot be waived.

## Source handling

The corpus is the primary source and the face of the tool, but not infallible canon.

- Every rule carries `confidence` and, where relevant, `counterevidence`.
- Floor candidates and every money-path rule (~20–40 in total) are checked against measured
  sources — Baymard, NN/g — before being promoted to floor.
- Conflicts between articles, or between an article and measured data, go into the rule's
  applicability condition, and are listed in `conflicts.md`. Never silently resolved.
- Paraphrase only. No verbatim text, no images published.
- `research/raw/` and downloaded images are git-ignored. Only derived rules are published.

Verified example of why this matters: `/ecommerce-cart` says a confirmation of adding to cart
should disappear on its own ("Пропадает само"), while NN/g's study of 49 stores documents
user errors when confirmation is too easy to miss. The same article's neighbouring items
require a cart link and a timing slow enough to read, so the conflict is narrow — but real.

## Review artifact

`ux-review.json` per reviewed target:

```json
{
  "canonVersion": "...",
  "target": {"path": "...", "commit": "...", "viewport": "...", "route": "..."},
  "results": [{"ruleId": "UX-CART-004", "status": "pass|fail|waived|unknown|untested|n/a",
               "evidence": "...", "waiverReason": "..."}]
}
```

`n/a` requires an applicability justification. `waived` is impossible for `floor`. Missing
browser capability produces `untested`, never `pass`.

## Validation

Before the corpus is expanded past the pilot:

1. One reference storefront, mutated in versioned ways; a hidden answer key; 10 violations,
   10 correct implementations, 10 edge cases. Two reviewers × three runs. Report precision,
   recall and coverage separately per tier and check class. No promotion to floor while the
   reviewer fails correct exceptions.
2. A delivery test: the same four tasks in both harnesses, including a foreign stack and a
   continuation after context compaction. Compare full index vs router. Record which rule IDs
   were actually read, token cost, and rule adherence.

15/15 caught gives a Wilson lower bound near 80% for recall — not enough to justify blocking.

## Working discipline

- One article = one extraction unit (a `research` run). Synthesis and de-duplication is a
  separate step per domain, because that is where the context cost actually sits.
- Stop at ~60% context fill and hand off. `PROGRESS.md` carries state across sessions.
- `research/raw/` never enters the main session.

## Open at the time of writing

The pilot scope is 20 rules across cart and checkout. Waves after the pilot: money path →
remaining web → mobile app.
