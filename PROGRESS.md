# Progress

State for picking this up in a new session. Read `DESIGN.md` first; it is the authority on
what was decided.

## Now

Spec and tickets are published. Nothing extracted, no code yet. Pick a ticket from the frontier
below and work it in a fresh session — each ticket is self-contained.

- Spec: issue #1, "canon, consultant skill and reviewer skill (pilot scope)".
- Tickets: #2–#21, all sub-issues of #1, all labelled `ready-for-agent`.

### Frontier — tickets with no open blocker

| Ticket | Issue | What it is |
| --- | --- | --- |
| 01 | #2 | Canon tracer bullet: one rule reviewed end to end |
| 06 | #7 | Extraction: cart article to source-item notes |
| 07 | #8 | Extraction: card payment form article to source-item notes |
| 08 | #9 | Extraction: checkout address and time article to source-item notes |

**Prerequisite not covered by any ticket:** the three pilot articles have not been fetched.
`research/raw/` does not exist yet. Tickets 06/07/08 each fetch their own article as a first
step; ticket 01 needs one extracted source item before it can satisfy its evidence criterion.

Everything else is blocked. The graph lives in GitHub issue dependencies, not in this file —
do not copy it here, it will drift.

### Driver order

1. 01 (#2) is on the critical path: 16 of 20 tickets are blocked behind it.
2. 06/07/08 (#7–#9) are the long tail and start in parallel with 01.
3. 05 (#6) needs both the storefront chain and the checkout canon; it is the last storefront
   ticket to unblock, not the first to start.

## Done

- [x] Source corpus mapped: 43 articles, on-site, ~122k words, `hardclient.com`.
- [x] Two reference implementations studied for form: `nutlope/hallmark` (skill router,
      gates, linter, fresh-context reviewers) and `mattpocock/skills` (dual-harness packaging).
- [x] 36 design decisions agreed, then adversarially reviewed by Codex `gpt-6-astra`.
      Two were overturned: infallible canon (now ADR-0001) and attribution/publishing
      (now ADR-0002). Split into two skills, router-based loading, array `check`.
- [x] Repo skeleton, `DESIGN.md`, `GLOSSARY.md`, two ADRs, tracker + domain docs, `.gitignore`.
- [x] `/to-spec` — `DESIGN.md` synthesised into spec issue #1.
- [x] `/to-tickets` — spec cut into 20 tickets, #2–#21. Breakdown reviewed by Codex
      `gpt-6-astra` at medium effort; the first cut of 15 was sent back for rework, and the
      published set reflects the corrections (storefront screens split out, the 20-rule pilot
      made an acceptance criterion, the delivery eval made decidable).

## Next

Work the frontier. Nothing in this file sequences the work; the dependency graph is the source
of truth, and it is on GitHub, not here.

Pilot in one line: fetch the three articles, extract, synthesise ~20 rules across `cart` and
`checkout`, build both skills, build the reference storefront, measure the reviewer. Only after
that, wave 1 (money path, remaining 12 articles) — and only if the delivery eval in ticket 20
passes.

## Pilot scope

20 rules across `cart` and `checkout`. Floor candidates and money-path rules get checked
against Baymard and NN/g before promotion.

Source articles for the pilot:

- `https://hardclient.com/ecommerce-cart` (203 guidelines) — **conflict found**, see ADR-0001.
- `https://hardclient.com/ecommerce-credit-card-form` (129).
- `https://hardclient.com/ecommerce-checkout-address-and-time` (167).

## Context budget

Stop at ~60% context fill. One article = one `research` run. `research/raw/` is git-ignored and
must not enter the main session — pass paths, not contents.
