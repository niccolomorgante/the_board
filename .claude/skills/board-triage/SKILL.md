---
name: board-triage
description: Turn a panel of independent referee reports into a single prioritised revision plan — merging findings, resolving contradictions between reviewers with stated reasoning, protecting the word budget, separating fixes that need only rewriting from fixes that need data you do not have, and scaffolding a point-by-point response letter. Use after board-panel, whenever the user asks what to do about their reviews, or when real referee reports need reconciling into an action list. Triggers on "what do I fix first", "reconcile these reviews", "make a revision plan", "the reviewers contradict each other", "help me write the response to reviewers".
---

# Review triage

Several referees produced findings that overlap, contradict, and compete for the same
words. Your job is to turn that into one ordered plan the author can execute, and to be
explicit about every judgement call you made getting there.

You are not the author. You did not write this manuscript and you do not know facts about
it that are not in front of you. That constraint shapes everything below.

## Works on real reviews too

Note that the panel has three reviewers, so "two independent reviewers raised this" is a
majority, not a minority — weight it accordingly, and be slower to dismiss a finding only
one of three raised than you would be with a larger board.

This skill does not care whether the reports came from `board-panel` or from an actual
journal. If the user drops genuine referee reports into `panel/reviews/<round>/`, run the
same process on those — with one difference that matters: real reviewers are people with
standing, and a finding you judge wrong still has to be *answered* rather than dismissed.
Flag those as "rebut, don't fix" and draft the rebuttal.

## Before you start

Read:

1. Every file in `panel/reviews/<round>/`, including `panel-summary.md` if present.
2. The document under review, including its figures where a finding turns on one — you
   cannot adjudicate a disagreement about a figure from the reviewers' descriptions of it.
3. `panel/references/criteria.md`, for the scored elements and the 1–3 scale, and
   `panel/references/review-format.md`, for the finding structure you are merging.

You **may** read `panel/context/` — you are the only skill that can. Use it for exactly
one purpose: checking whether a finding marked `NEEDS EVIDENCE` is actually answerable
from material the author already has. If a reviewer says "no sensitivity analysis for the
discount rate" and the context folder has one sitting in a supplementary table, the
finding changes category from "cannot fix" to "cite the thing you already have", which is
the most useful move available to you.

Do not import content from `panel/context/` into the manuscript yourself. Point at it.

## Step 1 — Merge

Collapse findings that are the same finding in different words. Keep the sharpest
formulation and attribute every reviewer who raised it — the count matters, because a
finding three isolated readers reached independently outranks one that a single reader
felt strongly about.

## Step 2 — Resolve contradictions, showing your work

Where reviewers genuinely conflict, do not average them and do not default to the harsher
one. Write out:

- what each reviewer said,
- which of them was positioned to judge it (the practitioner's view on comprehension and
  on whether an effect is large enough to act on outranks the methodologist's; the
  reverse holds for technical soundness and novelty; Reviewer 2 holds the highest
  evidentiary bar by design, so check that each of its findings is anchored in quoted text
  before adopting the severity — where it is, take it at face value rather than discounting
  it, and where another reviewer reached the same finding independently, it is the
  strongest signal available),
- what you are recommending and why.

The reasoning is not decoration. The author needs to be able to overrule you, and they can
only do that if they can see the call you made.

Many apparent contradictions are two true observations about one defect. Look for that
reading before adjudicating.

## Step 3 — Sort by what the fix actually requires

Four buckets, and the split matters more than the ranking:

**TEXT** — fixable by rewriting what is there. Cutting, restructuring, defining a term,
making an implicit step explicit, softening a claim to match the evidence, moving a buried
result into the open, relabelling or rescaling a figure. You can do these — except the
figure itself, which is ANALYSIS if it has to be redrawn from data.

**ANALYSIS** — requires running something the authors could plausibly run: a sensitivity
analysis, a subgroup, a robustness check, a reformatted figure. You cannot do it, but it
is inside their control. Say what would have to be run and what it would settle.

**EVIDENCE** — requires data, permission, or access the authors do not have. You cannot do
these and must not paper over them with confident phrasing. State precisely what is needed
and what it would unlock.

**DECISION** — requires a choice only the authors can make: scope, framing, which claim to
retreat from, which venue, how much to concede. Present the options and the trade-off,
then stop.

Rank within buckets by impact on the recommendation per unit of effort. A claim in the
abstract that outruns its evidence is a fifteen-minute TEXT fix that can move a reviewer
from major revision to minor; a new analysis that answers a MINOR finding is not.

## Step 4 — Pay for every addition

Manuscripts are length-constrained, so treat new text as something that has to be funded.
If the author has told you a limit, hold them to it; no file on the panel records one.
For each addition you recommend, name the passage it comes out of, and check the panel
summary's "What held up" section before you propose the cut: material two reviewers praised
independently is the most expensive thing in the document to lose, and trading it away
to answer one reviewer's minor comment is a net loss that is easy to make and hard to
notice afterwards.

Describe the trade in sentences, not arithmetic. You cannot count words reliably and should
not pretend to — if the author needs a number, they should take it from their word
processor.

## Step 5 — Write the plan

`panel/reviews/<round>/revision-plan.md`:

```markdown
# Revision plan — round <N>

## Where this stands
The recommendation spread, and what an editor would most likely do with it.

## What this costs
Each proposed addition and the passage it is funded from.

## Do first — TEXT
For each: finding, raised by, the specific change, words in/out.

## Needs running — ANALYSIS
For each: what to run, what it settles, which findings it closes.

## Blocked — EVIDENCE
For each: what is missing, what it unlocks, where it might come from.

## Your call — DECISION
For each: the options, the trade-off, the recommendation and its reasoning.

## Rebut, don't fix
Findings you judge wrong or not worth conceding, with the argument the authors
would make. Every one still needs answering in the response letter.

## Contradictions resolved
Reviewer A said X, reviewer B said Y, recommending Z because …

## Deliberately not doing
Findings you judged not worth the words, with the reason. An author who implements
every finding a harsh panel produced ends up with a manuscript written by committee,
which reads exactly like one.
```

## Step 6 — Draft the response letter

If asked, write `panel/reviews/<round>/response-to-reviewers.md`: one numbered entry per
finding, in the reviewers' own numbering, each with the comment, the action taken, and
where in the revised manuscript to find it.

Three rules that make the difference between a letter that works and one that irritates:

- **Answer every comment, including the ones you rejected.** An unanswered comment reads
  as evasion and editors check for it.
- **Concede clearly or disagree clearly.** "We have clarified this" for something you did
  not change is the single most common way to lose a referee who was on your side.
- **Quote the changed text.** Editors do not want to hunt through a revised manuscript,
  and referees who cannot find your change assume you did not make it.

Leave `[TO CONFIRM: …]` markers wherever the response depends on an ANALYSIS or EVIDENCE
item that has not actually been done yet. A response letter that claims a fix which has
not been made is a much worse problem than a visibly incomplete one.

## Step 7 — Optionally produce the next draft

If the user asks for revised text, apply **only the TEXT bucket** and write
`panel/submissions/draft-v<N+1>.md`. Never edit a draft in place — round-2 findings are
only interpretable against the exact text round 1 saw.

For every ANALYSIS or EVIDENCE item, leave an inline marker rather than smoothing over the
gap:

```
[NEEDS: sensitivity analysis on the discount rate — F7, methods]
```

A gap you cannot fill is a gap. Writing around it produces a fluent manuscript with a hole
in it, which is worse than an obviously incomplete draft, because the author stops seeing
the hole and the referee does not.
