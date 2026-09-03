# The Board
![The Board](tools/board.png)


A panel of 3 independent AI referees for a manuscript ready to be submitted.

You provide the manuscript. Three reviewers read it separately, without seeing each other's notes
and without access to anything except the manuscript. What comes back is one report per reviewer, 
a synthesis showing where they agreed independently, and a plan for what to change.

## Install
Requires Claude Code installed in your terminal.

```bash
git clone <your-repo> the-board
cd the-board
claude
```
Skills load from `.claude/skills/` only when Claude Code starts inside this folder.

## Use

```
/board-panel      run the reviewers and synthesise
/board-triage     turn the findings into a revision plan and a response letter
```

Put the manuscript at `panel/submissions/draft-v1.md` first. Markdown, real section
headings, and figures extracted to image files with placeholders that point at them:
`[FIGURE 1: caption. Axes: … media/figure-1.png]`. The reviewers open the images, so
extract them rather than stripping them to captions — `pandoc --extract-media` does it
during conversion. See `panel/references/document-format.md`.

## The reviewers

| Skill | Role | Looks for |
|---|---|---|
| `board-practitioner` | Practitioner where the findings would land | Whether the effect size would change a decision, whether the setting was real |
| `board-reviewer-2` | The strictest seat | The claim the paper cannot survive losing, and the alternative explanation nobody addressed |
| `board-methodologist` | In-field expert; also the statistical reviewer | Whether the design answers the question, whether the numbers hold, whether it is reproducible |
| `board-panel` | Orchestrator | Dispatches the reviewers, synthesises what came back |
| `board-triage` | Merge step | Reconciles contradictions, sorts fixes, drafts the response letter |

`board-reviewer-2` holds the highest evidentiary bar — a claim earns credit when the
manuscript establishes it, not when it is plausible. It is not a rejection generator, and
when it recommends acceptance that is the strongest signal this board produces. Every
reviewer writes a Strengths section before writing findings.

## Output

`panel/reviews/v1/` gets one report per reviewer plus `panel-summary.md`. Read the summary
first, in this order:

1. **Whether the reviewers read the same paper.** Each one summarises the manuscript before
   criticising it, and the summaries are printed side by side. Divergence there outranks
   everything below.
2. **What held up** — strengths named independently by more than one reviewer. These are the
   parts a revision most easily destroys by accident.
3. **The recommendation spread**, and what an editor would plausibly do with it.
4. **Findings two or more reviewers reached separately.** The highest-confidence signal here.
5. **Where they clashed**, and what has to be true about the manuscript for both to be right.
6. **Confidential comments to the editor**, merged.

`/board-triage` then sorts everything into four piles — fixable by rewriting, fixable by
running an analysis, blocked on data you do not have, and decisions only you can make — and
drafts the point-by-point response letter. It also works on real referee reports: drop them
into `panel/reviews/` and it runs the same process, marking findings to rebut rather than
concede.

## Configure

**`panel/references/criteria.md`** — the elements every reviewer scores against, and the
1–3 scale. Ships with defaults for empirical research. Edit the rows and every report's
score table follows; no skill edits needed. The part worth your time is section 2, on how
review actually works at your target venue — it is what turns a generic critique into a
predictive one.

Nothing in this board checks venue fit: length limits, required sections, and reporting
checklists such as STROBE, CONSORT, PRISMA or CHEERS are not verified by any reviewer.
That is a separate pass before you submit.

## Layout

```
CLAUDE.md                      rules Claude Code reads every session

.claude/skills/                one directory per reviewer, plus panel and triage

tools/                         banner generator + variants

panel/
  references/
    criteria.md                scored elements
    document-format.md         how to prepare a manuscript
    review-format.md           the report structure every reviewer writes to
  submissions/                 your manuscript
  context/                     optional support material; reviewers never read this
  reviews/v1/                  output
```

## Notes
Reviewers cannot see `panel/context/`. Only the triage step can, and only to check whether
something a reviewer said you cannot evidence is already sitting in your files.

Reviewers run as separate agents. 
