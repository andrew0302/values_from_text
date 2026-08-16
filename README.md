# values_from_text

Output manifest: every manuscript figure/table → its output file → the notebook that produces it.
Status: ✅ produced and used · ⚠️ used but needs a fix · 🔀 manuscript merges two notebook outputs · ❓ in manuscript but no notebook produces that exact file.

| Section | Manuscript item | Output file | Notebook | Status |
|---|---|---|---|---|
| General Methods | Survey flow | `images/general_survey_flow.png` | `text/0_survey_flow.qmd` | ⚠️ notebook writes `survey_flow.png` |
| Appendix A | Word counts | `images/general_wordcount.pdf` | `text/3_appendix_A.qmd` | ✅ |
| Appendix A | Screening by year | `images/general_lyric_year.pdf` + `tables/general_lyric_year.tex` | `text/3_appendix_A.qmd` | ✅ |
| Appendix A | Screening by popularity | `images/general_lyric_popularity.pdf` + `tables/general_lyric_popularity.tex` | `text/3_appendix_A.qmd` | ✅ |
| Appendix A | Genre terms | `tables/general_lyric_genre_terms.tex` | `text/3_appendix_A.qmd` | ✅ |
| Appendix A | Screening by genre | `images/general_lyric_genre.pdf` + `tables/general_lyric_genre.tex` | `text/3_appendix_A.qmd` | ✅ |
| Appendix A | Screening by topic | `images/general_lyric_topic.pdf` | `text/3_appendix_A.qmd` | ✅ |
| Appendix A | Speeches per president | `images/general_speeches_president.pdf` + `tables/general_speeches_party.tex` | `text/3_appendix_A.qmd` | ✅ |
| Pilot Methods | Pilot demographics | `tables/pilot_demographics.tex` | `participant/00_descriptives/01_pilot_demographics.qmd` | ✅ |
| Pilot Methods | Pilot characteristics | `tables/pilot_characteristics.tex` | — | ❓ merges `pilot_ethnicity` + `pilot_political_leaning` |
| Pilot Results | Reliability by rater *n* | `images/pilot_reliability_by_n.pdf` | `participant/03_inter_rater_reliability/03_pilot_rater_number_estimation.qmd` | ✅ |
| Pilot Results | Reliability by value — lyrics | `images/pilot_lyrics_reliability_by_value.pdf` | `participant/03_inter_rater_reliability/03_pilot_rater_number_estimation.qmd` | ✅ |
| Pilot Results | Reliability by value — speeches 1 | `images/pilot_speeches1_reliability_by_value.pdf` | `participant/03_inter_rater_reliability/03_pilot_rater_number_estimation.qmd` | ✅ |
| Pilot Results | Reliability by value — speeches 2 | `images/pilot_speeches2_reliability_by_value.pdf` | `participant/03_inter_rater_reliability/03_pilot_rater_number_estimation.qmd` | ✅ |
| Pilot Results | Quiz results | `images/quiz_correctness_by_study.pdf` | `participant/01_quiz_results/01_quiz_results.qmd` | ✅ |
| Main Methods | Main demographics | `tables/main_demographics.tex` | `participant/00_descriptives/03_main_descriptives.qmd` | ✅ |
| Main Methods | Main characteristics | `tables/main_characteristics.tex` | — | ❓ merges `main_ethnicity` + `main_political_leaning` |
| Main Results | MDS plots (self) | `images/main_SSVS_self.pdf` | `participant/04_mds_plots/2_MDS_plots.Rmd` | ✅ |
| Main Results | MDS plots (by text) | `images/main_SSVS_text.pdf` | `participant/04_mds_plots/2_MDS_plots.Rmd` | ✅ |
| Main Results | NA % by value | `images/main_missingness_by_text.pdf` | — | ❓ no notebook writes it |
| Main Results | Rating histogram by text | `images/main_histogram_by_text.pdf` | `participant/00_descriptives/03_main_descriptives.qmd` | ✅ |
| Main Results | Speech model specifications | `tables/main_speech_model_specifications.tex` | `participant/05_variable_importance/3_speech_model_selection.Rmd` | ✅ |
| Main Results | Speech model comparisons | `tables/main_speech_model_comparisons.tex` | `participant/05_variable_importance/3_speech_model_selection.Rmd` | ✅ |
| Main Results | Lyrics ANOVA (lyrics2) | `tables/wave_2_lyrics_mod_2_anova.tex` | `participant/05_variable_importance/4_lyric_model_analysis.Rmd` | ✅ |
| Main Results | Lyrics ANOVA (lyrics1) | `tables/wave_2_lyrics_mod_1_anova.tex` | `participant/05_variable_importance/4_lyric_model_analysis.Rmd` | ✅ |
| Main Results | Lyrics EMM by ethnicity×value | `images/main_emmeans_lyrics_by_ethnicity_value.pdf` | `participant/05_variable_importance/4_lyric_model_analysis.Rmd` | ✅ |
| Main Results | Speeches ANOVA | `tables/wave_2_speeches_mod_4_anova.tex` | `participant/05_variable_importance/5_speech_model_analysis.Rmd` | ⚠️ built from rejected speeches4 (rung-1) model |
| Main Results | Speeches ethnicity×value contrasts | `tables/wave_2_speeches_ethnicity_value_contrasts.tex` | `participant/05_variable_importance/5_speech_model_analysis.Rmd` | ✅ |
| Main Results | EMM by text × ethnicity/spectrum | `images/main_emmeans_text_by_ethnicity_spectrum.pdf` | — | ❓ no notebook writes this exact file |
| Main Results | EMM speeches by ethnicity/spectrum | `images/main_emmeans_speeches_by_ethnicity_spectrum.pdf` | `participant/05_variable_importance/5_speech_model_analysis.Rmd` | ⚠️ notebook writes `main_emmeans_speeches_by_ethnicity.pdf` |
| Main Results | EMM ethnicity/spectrum by party | `images/main_emmeans_spectrum_ethnicity_by_party.pdf` | `participant/05_variable_importance/5_speech_model_analysis.Rmd` | ✅ |
| Main Results | Pre-reg vs interpreted (speeches 1a/1b) | `tables/main_speeches_mod_1a_1b_anova.tex` | — | 🔀 merges `wave_2_speeches_mod_1a_anova` + `_1b_anova` |
| Main Results | Salient values per excerpt (RRA) | `images/main_values_RRA.pdf` | `participant/05_variable_importance/6_RRA_descriptives.Rmd` | ✅ |
| Main Results | Salient values by genre | `images/main_lyrics_RRA_genre.pdf` | `participant/05_variable_importance/6_RRA_descriptives.Rmd` | ✅ |
| Main Results | Salient values by rater characteristic | `images/main_speeches_RRA_characteristic_party.pdf` | `participant/05_variable_importance/6_RRA_descriptives.Rmd` | ✅ |
| Appendix C | Pilot 3 ethnicity | `tables/pilot_ethnicity_speeches2.tex` | `participant/00_descriptives/01_pilot_demographics.qmd` | ✅ |
| Appendix C | Lyric preference questions | `images/pilot_lyrics_questions.pdf` | `participant/00_descriptives/02_pilot_lyrics_questions.qmd` | ✅ |
| Appendix D | Quiz correctness (combined) | `tables/quiz_correctness_by_study.tex` | — | 🔀 merges `pilot_quiz_correctness` + `main_quiz_correctness` (`01_quiz_results.qmd`) |
| Appendix E | Confidence/subjectivity — pilot | `images/pilot_confidence_subjectivity.pdf` | `participant/02_subjectivity_confidence/02_pilot_subjectivity_confidence.qmd` | ✅ |
| Appendix E | Confidence/subjectivity — main | `images/main_confidence_subjectivity.pdf` | `participant/02_subjectivity_confidence/02_main_subjectivity_confidence.qmd` | ✅ |
| Appendix F | Reliability by value — lyrics | `images/main_lyrics_reliability_by_value_by_ethnicity.pdf` | `participant/03_inter_rater_reliability/05_wave_2_reliabilities.Rmd` | ✅ |
| Appendix F | Reliability by value — speeches (ethnicity) | `images/main_speeches_reliability_by_value_by_ethnicity.pdf` | `participant/03_inter_rater_reliability/05_wave_2_reliabilities.Rmd` | ✅ |
| Appendix F | Reliability by value — speeches (spectrum) | `images/main_speeches_reliability_by_value_by_spectrum.pdf` | `participant/03_inter_rater_reliability/05_wave_2_reliabilities.Rmd` | ✅ |
| Appendix F | Value presence by text | `tables/main_value_presence_by_text.tex` | `participant/05_variable_importance/1_preliminary_analysis.Rmd` | ✅ |
| Appendix F | EMM by value by text (table) | `tables/main_emmeans_text_by_value.tex` | `participant/05_variable_importance/1_preliminary_analysis.Rmd` | ✅ |
| Appendix F | EMM by value by text (figure) | `images/main_emmeans_text_by_value.PDF` | `participant/05_variable_importance/1_preliminary_analysis.Rmd` | ✅ |

---

## PROPOSED manifest (post-pruning) — under review, does not replace the table above

Built from the current state of the notebooks (read 2026-08-16) plus the pruning decisions
from planning chats. This is a record of **intent**: it maps each object we want in the
revised manuscript to the notebook output that now produces it, and to the old object it
replaces. The `_tex/` manuscript still cites the *old* set (Phase 9 rewrite pending), so
the "Replaces in manuscript" column is also the Overleaf swap list.

Status: ✅ produced, name matches, ready · ⚠️ produced but notebook/manuscript name still needs aligning · 🆕 new output, no predecessor · ✂️ dropped, no successor · 🔀 manuscript merges two notebook outputs (still hand-assembled) · ⛔ broken chunk to fix before this output regenerates.

Ordered by intended manuscript appearance.

| # | Section | Manuscript item | Output file (produced now) | Replaces (old object / manuscript ref) | Notebook | Status |
|---|---|---|---|---|---|---|
| 1 | General Methods | Survey flow | `images/survey_flow.png` | manuscript cites `general_survey_flow.png` | `text/0_survey_flow.qmd` | ⚠️ align name (add `general_` prefix to `ggsave`, or update manuscript) |
| 2 | Appendix A | Word counts | `images/general_wordcount.pdf` | — | `text/3_appendix_A.qmd` | ✅ |
| 3 | Appendix A | Screening by year | `images/general_lyric_year.pdf` + `tables/general_lyric_year.tex` | — | `text/3_appendix_A.qmd` | ✅ |
| 4 | Appendix A | Screening by popularity | `images/general_lyric_popularity.pdf` + `tables/general_lyric_popularity.tex` | — | `text/3_appendix_A.qmd` | ✅ |
| 5 | Appendix A | Genre terms | `tables/general_lyric_genre_terms.tex` | — | `text/3_appendix_A.qmd` | ✅ |
| 6 | Appendix A | Screening by genre | `images/general_lyric_genre.pdf` + `tables/general_lyric_genre.tex` | — | `text/3_appendix_A.qmd` | ✅ |
| 7 | Appendix A | Screening by topic | `images/general_lyric_topic.pdf` | — | `text/3_appendix_A.qmd` | ✅ |
| 8 | Appendix A | Speeches per president | `images/general_speeches_president.pdf` + `tables/general_speeches_party.tex` | — | `text/3_appendix_A.qmd` | ✅ |
| 9 | Pilot Methods | Pilot demographics | `tables/pilot_demographics.tex` | — | `participant/00_descriptives/01_pilot_demographics.qmd` | ✅ |
| 10 | Pilot Methods | Pilot characteristics | `tables/pilot_characteristics.tex` (hand-merged) | merges `pilot_ethnicity.tex` + `pilot_political_leaning.tex` | `participant/00_descriptives/01_pilot_demographics.qmd` | 🔀 decide: add merge chunk or document as hand-built |
| 11 | Pilot Results | Reliability by rater *n* | `images/pilot_reliability_by_n.pdf` | — | `participant/03_inter_rater_reliability/03_pilot_rater_number_estimation.qmd` | ✅ |
| 12 | Pilot Results | Reliability by value — lyrics | `images/pilot_lyrics_reliability_by_value.pdf` | — | `participant/03_inter_rater_reliability/03_pilot_rater_number_estimation.qmd` | ✅ |
| 13 | Pilot Results | Reliability by value — speeches 1 | `images/pilot_speeches1_reliability_by_value.pdf` | — | `participant/03_inter_rater_reliability/03_pilot_rater_number_estimation.qmd` | ✅ |
| 14 | Pilot Results | Reliability by value — speeches 2 | `images/pilot_speeches2_reliability_by_value.pdf` | — | `participant/03_inter_rater_reliability/03_pilot_rater_number_estimation.qmd` | ✅ |
| 15 | Pilot Results | Quiz results | `images/quiz_correctness_by_study.pdf` | — | `participant/01_quiz_results/01_quiz_results.qmd` | ✅ |
| 16 | Main Methods | Main demographics | `tables/main_demographics.tex` | — | `participant/00_descriptives/03_main_descriptives.qmd` | ✅ |
| 17 | Main Methods | Main characteristics | `tables/main_characteristics.tex` (hand-merged) | merges `main_ethnicity.tex` + `main_political_leaning.tex` | `participant/00_descriptives/03_main_descriptives.qmd` | 🔀 decide: add merge chunk or document as hand-built |
| 18 | Main Results | MDS plots (self) | `images/main_SSVS_self.pdf` | — | `participant/04_mds_plots/2_MDS_plots.Rmd` | ✅ |
| 19 | Main Results | MDS plots (by text) | `images/main_SSVS_text.pdf` | — | `participant/04_mds_plots/2_MDS_plots.Rmd` | ✅ |
| 20 | Main Results | Rating histogram by text | `images/main_histogram_by_text.pdf` | — | `participant/00_descriptives/03_main_descriptives.qmd` | ✅ |
| 21 | Main Results | Speech model specifications | `tables/main_speech_model_specifications.tex` | — | `participant/05_variable_importance/3_speech_model_selection.Rmd` | ✅ |
| 22 | Main Results | Speech model comparisons | `tables/main_speech_model_comparisons.tex` | — | `participant/05_variable_importance/3_speech_model_selection.Rmd` | ✅ |
| 23 | Main Results | Lyrics ANOVA (lyrics2) | `tables/wave_2_lyrics_mod_2_anova.tex` | — | `participant/05_variable_importance/4_lyric_model_analysis.Rmd` | ✅ |
| 24 | Main Results | Lyrics EMM by ethnicity×value | `images/main_emmeans_lyrics_by_ethnicity_value.pdf` | — | `participant/05_variable_importance/4_lyric_model_analysis.Rmd` | ✅ |
| 25 | Main Results | Subgroup deviation (speeches) | `tables/wave_2_speeches_subgroup_deviation.tex` | none | `participant/05_variable_importance/5_speech_model_analysis.Rmd` | 🆕 new output; confirm manuscript placement |
| 26 | Main Results | Speeches ANOVA (selected rung-2) | `tables/wave_2_speeches_mod_4_anova.tex` | replaces the same-named table **built from rejected speeches4 / rung-1** | `participant/05_variable_importance/5_speech_model_analysis.Rmd` | ✅ now reads rung-2 cached ANOVA/η² (Table 7 bug fixed) |
| 27 | Main Results | Speeches ethnicity×value contrasts | `tables/wave_2_speeches_ethnicity_value_contrasts.tex` | — | `participant/05_variable_importance/5_speech_model_analysis.Rmd` | ⛔ chunk currently commented out — re-enable if this table is kept; decide keep vs. cut |
| 28 | Main Results | Figure 13 — EMM by ethnicity × spectrum (2 panels) | `images/main_emmeans_speeches_by_ethnicity_spectrum.pdf` | replaces name-drift `main_emmeans_speeches_by_ethnicity.pdf` (old Fig 14, now dropped) | `participant/05_variable_importance/5_speech_model_analysis.Rmd` | ⛔ two-panel chunk currently commented out — re-enable to produce this figure |
| 29 | Main Results | Figure 15 — EMM ethnicity/spectrum | `images/main_emmeans_spectrum_ethnicity_by_party.pdf` | replaces party-faceted version (party interaction only trended) | `participant/05_variable_importance/5_speech_model_analysis.Rmd` | ⚠️ filename still says `_by_party` but plot no longer facets by party — consider renaming |
| 30 | Main Results | Pre-reg vs interpreted (speeches 1a/1b) | `tables/main_speeches_mod_1a_1b_anova.tex` (hand-merged) | merges `wave_2_speeches_mod_1a_anova.tex` + `_1b_anova.tex` | `participant/05_variable_importance/5_speech_model_analysis.Rmd` | 🔀 appendix comparator; add merge chunk or document as hand-built |
| 31 | Main Results | Salient values per excerpt (RRA) | `images/main_values_RRA.pdf` | — | `participant/05_variable_importance/6_RRA_descriptives.Rmd` | ✅ |
| 32 | Main Results | Salient values by genre | `images/main_lyrics_RRA_genre.pdf` | — | `participant/05_variable_importance/6_RRA_descriptives.Rmd` | ✅ |
| 33 | Main Results | Salient values by rater characteristic | `images/main_speeches_RRA_characteristic_party.pdf` | — | `participant/05_variable_importance/6_RRA_descriptives.Rmd` | ✅ |
| 34 | Appendix C | Pilot 3 ethnicity | `tables/pilot_ethnicity_speeches2.tex` | — | `participant/00_descriptives/01_pilot_demographics.qmd` | ✅ |
| 35 | Appendix C | Lyric preference questions | `images/pilot_lyrics_questions.pdf` | — | `participant/00_descriptives/02_pilot_lyrics_questions.qmd` | ✅ |
| 36 | Appendix D | Quiz correctness (combined) | `tables/quiz_correctness_by_study.tex` (hand-merged) | merges `pilot_quiz_correctness.tex` + `main_quiz_correctness.tex` | `participant/01_quiz_results/01_quiz_results.qmd` | 🔀 add merge chunk or document as hand-built |
| 37 | Appendix E | Confidence/subjectivity — pilot | `images/pilot_confidence_subjectivity.pdf` | — | `participant/02_subjectivity_confidence/02_pilot_subjectivity_confidence.qmd` | ✅ |
| 38 | Appendix E | Confidence/subjectivity — main | `images/main_confidence_subjectivity.pdf` | — | `participant/02_subjectivity_confidence/02_main_subjectivity_confidence.qmd` | ✅ |
| 39 | Appendix F | Reliability by value (overall, lyrics + speeches) | `images/main_reliability_by_value.pdf` | none | `participant/03_inter_rater_reliability/05_wave_2_reliabilities.Rmd` | 🆕 new output; confirm manuscript placement |
| 40 | Appendix F | Reliability by value — lyrics (by ethnicity) | `images/main_lyrics_reliability_by_value_by_ethnicity.pdf` | — | `participant/03_inter_rater_reliability/05_wave_2_reliabilities.Rmd` | ✅ |
| 41 | Appendix F | Reliability by value — speeches (ethnicity) | `images/main_speeches_reliability_by_value_by_ethnicity.pdf` | — | `participant/03_inter_rater_reliability/05_wave_2_reliabilities.Rmd` | ✅ |
| 42 | Appendix F | Reliability by value — speeches (spectrum) | `images/main_speeches_reliability_by_value_by_spectrum.pdf` | — | `participant/03_inter_rater_reliability/05_wave_2_reliabilities.Rmd` | ✅ |
| 43 | Appendix F | Value presence by text | `tables/main_value_presence_by_text.tex` | — | `participant/05_variable_importance/1_preliminary_analysis.Rmd` | ✅ |
| 44 | Appendix F | EMM by value by text (table) | `tables/main_emmeans_text_by_value.tex` | — | `participant/05_variable_importance/1_preliminary_analysis.Rmd` | ✅ |
| 45 | Appendix F | EMM by value by text (figure) | `images/main_emmeans_text_by_value.PDF` | — | `participant/05_variable_importance/1_preliminary_analysis.Rmd` | ✅ |

### Dropped from the manuscript (no successor — remove from Overleaf)

| Old manuscript item | Old output file | Note |
|---|---|---|
| ✂️ Figure 9 — NA % by value by text | `images/main_missingness_by_text.pdf` | subsumed by histogram (Fig 10); manuscript still `\includegraphics` it — remove |
| ✂️ Figure 14 — EMM speeches by ethnicity | `images/main_emmeans_speeches_by_ethnicity.pdf` | dropped; ethnicity×spectrum covered by Figure 13 (#28) |
| ✂️ EMM by text × ethnicity/spectrum | `images/main_emmeans_text_by_ethnicity_spectrum.pdf` | stale filename from pre-split combined-text model; manuscript still cites it — remove |
| ✂️ RRA by genre table | `tables/main_lyrics_RRA_by_genre.tex` | still written by `6_RRA_descriptives.Rmd` but never referenced — leave unreferenced or cut chunk |

### Open decisions before this manifest can go clean

1. **Re-enable the two commented-out speeches chunks** (#27 contrasts table, #28 Figure 13) if those outputs are kept — they currently produce nothing.
2. **Fix the broken `print_apa_comparisons(apa_ethspec)` chunk** in `5_speech_model_analysis.Rmd` — `apa_ethspec` no longer exists (helper deleted), so the chunk errors on run.
3. **Figure 15 filename** (#29) — decide whether to rename `main_emmeans_spectrum_ethnicity_by_party.pdf` now that party faceting is gone.
4. **New outputs** (#25 subgroup deviation, #39 overall reliability by value) — confirm where each lands in the manuscript.
5. **Merges** (#10, #17, #30, #36) — decide per row: add a notebook chunk that emits the combined `.tex`, or accept hand-built and document.
6. **Survey-flow name** (#1) — align `survey_flow.png` ↔ `general_survey_flow.png`.
