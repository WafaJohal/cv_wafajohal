# cv-repo — Wafa Johal Academic CV

## Repository structure

```
cv-repo/
├── config/
│   ├── section_config.tex       # Section/subsection formatting macros (coloured headers)
│   └── bib_config.tex           # biblatex configuration; bolds "Johal, Wafa" in references
├── sections/                    # One file per section; variant suffixes explained below
│   ├── employment.tex           # Full: 5 positions with all details
│   ├── employment_short.tex     # Condensed: all 5, no keywords/links
│   ├── employment_mini.tex      # Mini: 5 positions, 2–3 lines each
│   ├── supervision.tex          # All 10 current students
│   ├── supervision_short.tex    # Current students, max 6 active + TRIM-marked extras
│   ├── supervision_past.tex     # 13 completed supervisees
│   ├── awards.tex               # Full: 11 awards
│   ├── awards_mini.tex          # Top 6 awards
│   ├── teaching.tex             # 3 institutions (UniMelb, UNSW, EPFL)
│   ├── institutional.tex        # 8 institutional responsibilities
│   ├── talks.tex                # Full: 24 invited talks
│   ├── talks_short.tex          # Short: 10 selected talks
│   ├── projects.tex             # Full: 14 projects
│   ├── projects_short.tex       # Short: 7 key projects
│   ├── projects_mini.tex        # Mini: 4 current/most significant
│   ├── membership.tex           # Full: editorial, org committee, reviewing
│   ├── membership_short.tex     # Short: editorial + org committee + funding reviews
│   ├── membership_mini.tex      # Mini: 4 headline entries
│   ├── education.tex            # 3 degrees (PhD, MS, BS/BA)
│   ├── publications.tex         # Full manual list (journals, conf, book chapters,
│   │                            #   French conf, patents, other, thesis)
│   │                            #   — replace with \printbibliography once bib/ is populated
│   ├── publications_top10.tex   # Numbered list of 10 selected publications
│   ├── publications_mini.tex    # 5–6 most recent selected publications
│   ├── service.tex              # Workshop/seminar organisation (14 entries) +
│   │                            #   commented-out scientific societies placeholder
│   ├── careerbreaks.tex         # 2 maternity leaves
│   └── references.tex           # 3 academic referees
├── bib/
│   └── references.bib           # PLACEHOLDER — populate from sections/publications.tex
├── cv_full.tex                  # Full CV driver — no page limit
├── cv_2p.tex                    # 2-page CV driver — short/mini variants
├── cv_1p.tex                    # 1-page CV driver — mini variants only
└── README.md                    # This file
```

---

## How to compile

**Required engine:** LuaLaTeX or XeLaTeX (needed for the Carlito font via `fontspec`).

```bash
# Full CV
lualatex cv_full.tex

# 2-page CV
lualatex cv_2p.tex

# 1-page CV
lualatex cv_1p.tex
```

If the Carlito font is not installed on your system, install it from Google Fonts or substitute another sans-serif in each driver file:
```latex
\setmainfont{Carlito}   % change to e.g. Calibri, Helvetica, or TeX Gyre Heros
```

---

## How to add a new entry

| Section | Edit this file | Also update |
|---|---|---|
| New position | `sections/employment.tex` | `employment_short.tex`, `employment_mini.tex` |
| New student | `sections/supervision.tex` | `supervision_short.tex` (if current) |
| Student completed | Move from `supervision.tex` to `supervision_past.tex` | Remove from `supervision_short.tex` |
| New award | `sections/awards.tex` | `awards_mini.tex` (if top-6 calibre) |
| New talk | `sections/talks.tex` | `talks_short.tex` (if notable) |
| New project | `sections/projects.tex` | `projects_short.tex`, `projects_mini.tex` as appropriate |
| New publication | `sections/publications.tex` (manual list) | `publications_mini.tex` if recent & significant; `bib/references.bib` when migrating to biblatex |
| New service/org role | `sections/membership.tex` | `membership_short.tex`, `membership_mini.tex` as appropriate |
| New workshop organised | `sections/service.tex` | — |

---

## Variant convention

Each section exists in up to three variants:

| Suffix | Purpose | Typical length |
|---|---|---|
| *(none)* | **Full** — everything, used in `cv_full.tex` | No limit |
| `_short` | **Short** — most significant recent entries | Fits a 2-page CV |
| `_mini` | **Mini** — headline entries only | 3–6 rows / lines max |

Entries marked `% TRIM: consider removing for short variant` are included in the full file but should be evaluated for removal when the short/mini version feels crowded.

Entries marked `% (was commented out in original)` were already commented out in the legacy YAAC source files; they are preserved here as comments in case they need to be reinstated.

---

## Migration notes

- **Source:** `CV_WafaJohal_deprecated/` (YAAC `yaac-another-awesome-cv` template)
- **New style:** plain LaTeX with `titlesec` + `tabularx`; section headers use coloured backgrounds defined in `config/section_config.tex`
- **YAAC macros removed:** `\sectionTitle`, `\begin{experiences}`, `\experience`, `\experiencemini`, `\begin{keywords}`, `\keywordsentry`, `\begin{projects}`, `\project`, `\projectmini`, `\begin{scholarship}`, `\scholarshipentry`, `\begin{referees}`, `\referee`
- **`cv_alone.tex`:** This file was referenced as the design template but did not exist in the source. The new style preamble was constructed from `config/section_config.tex` and `config/header_short.tex` (both already present in the workspace).
- **`list_talks.tex`:** Was a full LaTeX document (not a section file); its content (`section_scientific_societies.tex`, which contained invited talks despite the name) is now in `sections/talks.tex`.
- **`section_headline.tex` / `section_competences.tex`:** Contained French-language boilerplate from the YAAC template (not Wafa's content). Not migrated.
- **`bib_config.tex`:** Copied from `bib_author.tex` in the workspace and updated to reference `bib/references.bib`.
- **`publications.tex`:** Currently uses manual citation lists. Once `bib/references.bib` is populated, replace each `\begin{itemize}` block with the corresponding `\printbibliography[type=..., title={...}]` call (template is commented at the top of the file).

---

## Known issue in source files

`config/section_config.tex` contains a duplicate definition of `\unnumberedsection` (copied verbatim from the source). This does not affect compilation but may generate a warning. The second definition (the one that uses `\addcontentsline`) takes precedence.
