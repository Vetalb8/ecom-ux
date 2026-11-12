# Glossary

Vocabulary this project uses precisely. Agents should use these terms, not synonyms.

## Canon

The collected set of rules. Not the articles: the articles are evidence.

## Rule

One atomic, checkable statement about an e-commerce interface, identified by an immutable ID
(`UX-CART-012`). The working unit of the canon. See `DESIGN.md` § A rule for the schema.

Rejected synonyms: guideline, best practice, recommendation. Those name what the source
articles contain; a **rule** is what we produce from them.

## Source item

One numbered claim inside a source article. A rule cites one or more source items as
`Evidence`. Rules are far fewer than source items; a rule may absorb many.

## Tier

How the reviewer treats a rule. `floor` — non-waivable invariant with narrow applicability;
`reflex` — strong default, waivable with a stated reason; `finish` — polish, waivable.

## Check class

How a rule can be verified: `static` (read source files), `dom` (inspect rendered output),
`judge` (a reviewer model reads evidence and decides). A rule usually needs more than one, so
`check` is an array.

## Review status

`pass` / `fail` / `waived` / `unknown` / `untested` / `n/a`. `unknown` means a check ran and
could not decide; `untested` means no check ran (e.g. no browser available). Neither is `pass`.

## Waiver

A recorded decision not to comply with a non-floor rule, naming evidence and a page-specific
reason. Floor rules cannot be waived.

## Domain

A group of rules by screen area — `cart`, `checkout`, `product`, `listing`, `nav`, `auth`.
Domains exist so the canon can be loaded a slice at a time.

## Router

The short file a skill loads first. It names the domains and the condition for reaching each.
Not the index: the index lists individual rules inside a domain.

## Adapter

Stack-specific implementation guidance (e.g. Next.js/Tailwind/shadcn) kept out of the rule
body so that the rule itself stays stack-agnostic.

## Counterevidence

A cited source that contradicts or narrows a rule. Its presence is normal, not a defect.
