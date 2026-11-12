# ADR-0002: Publish derived rules, never source text or images

## Status
Accepted.

## Context
The repo is public from the first commit. The corpus is a third party's published work: about
122,000 words of prose plus hundreds of annotated screenshots in which much of the meaning
lives.

The working assumption was that paraphrasing rules carries no obligations, so attribution and
content handling did not matter. That holds for the methods and ideas — copyright protects
expression, not technique. It does not hold for two artifacts the plan quietly included in the
public tree:

- `research/raw/<slug>.md` — near-verbatim extracted article text, ~122k words.
- `research/images/` and the annotated screenshots — actual copies.

Excluding those from the shipped *package* is not the same as excluding them from the public
*repository*.

## Decision
- Only derived rules are published. No source prose, no screenshots, no OCR output.
- `research/raw/` and `research/images/` are git-ignored and exist only on the extracting
  machine.
- Each rule's `Evidence` field records the source slug, item number and source date — a
  pointer for traceability, not a copy.
- Rules are written in our own words. Short quoted phrases are not used at all; the
  formulation is ours.
- Attribution to the corpus author in the README is optional on legal grounds and is not
  claimed as a requirement. If the repo is later promoted publicly, add a provenance note
  naming the corpus as the source of the material.

## Consequences
Reproducing a rule from scratch requires re-fetching the source, since the raw text is not in
the repo. That is the intended trade: the canon must stand on its own wording.

The rule schema therefore carries more weight than a citation would — `Why` has to explain the
mechanism rather than gesture at an authority.

## Rejected alternatives
- **Publish raw text for traceability.** Makes the repo a mirror of someone else's site.
- **Ask the author for permission first.** Legitimate, but blocks work on an external
  dependency when no permission is actually needed for the derived form.
