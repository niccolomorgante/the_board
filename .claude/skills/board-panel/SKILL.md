---
name: board-panel
description: Run a full independent referee panel over a manuscript or report — three reviewers (methodologist, practitioner, reviewer-2) dispatched as parallel subagents in isolated contexts, then synthesised into a panel summary with recommendation spread, score matrix, independent agreement, and disagreement. Use whenever the user wants a document reviewed, critiqued, stress-tested, or run past a mock referee panel before submitting it. Triggers on "review this", "run the panel", "what would reviewers say", "tear this apart before I submit", or any request for multi-perspective critique of a paper, manuscript, or report.
---

# Review panel

Dispatch independent referees over one document, wait for all of them, then synthesise.
The synthesis is the deliverable — separate opinions are raw material, and the value is
in where they converged without conferring and where they split.

## Step 1 — The panel

Three reviewers, all of them every time:

| Persona | Skill | Report |
|---|---|---|
| Methodologist | `board-methodologist` | `methodologist.md` |
| Practitioner | `board-practitioner` | `practitioner.md` |
| Reviewer 2 | `board-reviewer-2` | `reviewer-2.md` |

**Retarget the practitioner** before dispatching. It defaults to clinician-shaped. If the
document lands in policy, payer, industry, education, or software, say so in its dispatch
prompt — a clinician reading an HTA submission produces plausible findings about the wrong
world.

**What this panel does not cover.** No reviewer checks journal formatting, word limits,
structured-abstract compliance, or submission requirements. Say this once, up front, so
the user knows it is an untested gap rather than a clean bill.

**Three is a small board.** Two reviewers agreeing is a two-thirds majority, not a
coincidence of outliers, and one reviewer raising something alone is weaker evidence than
it would be on a board of five. Carry that into the synthesis rather than reading
convergence the way you would from a larger panel.

## Step 2 — Check the references, then the submission

The three reviewers all read `panel/references/criteria.md` and
`panel/references/review-format.md`. If either is missing, stop and say so — reviewers
without them invent their own scoring and structure, and the reports will not merge.

Note which rows `criteria.md` currently defines. The score matrix in step 4 uses those
rows, whatever they are; do not carry forward a row list from a previous run.

Then find the document. Default to the newest `draft-v*.md` in `panel/submissions/`. If
there is more than one candidate, or the user named a file, use theirs.

If `panel/submissions/` is empty, the document is somewhere else. Ask for it and convert it
per `panel/references/document-format.md`.

**Check the figures before dispatching.** The reviewers are told to open the images that
`[FIGURE n: ...]` placeholders point at. Confirm the paths resolve. A broken path degrades
silently into a caption-only read, and you will not be able to tell from the reports that
it happened.

If the user has told you a length limit and the draft is visibly far past it, say so before
dispatching — reviewers will otherwise spend findings on text that has to be cut anyway.
Estimate only; do not report a word count as though it were measured, and point the user
at their word processor for the real number. An over-length draft is not a reason to
refuse; reviewing one is a normal thing to want.

Determine the round: `v1` for a first pass, or match the draft's version number.

## Step 3 — Dispatch everyone in the same turn

Launch all three subagents **in one turn**, not sequentially. Each gets the skill path and
the document path and nothing else:

```
Execute this review:
- Skill: .claude/skills/<skill-name>/SKILL.md
- Document: panel/submissions/draft-v<N>.md
- Round: v<N>
- Write your report to: panel/reviews/v<N>/<report-name>
- Do not read any other file in panel/reviews/. Do not read panel/context/.
```

Use the skill names and report names from the table in step 1 — guessing the path fails
silently.

**Why separate contexts, and not one agent adopting three stances.** Overlap between the
reports is the output this pipeline exists to produce, and overlap only carries information
if the readers were sealed off from each other. A single agent asked to review from three
angles returns three paraphrases of one underlying judgement; the agreement you then observe
was manufactured by the prompt, not discovered in the manuscript. That is worse than
running one reviewer honestly, because a fabricated convergence signal is
indistinguishable from a real one and the author will act on it.

If subagents are unavailable, say so plainly and offer the sequential fallback — but tell
the user what it costs: the agreement signal, the most valuable output of the pipeline,
becomes unreliable.

Wait for all three. Do not begin synthesising on partial returns.

## Step 4 — Synthesise

Read every report. Write `panel/reviews/v<N>/panel-summary.md`:

```markdown
# Panel summary — <manuscript>, round <N>

**Panel:** methodologist, practitioner (retargeted to <field>, or clinician default),
reviewer 2. Note here whether every reviewer could see the figures.

## Recommendations
| Reviewer | Recommendation | One-line reason |
|---|---|---|

An editor faced with this spread would do what? Say it in one sentence. Two majors
and a reject is a different letter from three minors, and the authors need to know
which one they are looking at.

## Did they read the same paper?
Put the reviewers' "Summary of the manuscript" sections side by side. Where they
diverge on what the paper even claims, that is a framing defect no single finding
will surface, and it outranks everything below. Where they agree, say so and move on.

## What held up
Strengths named by more than one reviewer. Protect these — they are the parts of the
manuscript that survived independent scrutiny, and they are the first thing a revision
accidentally destroys. If no reviewer named a strength, say so; that is a finding
about the paper, or about a reviewer who decided early.

## Score matrix
| Element | Meth | Prac | R2 | Spread |
|---|---|---|---|---|

Rows are the scored elements in `criteria.md`, in its order. Scores run 1–3, so the
maximum spread is 2 — and a spread of 2 is the most interesting number in this
document. Say what it means. Note which reviewer was positioned to judge each row:
a Methods row scored low by the practitioner and high by the methodologist is not
a disagreement about the analysis, it is a reporting problem.

## Independent agreement
Findings raised by two or more reviewers who could not see each other's work,
ordered by how many converged. Highest-confidence signal the pipeline produces — an
applied reader and an in-field expert arriving separately at the same objection
means it is in the text, not in the reader.

## Disagreements, and what they reveal
For each clash: who said what, and — more useful — what has to be true about the
manuscript for both to be right. Usually something is. "The practitioner could not
follow the central claim and the methodologist called it well-specified" does not
mean one is wrong; it means the claim is precise and inaccessible, a specific fixable
defect neither reviewer could name alone.

## Findings that would block publication
MAJOR findings where a reviewer said revision cannot fix it — a different paper, a
different analysis, or a different venue. Quote the finding and that sentence, verbatim,
attributed. If there are any, say plainly whether this is a revision problem or a
different-paper problem.

## What nobody could judge
Merged "What I could not judge" sections. Read this for gaps in panel coverage — if
no reviewer was positioned to evaluate something central, the panel has not tested
it, and silence is not approval. With three reviewers this section is longer than it
would be on a real board; do not let it pass unremarked.

## Confidential comments, merged
The editor-facing sections, collected. This is where the reviewers said what they
would not say to the authors, and it is usually the most useful page here.

## Top five priorities
Ranked. For each: the finding, who raised it, and whether fixing it needs new
evidence or only new text.
```

## Step 5 — Report back

Summarise in chat: the recommendation spread, whether the reviewers read the same paper,
the strongest agreement, the most revealing clash, and whether anything is fatal. Point at
the summary file. Then suggest `board-triage`.

Do not soften the synthesis to be encouraging, and do not sharpen it for effect. If the
reviewers came back positive, say so — a panel that never returns a good verdict is a broken
instrument, not a rigorous one.

Read the spread with the panel's design in mind. `board-reviewer-2` holds the highest
evidentiary bar by construction, so its recommendation sitting a grade below the others is
the expected pattern and means little on its own. What matters is when another reviewer
lands as low as reviewer 2 does, or when reviewer 2 lands as high as the others. Both are
strong signals and should be called out explicitly. Reviewer 2 is not a rejection
generator: if it recommends acceptance, that is the strongest positive result this panel
can produce, and the summary should say so plainly rather than treating it as an
anomaly.

## Rounds

Watch the composition of the findings across rounds. Early rounds turn up things that
rewriting fixes; later rounds increasingly turn up things that need data or analysis the
author does not have. Once that second category dominates, further rounds change the
manuscript without improving it, and the honest thing is to say the panel has given what it
can. In practice this is round two or three.

Before submitting, remind the user that venue fit is untested by this panel: length limits,
required sections, reporting checklists, and submission format have not been checked by
anyone here, and they are the cheapest possible reason to be desk-rejected.
