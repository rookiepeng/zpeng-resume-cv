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
    ├── summary.tex       # sections shared by both documents
    ├── experience.tex
    ├── education.tex
    ├── skills.tex
    ├── honors.tex
    ├── highlights.tex    # résumé only
    ├── projects.tex      # CV only
    ├── activities.tex    # CV only
    ├── publications.tex  # CV only
    └── books.bib, journals.bib, proceedings.bib, patents.bib
```

Content lives in `cv/` and is shared by both documents, so an edit to
`cv/experience.tex` updates the résumé and the CV together. `highlights.tex` is
the one résumé-only block: a condensed view of the publications, patents,
service and open-source work that the CV lists in full.

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
