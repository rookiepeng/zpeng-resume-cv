# My CV/Résumé

<a href="https://rookiepeng.github.io/zpeng-resume-cv/zpeng_cv.pdf" target="_blank" rel="nofollow"><img src="https://img.shields.io/badge/Curriculum Vitae-PDF-blue.svg" height="20" ></a>
<a href="https://rookiepeng.github.io/zpeng-resume-cv/zpeng_resume.pdf" target="_blank" rel="nofollow"><img src="https://img.shields.io/badge/Résumé-PDF-blue.svg" height="20" ></a>

Both documents are built from one set of sources: the résumé is the two-page
subset, the CV is the full record. Push to `master` and GitHub Actions compiles
both and publishes them to GitHub Pages.

## Layout

```
LaTeX/
├── zpeng_style.tex     # shared design: palette, type scale, spacing, layout fixes
├── zpeng_resume.tex    # résumé driver — identity + which sections to include
├── zpeng_cv.tex        # CV driver — identity + which sections to include
├── awesome-cv.cls      # upstream Awesome-CV class (unmodified)
└── cv/
    ├── education.tex          # shared by both documents
    ├── skills.tex             # shared
    ├── summary_resume.tex     # résumé only
    ├── experience_resume.tex  # résumé only
    ├── highlights.tex         # résumé only
    ├── summary_cv.tex         # CV only
    ├── experience.tex         # CV only
    ├── projects.tex           # CV only
    ├── honors.tex             # CV only
    ├── activities.tex         # CV only
    ├── publications.tex       # CV only
    ├── activities_back.tex    # not compiled — per-journal review counts,
    │                          #   the source for the totals in activities.tex
    └── books.bib, journals.bib, proceedings.bib, patents.bib
```

Only `education.tex` and `skills.tex` are shared; everything else is written
for one document or the other. The two diverge because they answer different
questions. The résumé is a two-page argument for a hire, so it carries Aptiv
and MERL and folds publications, patents, service and awards into one
`highlights.tex` block. The CV is the full record, so it keeps every editorial
appointment as its own entry and lists the publications in full.

That means a fact appearing in both documents — the patent count, the review
totals, the citation metrics — lives in two files. When one changes, grep for
the old number before assuming a single edit covered it.

Anything visual — colors, font sizes, margins, spacing — belongs in
`zpeng_style.tex`, not in the two driver files.

## The design

Both documents are laid out on a single left rail. Dates, skill categories,
honor years and project names all sit in that rail, right-aligned; their
content starts at the same x-position on every page. That gives one vertical
rhythm rather than a different one per section, and makes the document
scannable either by time (experience, education, honors) or by topic (skills,
projects).

Everything is built on one primitive, `\cvrailline{<width>}{<rail>}{<content>}`,
so `\cventry`, `\cvskill` and `\cvhonor` all share the same geometry.
`\cvrailwidth` is the number that matters — change it and the whole document
reflows coherently. Sections whose labels need more room than a date (the
project lists) pass their own width: `\begin{cvskills}[4.15cm]`.

Type is IBM Plex Sans, with dates set in tabular figures so digits line up
down the rail. The palette is one accent hue plus a four-step neutral ramp;
hierarchy comes from weight and tone rather than from size alone.

## Building locally

Requires a TeX Live installation with XeLaTeX and Biber:

```bash
cd LaTeX
latexmk -xelatex zpeng_cv.tex
latexmk -xelatex zpeng_resume.tex
```

## Credits

- [Awesome CV](https://github.com/posquit0/Awesome-CV) - LaTeX template for your outstanding job application
