# Topological Causal Data Analysis

A position-and-framework paper proposing **Topological Causal Data Analysis (TCDA)** as a coherent research domain at the intersection of topological data analysis (TDA) and causal inference.

## Paper

The compiled article is `main.pdf` (44 pages: 33-page body + 10-page bibliography).
LaTeX source is split across `main.tex`, `sections/`, `figures/`, and `bibliography.bib`.

### Sections

| File | Section | Role |
|------|---------|------|
| `sections/introduction.tex` | §1 Introduction | Parallel evolution of TDA and causal inference; motivating limitations; four enumerated contributions |
| `sections/preliminaries.tex` | §2 Preliminaries | Self-contained background on persistent homology, Mapper, Reeb graphs, SCMs, do-calculus, identifiability |
| `sections/framework.tex` | §3 Framework | Formal `Definition 3.1` of a TCDA problem `(M, G, T, C)`; foundational stability and identifiability propositions; four-domain taxonomy A/B/C/D |
| `sections/literature_review.tex` | §4 Literature Review | Five threads of existing work; gap analysis explaining why TCDA is needed now |
| `sections/case_studies.tex` | §5 Case Studies | Five proof-of-concept instantiations spanning biomedical imaging, dependence-network discovery, confounding diagnostics, Mapper-based abstractions, and climate attribution |
| `sections/research_agenda.tex` | §6 Research Agenda | 11 Open Questions, 14 Research Avenues, 4 Computational Challenges, organised into theoretical / methodological / computational / domain / industry strata |
| `sections/conclusion.tex` | §7 Conclusion | Recap, "four cornerstones" framing, caveats, call for interdisciplinary collaboration |

### Figures

| File | Used in | Purpose |
|------|---------|---------|
| `figures/timeline_tikz.tex` | §1 | Parallel timeline of TDA and causal inference |
| `figures/taxonomy_tikz.tex` | §3 | Four-domain TCDA taxonomy (A/B/C/D) |
| `figures/functorial_diagram.tex` | §3 | Commutative diagram for `Definition 3.1` |
| `figures/research_mindmap.tex` | §6 | Mindmap linking the research agenda to formal statements |

## Compilation

The paper uses `pdflatex` + `bibtex` + `natbib` and requires the TikZ libraries declared in `main.tex`.

```bash
pdflatex main.tex
bibtex   main
pdflatex main.tex
pdflatex main.tex
```

This produces `main.pdf` with all cross-references and citations resolved.
Auxiliary files (`main.aux`, `main.bbl`, `main.log`, `main.out`, `main.blg`) are regenerated on each build and are not tracked.

### Required LaTeX packages

`amsmath`, `amssymb`, `amsthm`, `mathtools`, `bm`, `geometry`, `setspace`, `enumitem`, `graphicx`, `booktabs`, `multirow`, `array`, `caption`, `subcaption`, `tikz` (with libraries `positioning`, `arrows.meta`, `shapes`, `fit`, `calc`, `decorations.pathreplacing`, `trees`, `mindmap`, `backgrounds`), `tikz-cd`, `algorithm`, `algpseudocode`, `natbib`, `hyperref`, `cleveref`, `microtype`, `lmodern`.

A current TeX Live distribution (2022 or later) provides all of these.

## Bibliography

`bibliography.bib` holds 157 entries in BibTeX format and is cited via `natbib` with the `plainnat` style.
The four seed papers anchoring the field are:

1. `ibeling2021topological` — topology of causal-model spaces; no-free-lunch
2. `kim2026topological` — doubly-robust, stability-guaranteed topological treatment effects
3. `lecci2014statistical` — statistical inference for persistent homology (confidence sets, bootstrap)
4. `elyaagoubi2023statistical` — simulation-based benchmark for topology-aware discovery in time series

## License

Source files in this repository are research artefacts associated with an in-progress manuscript.
Reuse of the LaTeX source for derivative scholarly work is welcome with citation.
