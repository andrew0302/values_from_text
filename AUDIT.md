# AUDIT — working notes

Scratchpad for cleaning up outputs before finalising the `README.md` manifest.
This file is disposable; the durable map lives in `README.md`.

Method: two-way sweep — every `ggsave`/`gtsave` target in the notebooks checked against
every `\includegraphics`/`\input`/`\include` in `_tex/sections/`, and vice versa. `_tex/`
is a read-only copy of the Overleaf manuscript, used only to resolve what's actually cited.

---

## 1. Orphans — R outputs nothing in the manuscript uses (safe to delete)

| Output file | Notebook | Note |
|---|---|---|
| `tables/main_ethnicity.tex` | `03_main_descriptives.qmd` | superseded by `main_characteristics` merge |
| `tables/main_political_leaning.tex` | `03_main_descriptives.qmd` | superseded by `main_characteristics` merge |
| `tables/pilot_ethnicity.tex` | `01_pilot_demographics.qmd` | superseded by `pilot_characteristics` merge |
| `tables/pilot_political_leaning.tex` | `01_pilot_demographics.qmd` | superseded by `pilot_characteristics` merge |
| `tables/main_lyrics_RRA_by_genre.tex` | `6_RRA_descriptives.Rmd` | never referenced |
| `images/pilot_lyrics_icc2_reliability_by_value.pdf` | `03_pilot_rater_number_estimation.qmd` | ICC2 variant, unused |
| `images/pilot_speeches1_icc2_reliability_by_value.pdf` | `03_pilot_rater_number_estimation.qmd` | ICC2 variant, unused |
| `images/pilot_speeches2_icc2_reliability_by_value.pdf` | `03_pilot_rater_number_estimation.qmd` | ICC2 variant, unused |
| `images/main_emmeans_speeches_by_ethnicity_spectrum_by_value.pdf` | `5_speech_model_analysis.Rmd` | never referenced |
| `images/main_emmeans_speeches_by_ethnicity.pdf` | `5_speech_model_analysis.Rmd` | manuscript wants `..._spectrum.pdf` (see §3) |

Also present in `_tex/tables/` but never `\input` and produced by no notebook:
- `tables/main_r2_table.tex` — stale asset.

---

## 2. Merges — one manuscript table fuses two notebook tables (combined file has NO source)

The manuscript `\input`s a combined table; the components exist but the combined file is
not produced by any notebook (hand-assembled, or from a since-changed notebook). Each needs
a decision: **add a notebook chunk that emits the combined `.tex`**, or accept it as
hand-built and document that.

| Combined file (used) | Component files (produced) | Notebook | Section |
|---|---|---|---|
| `tables/main_characteristics.tex` | `main_ethnicity.tex` + `main_political_leaning.tex` | `03_main_descriptives.qmd` | Main Methods |
| `tables/pilot_characteristics.tex` | `pilot_ethnicity.tex` + `pilot_political_leaning.tex` | `01_pilot_demographics.qmd` | Pilot Methods |
| `tables/quiz_correctness_by_study.tex` | `pilot_quiz_correctness.tex` + `main_quiz_correctness.tex` | `01_quiz_results.qmd` | Appendix D |
| `tables/main_speeches_mod_1a_1b_anova.tex` | `wave_2_speeches_mod_1a_anova.tex` + `wave_2_speeches_mod_1b_anova.tex` | `5_speech_model_analysis.Rmd` | Main Results |

→ If you split the quiz notebook into pilot/main (discussed), the App D merge instead
consumes one table from each of the two new notebooks.

---

## 3. No-source / name drift — manuscript file exists, notebook writes a different name

| Manuscript file | What the notebook actually writes | Notebook | Fix |
|---|---|---|---|
| `images/general_survey_flow.png` | `survey_flow.png` | `0_survey_flow.qmd` | rename `ggsave` target (add `general_` prefix) |
| `images/main_emmeans_speeches_by_ethnicity_spectrum.pdf` | `main_emmeans_speeches_by_ethnicity.pdf` (the `_spectrum` `ggsave` is commented out) | `5_speech_model_analysis.Rmd` | re-enable/rename the intended `ggsave` |
| `images/main_emmeans_text_by_ethnicity_spectrum.pdf` | (nothing) | — | stale filename from the pre-split combined-text model; confirm which current figure replaces it |
| `images/main_missingness_by_text.pdf` | (nothing) | — | NA-% plot has no active source; the `plot_na_percentage()` code in `06_wave_2_precision.Rmd` isn't saved. Decide who owns it |

---

## 4. Model bug — speeches ANOVA table reports the wrong model

`5_speech_model_analysis.Rmd` builds `wave_2_speeches_mod_4_anova.tex` (the interpreted
speeches table in Main Results) from `speeches4` — the **rejected rung-1** model.
`3_speech_model_selection.Rmd` selects the **rung-2** combined model
(`wave_2_speeches_combined_mod.RDS`) and computes its Type III ANOVA + partial η², but
**never saves them to disk**. Repoint the table build to the rung-2 model's ANOVA/η²
(and save those objects in `3_`).

---

## Suggested order

1. Delete §1 orphans.
2. Fix §3 name drifts (cheap: rename `ggsave` targets + matching `\includegraphics`).
3. Resolve §2 merges (add combined-table chunks, or document as hand-built).
4. Fix §4 model bug (save rung-2 ANOVA/η² in `3_`, repoint table in `5_`).
5. Re-run the sweep; every row in `README.md` should read ✅. Then drop the Status column
   and the manifest is submission-ready.
6. Only then touch folder structure.
