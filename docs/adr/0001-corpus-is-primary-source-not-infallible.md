# ADR-0001: The corpus is the primary source, not infallible canon

## Status
Accepted.

## Context
The plan originally treated the 43 hardclient.com articles as unquestionable canon: their
recommendations would feed rules directly, and where they disagreed with measured research the
research would simply not be consulted.

An adversarial review against primary sources found a concrete contradiction. The corpus's cart
article states a confirmation of "added to cart" should disappear on its own
("Пропадает само"), while NN/g's study of 49 stores documents user errors when confirmation is
too easy to miss. The same article's neighbouring items require a cart link and timing slow
enough to read, so the conflict is narrow rather than total — but it is real, and it was
invisible while the corpus held canonical status.

## Decision
The corpus remains the primary source and the face of the tool. It stops being infallible.

- Every rule carries `confidence` (`high | medium | opinion`) and, where relevant,
  `counterevidence`.
- Floor candidates and every money-path rule (roughly 20–40 in total) are checked against
  measured sources — Baymard, NN/g — before promotion to `tier: floor`.
- Divergence is recorded in the rule's applicability condition and listed in `conflicts.md`.
  Never silently resolved.
- `tier: floor` is reserved for narrow invariants with explicit applicability. A contested
  recommendation becomes `reflex`, however confidently the source states it.

## Consequences
Extraction is slower for the money path, and the canon is slightly smaller than a straight
transcription. In exchange a correct exception does not get a FAIL, which is the failure mode
that would make the reviewer unusable in one afternoon.

## Rejected alternatives
- **Verify everything against external research.** Multiplies extraction cost across 5,200
  source items for a corpus the user has already read and endorses.
- **Keep infallible canon, mark conflicts in prose only.** Prose is not shipped in the rule, so
  the reviewer would never see it.
