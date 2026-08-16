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

## Building locally

Requires a TeX Live installation with XeLaTeX and Biber:

```bash
cd LaTeX
latexmk -xelatex zpeng_cv.tex
latexmk -xelatex zpeng_resume.tex
```

## Credits

- [Awesome CV](https://github.com/posquit0/Awesome-CV) - LaTeX template for your outstanding job application
