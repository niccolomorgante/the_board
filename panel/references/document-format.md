# Document conventions

The board reviews documents it did not write. This file is the contract between whatever
you drop in and what the reviewers can work with.

## Where things go

```
panel/submissions/   the manuscript under review, versioned: draft-v1.md, draft-v2.md
panel/context/       optional. Supplementary material, protocol, prior analyses.
panel/reviews/v1/    output, one file per reviewer plus panel-summary.md
```

**Referees never read `panel/context/`.** Only `board-triage` does, and only to check
whether a NEEDS EVIDENCE finding is actually answerable from material you already have.
This is the whole point: a referee has your manuscript and nothing else, so a reviewer who
has seen your supplementary material is not simulating a referee, they are simulating a
co-author.

## Preparing a submission

Markdown is the working format. It costs nothing to convert to, it keeps section
boundaries explicit, and it lets the reviewers anchor findings to a heading.

### From Word

```
pandoc --track-changes=reject --extract-media=panel/submissions/media \
       draft.docx -o panel/submissions/draft-v1.md
```

`--track-changes=reject` matters. The default renders insertions and deletions inline, and
a reviewer will spend findings on text you already deleted. Use `accept` if the version
you want reviewed is the marked-up one — but choose, do not leave it to the default.

Comments in the Word file are dropped by pandoc. If they contain anything the reviewers
should see, move it into the text first.

### From PDF

Pandoc cannot read PDF. If a Word or LaTeX original exists, convert that instead — always
prefer it. If PDF is all you have:

```
pdftotext -layout draft.pdf draft.txt
```

then fix the output by hand. Expect to spend ten minutes on it. Two-column layouts
interleave into nonsense, tables lose their structure entirely, ligatures and hyphens break
words across line ends, and headers and footers repeat on every page. A reviewer who hits
this debris will report it as unclear writing, which wastes a finding and misleads you.

Do not submit a PDF conversion you have not read through once yourself.

### After any conversion, check these

Conversion fails silently, so verify rather than assume:

- **Section headings survived**, with the manuscript's own labels.
- **Every figure has a placeholder** with a working image path — count them against the
  original and open two at random.
- **Tables are still tables**, not runs of loose text.
- **Equations survived.** Word equations often convert to nothing at all. If a formula is
  load-bearing, retype it.
- **Reference list is intact**, or deliberately removed.

## Headings

One `##` per section, using the real labels: `## Abstract`, `## Methods`, `## Discussion`.
If the journal requires a structured abstract, keep its subheadings as `###` so the journal
reviewer can check them.

## Figures

Reviewers look at the figures. Extract them and point at them:

```
[FIGURE 1: caption text exactly as submitted. Axes: x = follow-up months,
y = proportion event-free. media/figure-1.png]
```

`--extract-media` writes the image files during conversion; the placeholder is what tells a
reviewer where to find them. Name the file path in every placeholder, and check the paths
resolve before you run the panel — a broken path degrades silently into a caption-only
read.

Keep the caption and the axis description even when the image is there. They are what a
reviewer falls back on if it cannot open images, and writing them is its own test: a figure
you cannot describe in two lines has already failed.

**Do it for every figure or none.** A panel where some figures are visible and others are
captions produces findings that contradict each other, and you will not be able to tell
from the reports which reviewer saw what.

From a PDF, extract page images rather than nothing:

```
pdftoppm -png -r 150 draft.pdf panel/submissions/media/page
```

Crop to the figure if you can be bothered; a full page is still far better than a caption.

## Tables

Keep them as Markdown tables. If a table is too wide to survive as one, that is worth
knowing — it means it is too wide in the manuscript too.

## Anchoring

Reviewers locate findings with a section plus a short quoted phrase. That survives
reformatting; line and page numbers do not, and drift the moment you revise. Do not add
them.

## Keeping notes out of the review

Anything inside an HTML comment `<!-- ... -->` is a note to yourself, not part of the
manuscript. This only works if the reviewer skills say so — check that they do before
relying on it.

Pandoc can also emit raw HTML from Word. Convert with `-t markdown-raw_html` if you want to
be sure no stray markup is mistaken for your own notes.

## Versioning

Never edit a draft in place. `draft-v1.md` stays exactly as the panel saw it, so round-2
findings can be compared against round-1 findings honestly. If the text moves, the version
number moves.
