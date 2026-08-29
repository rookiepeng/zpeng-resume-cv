# My CV/Résumé

<a href="https://rookiepeng.github.io/zpeng-resume-cv/zpeng_cv.pdf" target="_blank" rel="nofollow"><img src="https://img.shields.io/badge/Curriculum Vitae-PDF-blue.svg" height="20" ></a>
<a href="https://rookiepeng.github.io/zpeng-resume-cv/zpeng_resume.pdf" target="_blank" rel="nofollow"><img src="https://img.shields.io/badge/Résumé-PDF-blue.svg" height="20" ></a>

Both documents are built from one set of sources: the résumé is the two-page
subset, the CV is the full record. Push to `master` and GitHub Actions compiles
both and publishes them to GitHub Pages.

## Layout

```
LaTeX/
├── zpeng_style.tex     # shared design: palette, type scale, spacing, the rail
├── zpeng_resume.tex    # résumé driver — identity + which sections to include
├── zpeng_cv.tex        # CV driver — identity + which sections to include
├── awesome-cv.cls      # upstream Awesome-CV class (unmodified)
└── cv/
    ├── facts.tex              # shared — every count and metric, defined once
    ├── experience.tex         # shared
    ├── education.tex          # shared
    ├── skills.tex             # shared
    ├── summary_resume.tex     # résumé only
    ├── highlights.tex         # résumé only
    ├── selected.tex           # résumé only — a seven-item pick from the .bib
    ├── summary_cv.tex         # CV only
    ├── projects.tex           # CV only
    ├── honors.tex             # CV only
    ├── activities.tex         # CV only
    ├── publications.tex       # CV only — the full record
    └── books.bib, journals.bib, proceedings.bib, patents.bib
```

The two documents diverge because they answer different questions. The résumé
is a two-page argument for a hire, so it folds publications, patents, service
and awards into one `highlights.tex` block and closes on seven representative
works. The CV is the record, so it keeps every appointment as its own entry and
lists the publications in full.

What is *not* duplicated matters as much as what is. Employment is one shared
`experience.tex`; the editorial appointments live only in `activities.tex`,
because they are service rather than employment; and every number either
document quotes — the patent count, the publication totals, the citation
metrics, the review totals — is a macro from `facts.tex`. Editing a count in
one place now changes it everywhere, and the build fails if a count stops
matching the bibliography it claims to summarize.

Anything visual — colors, font sizes, margins, spacing — belongs in
`zpeng_style.tex`, not in the two driver files.

## The design

Both documents are laid out on a single left rail. Dates, skill categories,
honor years and project years all sit in that rail; their content starts at the
same x-position in every section, on every page. That gives one vertical rhythm
rather than a different one per section, and makes the document scannable
either by time (experience, education, honors, projects) or by topic (skills,
highlights). `\cvrailwidth` is the number that matters — change it and the
whole document reflows coherently.

The rail label is hung to the left of the content with `\llap`, so it takes up
no width in the paragraph and the content is ordinary flowing text. That is
what lets a long entry break across a page instead of being pushed onto the
next one whole — which is worth knowing before changing it, because the obvious
implementation (a pair of side-by-side `minipage`s) makes every entry an
unbreakable box and can cost 40% of a page each time one lands near a break.
Two smaller traps are documented at their definitions in `zpeng_style.tex`: the
`\leavevmode` that keeps rail labels on the baseline, and the `\parskip` that
has to be zeroed inside an entry.

Rail labels are expected to fit on one line. A label that wraps degrades to a
wider gap rather than to an overlap, but shorten it — or widen `\cvrailwidth` —
instead.

Type is IBM Plex Sans, with dates set in tabular figures so digits line up down
the rail. The palette is one accent hue plus a four-step neutral ramp;
hierarchy comes from weight and tone rather than from size alone. Text is set
ragged right throughout: justifying a 13 cm measure of sans-serif full of
"mm-wave" and "IEEE Trans." opens rivers between the words.

## Building locally

Requires a TeX Live installation with XeLaTeX, Biber and IBM Plex
(`plex-sans.sty`):

```bash
cd LaTeX
latexmk -xelatex zpeng_cv.tex
latexmk -xelatex zpeng_resume.tex
```

The résumé must come out at two pages and the CV at nine. CI reports both page
counts in the run summary; if a content edit changes them, that is the thing to
look at first.

## Credits

- [Awesome CV](https://github.com/posquit0/Awesome-CV) - LaTeX template for your outstanding job application
