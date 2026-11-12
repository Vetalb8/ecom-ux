# Progress

State for picking this up in a new session. Read `DESIGN.md` first; it is the authority on
what was decided.

## Now

Repo scaffolded and published. Design record, glossary, ADRs, and tracker conventions are in
place. Nothing extracted yet.

## Done

- [x] Source corpus mapped: 43 articles, on-site, ~122k words, `hardclient.com`.
- [x] Two reference implementations studied for form: `nutlope/hallmark` (skill router,
      gates, linter, fresh-context reviewers) and `mattpocock/skills` (dual-harness packaging).
- [x] 36 design decisions agreed, then adversarially reviewed by Codex `gpt-6-astra`.
      Two were overturned: infallible canon (now ADR-0001) and attribution/publishing
      (now ADR-0002). Split into two skills, router-based loading, array `check`.
- [x] Repo skeleton, `DESIGN.md`, `GLOSSARY.md`, two ADRs, tracker + domain docs, `.gitignore`.

## Next

1. `/to-spec` — synthesise `DESIGN.md` into a spec in GitHub Issues.
2. `/to-tickets` — cut the spec into tickets: one per domain of the pilot, one per pump.
3. Pilot: extract cart + checkout, synthesise ~20 rules, build both skills, build the
   reference storefront, measure the reviewer.
4. Only then wave 1 (money path, remaining 12 articles).

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
