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
