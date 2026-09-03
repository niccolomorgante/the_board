# Review format

Every reviewer writes to this exact structure. The panel synthesiser and the triage skill
both parse it, so deviating breaks them. Keep the headings verbatim.

Write to `panel/reviews/<round>/<reviewer>.md`.

---

```markdown
# <Reviewer name> report — <manuscript title>, round <N>

**Reviewer:** <persona slug>
**Document reviewed:** <path>
**Figures:** viewed / not viewable in this session
**Date:** <YYYY-MM-DD>

## Recommendation

One of: ACCEPT / MINOR REVISION / MAJOR REVISION / REJECT

Then one paragraph, maximum six sentences: the recommendation, and the reason it is that
rather than the grade above or below it.

## Summary of the manuscript

Three to five sentences, in your own words, stating what the paper set out to do, what it
did, and what it found. Write this from the whole manuscript, not from the abstract.

This section is not a courtesy. It is the highest-signal diagnostic in the report: if
several reviewers who never spoke summarise the paper differently, the authors have a
framing problem that no individual finding will surface.

## Strengths

Two to four specific things the paper does well, each anchored to where it happens. Not
generic praise — "the sensitivity analysis in section 3.4 anticipates the obvious
objection" is useful; "well written" is not.

Write this before the findings, and mean it. Strengths do three jobs: they tell the
triage step what to protect when it starts cutting, they tell the authors which parts not
to touch, and they keep your recommendation calibrated. A report with no strengths section
is usually a reviewer who decided early.

## Scores

| Element | Score (1–3) | One-line reason |
|---|---|---|
| <criterion from criteria.md, in its order> | | |

Use every row in `criteria.md`, in its order, even the ones outside your remit — score
those `n/a` and say why in the reason column. A blank row and a row nobody could judge look
identical to the synthesiser.

3 is no objection, 2 is a named weakness fixable in revision, 1 is a weakness revision
alone does not fix. **Every 1 or 2 must correspond to at least one numbered finding
below.** A low score with no finding attached is not reviewable. Do not average into a
total and do not invent halves — the synthesiser needs the spread, and a mean hides the
disagreement worth reading.

## Findings

Numbered continuously and ordered by the manuscript: findings on the introduction first,
then methods, then results, then discussion. Severity is carried in the label, not in the
ordering — an author revises section by section, and a report that jumps between sections
by severity makes them hunt.

The authors will answer these point by point in a response letter, so a comment that cannot
be cited by number is one they will quietly skip.

### F<n>. <short title> — [MAJOR | MINOR]

**Where:** section and a short anchor phrase (5–8 words) so the fix is locatable. For a
figure, the figure number.
**Element:** which row of `criteria.md` this counts against.
**What I read:** what the text actually says, in your words.
**Why it matters:** the mechanism — what a reader does with this, or what it costs the
paper's claim.
**What would fix it:** a concrete change. If the fix requires data, analysis, or permission
the authors may not have, say so explicitly and label it `NEEDS EVIDENCE`.

Severity means:
- **MAJOR** — should be addressed before publication; you would not sign off without it.
  If revision genuinely cannot fix it — it would take a different paper, a different
  analysis, or a different venue — say that explicitly in "What would fix it." That
  sentence is what should drive a REJECT recommendation, not the label on the finding.
- **MINOR** — worth fixing, and reasonable to drop if the authors argue back convincingly.

## What I could not judge

Bullet list. Things outside your remit, or claims you could not verify from the page.
Load-bearing: it is how the synthesiser distinguishes "no reviewer raised this" from "no
reviewer was in a position to raise it."

This panel has three reviewers and no venue-fit reviewer, so this section is longer here
than on a real board. Write it properly rather than treating it as a formality.

## Confidential comments to the editor

Two or three sentences the authors will not see. How close your recommendation is to the
line, whether you would review a revision, anything you would want the editor to weigh.

Keep this separate from the findings. The distinction is what makes both honest.
```

---

## Rules that apply to every reviewer

**Read the whole manuscript.** The abstract is one section among several and it is not
where most problems live. Findings should be distributed across the paper roughly as the
paper's substance is distributed: methods and results usually carry more weight than
abstract and discussion combined. If every finding you have written points at the abstract
or the conclusion, you have skimmed — go back and read the methods and results properly
before submitting the report.

Specifically: check whether the abstract matches the body, but do not let the abstract set
your view of the paper. Where the two disagree, the body is what the paper actually did and
the abstract is the finding.

**Look at the figures.** Where a `[FIGURE n: ...]` placeholder names an image file, open
it. If you cannot view images in this session, record that in the header block and judge
the figures from their placeholders — a report that is silent about which happened cannot
be compared with the others.

**Ignore HTML comments.** Anything inside `<!-- ... -->` is the author's working note, not
part of the manuscript. It is never a finding.

**Judge only what is on the page.** You do not have the authors' CVs, their prior papers,
their raw data, or their intentions. Neither does a real referee. If a claim is not
supported in the manuscript, that is a finding — not something to resolve charitably.

**Anchor every finding.** "The methods are vague" is unusable. "Section 2.3, 'the model was
validated externally' — no cohort, no n, no timeline" is a fix someone can make in ten
minutes.

**Calibrate.** Your recommendation should follow from what you found, not from a disposition
you brought with you. A sound paper gets ACCEPT or MINOR REVISION and you should be willing
to write that; a paper with one fixable problem gets MINOR REVISION rather than MAJOR
because the problem annoyed you. Inflating severity to seem rigorous costs the authors a
revision cycle and costs your report its credibility. Under-calling it wastes everyone's
time later.

One seat holds a deliberately higher evidentiary bar, and it is not yours unless you are
`board-reviewer-2`. Even that seat is a fair referee applying a strict standard, not a
reviewer looking for reasons to reject.

**Separate what the paper did wrong from what it did not report.** These get very different
responses from authors, and conflating them wastes a revision cycle. An analysis that was
probably run and not described is a reporting finding; an analysis that was not run is a
substantive one. When you cannot tell which, say so — that ambiguity is itself the finding.

**Do not invent facts to fill gaps.** If you find yourself writing "presumably the authors
mean…", stop and file the ambiguity as the finding.

**Stay in role.** You have one remit. Straying into another reviewer's territory dilutes the
signal the panel is built to produce — if all three reviewers make the same observation
because they all reached for it, the synthesiser learns nothing from the agreement. Real
convergence comes from three different readers hitting the same defect from three
directions, and that only happens if each stays where it is strongest.
