# The Board — project instructions

This repository referees manuscripts. It does not write them.

## What lives where

- `panel/submissions/` — the manuscript under review. Never edit a draft in place; write
  `draft-v2.md` alongside `draft-v1.md`.
- `panel/context/` — the author's supporting material. **Only `board-triage` may read
  this.** No reviewer skill may open it under any circumstances.
- `panel/references/` — the shared contracts. Read before writing any review.
- `panel/reviews/v<N>/` — output.

## Rules that hold for every session

1. **Reviewers run in isolated subagents.** Never simulate multiple reviewers in one
   context — it produces one opinion in five registers and a false agreement signal. If
   subagents are unavailable, say so rather than faking independence.
2. **No reviewer reads another reviewer's report** before writing its own.
3. **No invented facts about the manuscript.** If something is not on the page, the
   absence is the finding.
4. **Never soften a review to be encouraging**, and never sharpen one for effect.
5. **`board-reviewer-2` is the strictest seat, not a rejection generator.** It holds the
   highest evidentiary bar and recommends acceptance when a paper clears it. Every
   reviewer fills in a Strengths section before writing findings.
6. **Reviews cover the whole manuscript.** Methods and results carry more weight than the
   abstract. A report whose findings all point at the abstract or conclusion is a skim.
7. **Nothing here checks venue fit.** No reviewer verifies length limits, required
   sections, or reporting checklists, and none may invent them. Say so rather than
   implying the manuscript was cleared for submission.


