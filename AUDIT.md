# AUDIT — Notebook-to-Manuscript Map

Static, read-only audit per `AUDIT_BRIEF.md`. No notebook, data, or manuscript file was
executed, rendered, moved, renamed, or edited to produce this report.

**Rule deviation, flagged per the brief's "record it, don't guess" instruction:** the
brief's matching rule names `\includegraphics{...}` and `\input{...}`. Five table
citations in `_tex/sections/91_appendix_A.tex` actually use `\include{...}` (a third,
functionally-identical LaTeX command the brief didn't name — e.g.
`\include{tables/general_lyric_genre}`). I've treated `\include` the same as `\input`
for matching, since excluding it would misreport five correctly-cited tables as
"Missing." Flagging this rather than silently expanding the rule.

Two resolved conventions applied throughout (per prior discussion):
- Commented-out `ggsave()`/`gtsave()` calls are included as real outputs, tagged
  `(save commented — render-time skip)`.
- A citation found only in `_tex/sections/97_appendix_G.tex` (whose own `\input` is
  commented out in `manuscript.tex`) would count as `✓ (appendix G only — commented
  out)` with `Recommendation = Unsure`. In practice this never applies: every citation
  inside `97_appendix_G.tex` duplicates a citation that's also active in
  `32_main_results.tex`, so no notebook's fate hinges on it.

Archived subfolders skipped (contents not audited, per scope): each of
`00_descriptives/`, `01_quiz_results/`, `02_subjectivity_confidence/`,
`03_inter_rater_reliability/`, `04_mds_plots/`, and `05_variable_importance/` under
`_notebooks/participant/` has an `archive/` subfolder.

## Notebook map

### `_notebooks/machine/` (status uncertain per AGENTS.md — not modified)

| Notebook | Likely runs? (static) | Figure/table outputs | Data outputs | In `_tex/`? | Section / approx. lines | Recommendation (provisional) |
|---|---|---|---|---|---|---|
| `01_format_data.Rmd` | ✓ likely (all inputs exist: `wave_1_m_df.RDS`, `wave_2_m_dfs.RDS`, `wave_1_llm_df.RDS`, `wave_2_llm_dfs.RDS`, `wave_2_supervised_dfs.RDS` in `_data/_machine_scores/`; `wave_1_df.RDS`, `wave_2_dfs.RDS` in `_data/_participant_scores/`) — note: line 51 references `wave_2_llm_df`/`wave_2_supervised_df`/`wave_2_w2v_df` which are never assigned in this file (only the plural `*_dfs` list objects are); this looks like it would error at runtime despite inputs existing | none — writes `machine_df.RDS` to `_data/_machine_scores/` | — | n/a | Unsure (no figure/table outputs) |
| `02_lyrics_correlations.Rmd` | ✓ likely (all inputs exist: `wave_2_dfs.RDS`, `wave_1_df.RDS` in `_participant_scores/`; `wave_2_m_dfs.RDS`, `wave_2_llm_dfs.RDS`, `wave_2_supervised_dfs.RDS` in `_machine_scores/`) | none | none written | n/a | Unsure (no figure/table outputs) |
| `llm_pilots/1_overall_reliabilities.Rmd` | ✗ broken — reads `pilot_dfs.RDS` from `path <- here("_data","_intermediary_data","wave_2")`; that `wave_2` subdirectory does not exist under `_intermediary_data` (only `bootstrapped_ICC/`, `demog_dfs/`, `models/`, `spec_curves/`, and files directly do) | none | none | n/a | Unsure (no figure/table outputs; also broken) |
| `llm_pilots/2_overall_correlations.Rmd` | ✗ broken — same missing `path`; also reads `_data/_raw_data/wave_2/pilot_2_dfs.RDS`, and `_data/_raw_data/` does not exist anywhere in the repo | none | none | n/a | Unsure |
| `llm_pilots/3_subset_correlations.Rmd` | ✗ broken — same two missing paths as `2_overall_correlations.Rmd` | none | none | n/a | Unsure |
| `llm_pilots/4_estimate_bootstrap_reliability.Rmd` | ✗ broken — same missing `path` | none | writes `bootstrap_dfs.RDS` to the same nonexistent `path` | n/a | Unsure |
| `llm_pilots/5_plot_bootstrap_reliability.Rmd` | ✗ broken — reads `bootstrap_dfs.RDS` from the same nonexistent `path` (which `4_*` would also fail to write) | none | none | n/a | Unsure |
| `llm_waves/1_overall_reliabilities.Rmd` | ✗ broken — reads `wave_df.RDS` from the same nonexistent `_intermediary_data/wave_2` path | none | none | n/a | Unsure |
| `llm_waves/2_overall_correlations.Rmd` | ✗ broken — same, plus reads `_data/_raw_data/wave_2/wave_2_dfs.RDS` (nonexistent dir) | none | none | n/a | Unsure |
| `llm_waves/3_rank_correlations.Rmd` | ✗ broken — same two issues as `2_overall_correlations.Rmd` | none | none | n/a | Unsure |
| `llm_waves/4_energy_consumption.Rmd` | ✗ broken — reads `_data/_machine_scores/LLMs/wave_2/energy.csv`; no `LLMs/` subfolder exists under `_machine_scores/` | none | none | n/a | Unsure |

Pipeline order note: within `llm_pilots/` and `llm_waves/`, numeric prefixes (`1`…`5`,
`1`…`4`) indicate run order, and `4`/`5` (and `2`/`3`) each depend on outputs of earlier
steps in the same subfolder. Since the shared `path <- here("_data","_intermediary_data","wave_2")`
doesn't exist, the whole chain in both subfolders is static-broken at its root input,
independent of run order.

### `_notebooks/participant/00_descriptives/`

| Notebook | Likely runs? (static) | Figure/table outputs | Data outputs | In `_tex/`? | Section / approx. lines | Recommendation (provisional) |
|---|---|---|---|---|---|---|
| `00_pilot_demographics_data_format.qmd` | ✓ likely (`pilot_2_dfs.RDS` exists in `_data/_participant_scores/wave_2/`) | none | in: `pilot_2_dfs.RDS`; out: `pilot_2_demog_df.RDS`, `pilot_2_demog_dfs.RDS` (both exist in `_data/_intermediary_data/demog_dfs/`, feeding `01_pilot_demographics.qmd`) | n/a | Unsure (no figure/table outputs) |
| `01_pilot_demographics.qmd` | ✓ likely (`pilot_2_demog_dfs.RDS` exists) | `pilot_demographics.tex`; `pilot_ethnicity.tex`; `pilot_political_leaning.tex`; `pilot_ethnicity_speeches2.tex` | in: `pilot_2_demog_dfs.RDS` | `pilot_demographics.tex` ✓; `pilot_ethnicity_speeches2.tex` ✓; `pilot_ethnicity.tex` ✗; `pilot_political_leaning.tex` ✗ | `pilot_demographics.tex`: Pilot Methods §Ratings per stimulus, `_tex/sections/21_pilot_methods.tex:13`. `pilot_ethnicity_speeches2.tex`: Pilot Study Addendum §Demographics, `_tex/sections/93_appendix_C.tex:8` | Keep |
| `02_pilot_lyrics_questions.qmd` | ✓ likely (`pilot_2_dfs.RDS` exists) | `pilot_lyrics_questions.pdf` | in: `pilot_2_dfs.RDS` | ✓ | Pilot Study Addendum §Lyric Preferences, `_tex/sections/93_appendix_C.tex:17` | Keep |
| `03_main_descriptives.qmd` | ✓ likely (`wave_2_dfs.RDS` exists both in `_participant_scores/wave_2/` and `_intermediary_data/`) | `main_demographics.tex`; `main_ethnicity.tex`; `main_political_leaning.tex`; `main_missingness_by_text.pdf` (line 297; commented duplicate at line 296, same name — tagged `(save commented — render-time skip)`); `main_histogram_by_text.pdf` | in: `wave_2_dfs.RDS` | `main_demographics.tex` ✓; `main_missingness_by_text.pdf` ✓; `main_histogram_by_text.pdf` ✓; `main_ethnicity.tex` ✗ (not even present in `_tex/tables/`); `main_political_leaning.tex` ✗ (not present in `_tex/tables/`) | `main_demographics.tex`: Main Study Methods, `_tex/sections/31_main_methods.tex:7`. `main_missingness_by_text.pdf`: Main Study Results §Reliability, `_tex/sections/32_main_results.tex:52`. `main_histogram_by_text.pdf`: §Rating Distribution by Text Type, `32_main_results.tex:119` | Keep |

### `_notebooks/participant/01_quiz_results/`

| Notebook | Likely runs? (static) | Figure/table outputs | Data outputs | In `_tex/`? | Section / approx. lines | Recommendation (provisional) |
|---|---|---|---|---|---|---|
| `01_quiz_results.qmd` | ✓ likely (`pilot_2_dfs.RDS`, `wave_2_quiz_df.RDS` both exist in `_data/_participant_scores/wave_2/`) | `quiz_correctness_by_study.pdf`; `pilot_quiz_correctness.tex`; `main_quiz_correctness.tex` | in: `pilot_2_dfs.RDS`, `wave_2_quiz_df.RDS` | `quiz_correctness_by_study.pdf` ✓; `pilot_quiz_correctness.tex` ✗; `main_quiz_correctness.tex` ✗ — but see `~ rename?` below | `quiz_correctness_by_study.pdf`: Pilot Results §Exploring Quiz Results, `_tex/sections/22_pilot_results.tex:35` | Keep — see rename note |

`~ rename?`: `_tex/sections/94_appendix_D.tex:6` cites `\input{tables/quiz_correctness_by_study}`.
`_tex/tables/quiz_correctness_by_study.tex` exists on disk and is captioned "Quiz Item
Correctness - Pilot and Main Studies" (`\label{tab:quiz_correctness_combined}`) — it
reads as a hand-merged combination of this notebook's two actual outputs,
`pilot_quiz_correctness.tex` and `main_quiz_correctness.tex`, neither of which this
notebook (or any other) produces under the combined name. Recorded, not fabricated:
I did not find any notebook that writes `quiz_correctness_by_study.tex` literally.

### `_notebooks/participant/02_subjectivity_confidence/`

| Notebook | Likely runs? (static) | Figure/table outputs | Data outputs | In `_tex/`? | Section / approx. lines | Recommendation (provisional) |
|---|---|---|---|---|---|---|
| `02_main_subjectivity_confidence.qmd` | ✓ likely (`wave_2_dfs.RDS` exists in `_participant_scores/wave_2/`) | `main_confidence_subjectivity.pdf` | in: `wave_2_dfs.RDS` | ✓ | Confidence and Perceived Subjectivity, `_tex/sections/95_appendix_E.tex:19` | Keep |
| `02_pilot_subjectivity_confidence.qmd` | ✓ likely (`pilot_2_dfs.RDS` exists) | `pilot_confidence_subjectivity.pdf` | in: `pilot_2_dfs.RDS` | ✓ | Confidence and Perceived Subjectivity, `_tex/sections/95_appendix_E.tex:7` | Keep |

### `_notebooks/participant/03_inter_rater_reliability/`

| Notebook | Likely runs? (static) | Figure/table outputs | Data outputs | In `_tex/`? | Section / approx. lines | Recommendation (provisional) |
|---|---|---|---|---|---|---|
| `01_pilot_2_estimate_boot_reliabilities.Rmd` | ✓ likely (`pilot_2_dfs.RDS` exists) | none | in: `pilot_2_dfs.RDS`; out: `pilot_2_lyrics_subsample_list.RDS`, `pilot_2_speeches1_subsample_list.RDS`, `pilot_2_speeches2_subsample_list.RDS`, `pilot_2_lyrics_by_row_dfs.RDS`, `pilot_2_speeches1_by_row_dfs.RDS`, `pilot_2_speeches2_by_row_dfs.RDS` (all exist in `_data/_intermediary_data/bootstrapped_ICC/`, feeding `02_*` and `03_*`) | n/a | Unsure (no figure/table outputs) |
| `02_pilot_2_estimate_summary_reliabilities.Rmd` | ✓ likely (`pilot_2_dfs.RDS` and the three `*_subsample_list.RDS` files all exist) | none | in: `pilot_2_dfs.RDS`, subsample lists; out: `pilot_2_likert_summary_dfs.RDS`, `pilot_2_likert_summary_icc1_dfs.RDS` (both exist, feeding `03_*`) | n/a | Unsure |
| `03_pilot_rater_number_estimation.qmd` | ✓ likely (all six upstream `.RDS` inputs exist) | `pilot_reliability_by_n.pdf`; `pilot_lyrics_reliability_by_value.pdf` (line 222; commented duplicate at line 291, tagged `(save commented — render-time skip)`); `pilot_speeches1_reliability_by_value.pdf` (line 225; commented dup at 319); `pilot_speeches2_reliability_by_value.pdf` (line 228; commented dup at 345); `pilot_lyrics_icc2_reliability_by_value.pdf`; `pilot_speeches1_icc2_reliability_by_value.pdf`; `pilot_speeches2_icc2_reliability_by_value.pdf` | in: six `.RDS` files listed above | `pilot_reliability_by_n.pdf` ✓; `pilot_lyrics_reliability_by_value.pdf` ✓; `pilot_speeches1_reliability_by_value.pdf` ✓; `pilot_speeches2_reliability_by_value.pdf` ✓; the three `*_icc2_*` files ✗ (not even present in `_tex/images/`) | `pilot_reliability_by_n.pdf`: Pilot Results §Estimating the number of raters, `22_pilot_results.tex:11`. `pilot_lyrics_reliability_by_value.pdf`: §Conclusion (subsubsection), `22_pilot_results.tex:49`. `pilot_speeches1_reliability_by_value.pdf`: same subsubsection, `:59`. `pilot_speeches2_reliability_by_value.pdf`: same, `:69` | Keep |
| `04_pilot_rater_lmer_analysis.qmd` | ✓ likely (`pilot_2_dfs.RDS` exists) | none | in: `pilot_2_dfs.RDS` | n/a | Unsure |
| `04_wave_2_estimate_summary_reliabilities.Rmd` | ✓ likely (`wave_2_dfs.RDS` exists in `_participant_scores/wave_2/`) | none | in: `wave_2_dfs.RDS`; out: `wave_2_subsample_ethnicity_ICC_dfs.RDS`, `wave_2_subsample_spectrum_ICC_dfs.RDS` (both exist in `_intermediary_data/`, feeding `05_*`) | n/a | Unsure |
| `05_wave_2_reliabilities.Rmd` | ✓ likely (both `*_ICC_dfs.RDS` inputs exist) | `main_lyrics_reliability_by_value_by_ethnicity.pdf`; `main_speeches_reliability_by_value_by_ethnicity.pdf`; `main_speeches_reliability_by_value_by_spectrum.pdf` | in: `wave_2_subsample_ethnicity_ICC_dfs.RDS`, `wave_2_subsample_spectrum_ICC_dfs.RDS` | all three ✓ | All three: Main Study Addendum §Reliability by Rater Characteristic, `_tex/sections/96_appendix_F.tex:12`, `:22`, `:32` | Keep |
| `06_wave_2_precision.Rmd` | ✓ likely (`wave_2_dfs.RDS` exists) | none | in: `wave_2_dfs.RDS` | n/a | Unsure |

### `_notebooks/participant/04_mds_plots/`

| Notebook | Likely runs? (static) | Figure/table outputs | Data outputs | In `_tex/`? | Section / approx. lines | Recommendation (provisional) |
|---|---|---|---|---|---|---|
| `2_MDS_plots.Rmd` | ✓ likely (`wave_2_dfs.RDS` exists) | `main_SSVS_self.pdf`; `main_SSVS_text.pdf` | in: `wave_2_dfs.RDS` | both ✓ | `main_SSVS_self.pdf`: Main Study Results §SSVS self-reports, `32_main_results.tex:8`. `main_SSVS_text.pdf`: §Rating Distribution by Text Type, `32_main_results.tex:133` | Keep |

### `_notebooks/participant/05_variable_importance/`

| Notebook | Likely runs? (static) | Figure/table outputs | Data outputs | In `_tex/`? | Section / approx. lines | Recommendation (provisional) |
|---|---|---|---|---|---|---|
| `0_data_format.Rmd` | ✓ likely (`wave_2_dfs.RDS`, `public_lyrics_df.RDS`, `speech_df.RDS` all exist) | none | in: `wave_2_dfs.RDS` (`_participant_scores/wave_2/`), `public_lyrics_df.RDS`, `speech_df.RDS` (`_primary_data/`); out: `wave_2_dfs.RDS` (a *different* file, written to `_intermediary_data/` — same basename, different folder; exists, feeding several downstream notebooks) | n/a | Unsure (no figure/table outputs) |
| `1_model_selection.Rmd` | ✓ likely (`_intermediary_data/wave_2_dfs.RDS` exists) | none | in: `wave_2_dfs.RDS` (`_intermediary_data/`); out: `wave_2_lyrics_mods.RDS`, `wave_2_speeches_mods.RDS` (written twice, lines 79 and 93, from different variables to the same filename — both exist on disk, but the second write appears to silently overwrite the first; flagged as a static code observation, not verified at runtime) | n/a | Unsure |
| `2_preliminary_analysis.Rmd` | ✓ likely (`_intermediary_data/wave_2_dfs.RDS` and `models/wave_2_text_presence_mod.RDS` exist) | `main_value_presence_by_text.tex`; `main_emmeans_text_by_value.tex`; `main_emmeans_text_by_value.PDF` | in: `wave_2_dfs.RDS`, `wave_2_text_presence_mod.RDS`; a `saveRDS(mod, ...)` at line 51 and a `saveRDS(text_mod, ...)` at line 125 are both commented out (`(save commented — render-time skip)`) | `main_value_presence_by_text.tex` ✓; `main_emmeans_text_by_value.tex` ✓; `main_emmeans_text_by_value.PDF` ✓ | `main_value_presence_by_text.tex` and `main_emmeans_text_by_value.tex`: Main Study Addendum §Value Rating Presence and Distribution by Text Type, `96_appendix_F.tex:45`, `:49`. `main_emmeans_text_by_value.PDF`: same section, `:54` | Keep |
| `3_lmer_model_estimation.Rmd` | ✓ likely (`_intermediary_data/wave_2_dfs.RDS` exists) | `main_speech_model_comparisons.tex`; `main_speech_model_specifications.tex` | in: `wave_2_dfs.RDS`; several `saveRDS(...)` calls for ANOVA/model/eta objects are commented out throughout (lines 49, 65, 70, 79, 87, 92, 102, 144, 145, 371, 377, 385 — tagged `(save commented — render-time skip)`), and the notebook then reads those same `.RDS` files back in as if they exist (all do exist in `_data/_intermediary_data/models/`) | both ✓ | Both: Main Study Results §lyrics Models, `32_main_results.tex:167`, `:168` (also cited again in the commented-out `97_appendix_G.tex:37-38`, moot per the appendix-G convention above) | Keep |
| `4_lmer_analysis.Rmd` — archived 2026-07-23 as `archive/4_lmer_analysis_2026-07-23.Rmd` (`BRIEF_split_lmer_analysis.md`, Step 3); content split into `4_lyric_model_analysis.Rmd` and `5_speech_model_analysis.Rmd`, neither yet audited under this document's methodology | ✓ likely (`_intermediary_data/wave_2_dfs.RDS` and `_primary_data/lyrics_df.RDS` exist) | `wave_2_lyrics_mod_1_anova.tex`; `wave_2_lyrics_mod_2_anova.tex`; `wave_2_speeches_mod_1a_anova.tex`; `wave_2_speeches_mod_1b_anova.tex`; `wave_2_speeches_mod_4_anova.tex`; `main_emmeans_text_by_ethnicity_spectrum.pdf`; `main_emmeans_lyrics_by_ethnicity_value.pdf`; `main_emmeans_speeches_by_ethnicity_spectrum_by_value.pdf`; `main_emmeans_speeches_by_ethnicity_spectrum.pdf` (line 647, commented — tagged); `main_emmeans_speeches_by_ethnicity.pdf` (line 660, the active replacement for the line-647 figure); `main_emmeans_spectrum_ethnicity_by_party.pdf` (line 675 commented, line 685 active — same filename both times); `wave_2_speeches_ethnicity_value_contrasts.tex` | in: `wave_2_dfs.RDS`, `lyrics_df.RDS`; several intermediate model/anova `.RDS` reads, all present in `_intermediary_data/models/` | `wave_2_lyrics_mod_1_anova.tex` ✓; `wave_2_lyrics_mod_2_anova.tex` ✓; `wave_2_speeches_mod_4_anova.tex` ✓; `wave_2_speeches_ethnicity_value_contrasts.tex` ✓; `main_emmeans_text_by_ethnicity_spectrum.pdf` ✓; `main_emmeans_lyrics_by_ethnicity_value.pdf` ✓; `main_emmeans_speeches_by_ethnicity_spectrum.pdf` ✓; `main_emmeans_spectrum_ethnicity_by_party.pdf` ✓; `wave_2_speeches_mod_1a_anova.tex` ✗; `wave_2_speeches_mod_1b_anova.tex` ✗; `main_emmeans_speeches_by_ethnicity_spectrum_by_value.pdf` ✗; `main_emmeans_speeches_by_ethnicity.pdf` ✗ — but see `~ rename?` below | `wave_2_lyrics_mod_1_anova.tex`: Main Study Results §Pre-registered vs. interpreted models, `32_main_results.tex:257`. `wave_2_lyrics_mod_2_anova.tex`: §Multiverse analysis, `:189`. `wave_2_speeches_mod_4_anova.tex`: subsubsection speeches, `:211`. `wave_2_speeches_ethnicity_value_contrasts.tex`: subsubsection speeches, `:241`. `main_emmeans_text_by_ethnicity_spectrum.pdf`: subsubsection speeches, `:218`. `main_emmeans_lyrics_by_ethnicity_value.pdf`: subsubsection lyrics, `:200`. `main_emmeans_speeches_by_ethnicity_spectrum.pdf`: subsubsection speeches, `:230`. `main_emmeans_spectrum_ethnicity_by_party.pdf`: subsubsection speeches, `:246` | Keep — see rename note |
| `6_RRA_descriptives.Rmd` (renamed from `5_RRA_descriptives.Rmd`, `BRIEF_split_lmer_analysis.md` Step 3 — no content change) | ✓ likely (`_intermediary_data/wave_2_dfs.RDS` and `_primary_data/lyrics_df.RDS` exist) | `main_lyrics_RRA_by_genre.tex`; `main_lyrics_RRA_genre.pdf`; `main_speeches_RRA.pdf` (line 319, commented — tagged); `main_values_RRA.pdf`; `main_speeches_RRA_characteristic_party.pdf` | in: `wave_2_dfs.RDS`, `lyrics_df.RDS` | `main_lyrics_RRA_genre.pdf` ✓; `main_values_RRA.pdf` ✓; `main_speeches_RRA_characteristic_party.pdf` ✓; `main_lyrics_RRA_by_genre.tex` ✗ (not even present in `_tex/tables/`); `main_speeches_RRA.pdf` ✗ (not present in `_tex/images/`) | `main_lyrics_RRA_genre.pdf`: Main Study Results §Grounding, `32_main_results.tex:290`. `main_values_RRA.pdf`: same, `:278`. `main_speeches_RRA_characteristic_party.pdf`: same, `:302` | Keep |

`~ rename?` (for `4_lmer_analysis.Rmd`, now archived as `archive/4_lmer_analysis_2026-07-23.Rmd`): `_tex/sections/32_main_results.tex:261` cites
`\input{tables/main_speeches_mod_1a_1b_anova}`. `_tex/tables/main_speeches_mod_1a_1b_anova.tex`
exists on disk, captioned "Type III ANOVA on models: speeches1a and speeches1b" — it
reads as a hand-merged combination of this notebook's `wave_2_speeches_mod_1a_anova.tex`
and `wave_2_speeches_mod_1b_anova.tex`, neither of which is cited under its own name.
No notebook writes the literal combined filename.

### `_notebooks/text/`

| Notebook | Likely runs? (static) | Figure/table outputs | Data outputs | In `_tex/`? | Section / approx. lines | Recommendation (provisional) |
|---|---|---|---|---|---|---|
| `0_survey_flow.qmd` | ✓ likely (no external data inputs; builds a diagram in-memory via DiagrammeR) | `survey_flow.png` (written via `rsvg_png(...)`, not `ggsave`/`gtsave` — same "figure/table output" category, just a different R call) | none | ✗ exact match — but see `~ rename?` below | — | Keep — see rename note |
| `1_lyric_get_genre_tags_api.Rmd` | ✓ likely — reads `public_lyrics_df.RDS` (exists); a second input, `cache_path` (`0_primary_lyric_data/archive/artist_genre_cache.csv`), doesn't exist anywhere in the repo, but the code guards it with `if (file.exists(cache_path)) ... else tibble(...)`, so a missing cache doesn't break the notebook. Note: `SPOTIFY_CLIENT_ID`/`SPOTIFY_CLIENT_SECRET`/`LASTFM_KEY` are literal placeholder strings (`"ENTER_ID"` etc.) — the API calls would fail without real credentials, which file-existence checks can't catch | in: `public_lyrics_df.RDS`; out: `artist_tags.RDS` (exists in `_primary_data/`, feeding `2_lyric_bin_labels.Rmd`); also writes the cache CSV back to the nonexistent `0_primary_lyric_data/archive/` path | n/a | — | Unsure (no figure/table outputs) |
| `2_lyric_bin_labels.Rmd` | ✓ likely (`public_lyrics_df.RDS` and `artist_tags.RDS` both exist) | none | in: `public_lyrics_df.RDS`, `artist_tags.RDS`; out: `lyrics_df.RDS` (exists in `_primary_data/`, feeding `3_appendix_A.qmd` and several `05_variable_importance/` notebooks) | n/a | — | Unsure |
| `3_appendix_A.qmd` | ✓ likely (`lyrics_df.RDS`, `speech_df.RDS`, `wave_2_dfs.RDS`, `pilot_2_dfs.RDS` all exist) | `general_lyric_year.pdf` + `.tex`; `general_lyric_popularity.pdf` + `.tex`; `general_lyric_genre_terms.tex`; `general_lyric_genre.pdf` + `.tex`; `general_lyric_topic.pdf`; `general_speeches_president.pdf`; `general_speeches_party.tex`; `general_wordcount.pdf` | in: `lyrics_df.RDS`, `speech_df.RDS`, `wave_2_dfs.RDS`, `pilot_2_dfs.RDS` | all ✓ (the four `.tex` tables via `\include`, not `\input` — see rule-deviation note at top) | `general_wordcount.pdf`: Stimuli §Word Counts, `91_appendix_A.tex:12`. `general_lyric_year.*`: §Release Date, `:32`/`:39`. `general_lyric_popularity.*`: §Popularity, `:48`/`:56`. `general_lyric_genre_terms.tex`, `general_lyric_genre.*`, `general_lyric_topic.pdf`: §Genre, `:64`/`:69`/`:76`/`:85`. `general_speeches_president.pdf`, `general_speeches_party.tex`: §Political Speech Excerpts, `:107`/`:114` | Keep |

`~ rename?` (for `0_survey_flow.qmd`): `_tex/sections/11_general_methods.tex:41` cites
`images/general_survey_flow.png`. The notebook writes `survey_flow.png` (no `general_`
prefix) to the `images/` folder — differs by one word, matching the brief's rename
pattern. Supporting evidence for the reverse pattern also exists in
`22_pilot_results.tex`: its `\label{fig:pilot_reliability_by_value_lyrics}` (and the
`speeches1`/`speeches2` equivalents) use the word order `reliability_by_value_X`, while
the actual `\includegraphics` on the same lines correctly cites the current filenames
(`pilot_X_reliability_by_value.pdf`) — i.e. this codebase has a history of the label
and the includegraphics/filename drifting out of word-order sync during renames, which
is exactly what looks to have happened here too.

## Missing outputs (cited in `_tex/`, not produced by any notebook)

- **`circle.png`** — cited `_tex/sections/01_introduction.tex:24` (§Personal Values).
  No notebook (in-scope or archived) produces or references this filename. Plausibly a
  manually-created/external illustration (e.g. a values-circle diagram) rather than a
  code-generated figure.
- **`pilot_characteristics.tex`** — cited `_tex/sections/21_pilot_methods.tex:22`
  (§Participants). No notebook produces this filename.
- **`main_characteristics.tex`** — cited `_tex/sections/31_main_methods.tex:11` (Main
  Study Methods). No notebook produces this filename.

(`general_survey_flow.png` looks missing at first pass but is treated as a `~ rename?`
of `survey_flow.png` — see `0_survey_flow.qmd` above, not listed here.)

**New as of 2026-07-23, not yet folded into the table above:** `main_emmeans_text_by_ethnicity_spectrum.pdf`
(Figure 13, cited `32_main_results.tex:218/222/234`) was produced by `4_lmer_analysis.Rmd`
(archived) but the generating chunk was deliberately dropped during
`BRIEF_split_lmer_analysis.md` Step 2 rather than relocated — see recovery coordinates and
rationale in `_briefs/report_manuscript_reference_audit.md`. No notebook currently produces
this file; the manuscript reference is expected to go stale temporarily until a later rework
brief restores a two-panel version.

## Unreferenced outputs (produced by a notebook, not cited in `_tex/`)

- `pilot_ethnicity.tex`, `pilot_political_leaning.tex` — `01_pilot_demographics.qmd`.
  Present in `_tex/tables/` but not `\input`/`\include`d anywhere.
- `main_ethnicity.tex`, `main_political_leaning.tex` — `03_main_descriptives.qmd`. Not
  even present in `_tex/tables/` (not synced), and not cited.
- `pilot_lyrics_icc2_reliability_by_value.pdf`, `pilot_speeches1_icc2_reliability_by_value.pdf`,
  `pilot_speeches2_icc2_reliability_by_value.pdf` — `03_pilot_rater_number_estimation.qmd`.
  Not present in `_tex/images/`, not cited.
- `wave_2_speeches_mod_1a_anova.tex`, `wave_2_speeches_mod_1b_anova.tex` —
  `4_lmer_analysis.Rmd` (archived; now produced by `5_speech_model_analysis.Rmd`).
  Present in `_tex/tables/` but not individually cited (a differently-named merged
  table is — see the `~ rename?` note under that notebook). Per
  `_briefs/report_manuscript_reference_audit.md`: these are the inputs to the
  hand-merged `main_speeches_mod_1a_1b_anova.tex` (Table 10), which is being kept as
  the pre-registered comparator in the appendix — not slated for removal.
- `main_emmeans_speeches_by_ethnicity_spectrum_by_value.pdf`,
  `main_emmeans_speeches_by_ethnicity.pdf` — `4_lmer_analysis.Rmd` (archived; now
  produced by `5_speech_model_analysis.Rmd`). Present in `_tex/images/` (the first) or
  not (the second — not synced), neither cited.
- `main_lyrics_RRA_by_genre.tex` — `6_RRA_descriptives.Rmd` (renamed from
  `5_RRA_descriptives.Rmd`). Not present in `_tex/tables/`, not cited.
- `main_speeches_RRA.pdf` — `6_RRA_descriptives.Rmd` (renamed from
  `5_RRA_descriptives.Rmd`; line 319, commented out). Not present in `_tex/images/`,
  not cited.

## Unsure

- **Entire `_notebooks/machine/llm_pilots/` and `_notebooks/machine/llm_waves/`
  subfolders** (9 notebooks) — every one reads from
  `here("_data","_intermediary_data","wave_2")`, a directory that doesn't exist on
  disk (only `bootstrapped_ICC/`, `demog_dfs/`, `models/`, `spec_curves/`, and files
  exist directly under `_intermediary_data/`), and/or from `_data/_raw_data/`, which
  doesn't exist anywhere in the repo. Marked `✗ broken` above. Since AGENTS.md flags
  this whole folder's status as "uncertain," I haven't guessed whether this reflects
  an abandoned pipeline, a path that changed elsewhere, or files that were never
  committed — recording the fact, not the cause.
- **`main_r2_table.tex`, `main_yhat_plots.pdf`** — both exist in `_tex/tables/` and
  `_tex/images/` respectively, and both are produced only by an *archived* notebook
  (`_notebooks/participant/05_variable_importance/archive/3_model_selection.Rmd`,
  out of audit scope per the brief). Neither is cited in `_tex/sections/`. They don't
  cleanly fit "Missing" (not cited) or "Unreferenced" (producer is out of scope) —
  flagging as leftover copies from an archived analysis path.
- **`quiz_correctness_by_study.tex`** and **`main_speeches_mod_1a_1b_anova.tex`** —
  both are cited, both exist in `_tex/tables/`, and both read as hand-merged
  combinations of two separate notebook-produced tables (see the `~ rename?` notes
  under `01_quiz_results.qmd` and `4_lmer_analysis.Rmd` [archived] above). I can't confirm how
  or when the merge happened since it isn't in any notebook's static code.
- **`main_emmeans_ethnicity_by_party.pdf`, `main_emmeans_spectrum_by_ethnicity_spectrum.pdf`,
  `main_emmeans_spectrum_by_party.pdf`, `main_emmeans_spectrum_ethnicity_by_value.pdf`,
  `pilot_reliability_by_value_lyrics.pdf`, `pilot_reliability_by_value_speeches1.pdf`,
  `pilot_reliability_by_value_speeches2.pdf`** — all sit in `_tex/images/`, none are
  cited in `_tex/sections/`, and none are produced by any in-scope or archived
  notebook I could find. The `pilot_reliability_by_value_*` three are almost certainly
  stale copies from before a filename word-order change (see the `~ rename?` evidence
  under `0_survey_flow.qmd` above, where the LaTeX `\label`s still use this exact
  reversed word order even though the `\includegraphics` calls were updated). The
  `main_emmeans_*` four have no such clear paper trail — recording them as orphaned
  files rather than guessing a source.
- **`01_format_data.Rmd` line 51** — `bind_rows(wave_1_m_df, wave_1_llm_df,
  wave_2_llm_df, wave_2_supervised_df, wave_2_w2v_df)` references three variable names
  (`wave_2_llm_df`, `wave_2_supervised_df`, `wave_2_w2v_df`) that are never assigned in
  this file — only the plural `wave_2_llm_dfs`/`wave_2_supervised_dfs` (list) objects
  are created. This is outside the brief's input-existence proxy (all *file* inputs
  exist), but it's visible from a static read and would very likely break at runtime.
- **`1_model_selection.Rmd` lines 79 and 93** — two different variables
  (`wave_2_speeches_ethnicity_mods`, computed differently at each line) are both
  `saveRDS`'d to the identical path `_data/_intermediary_data/models/wave_2_speeches_mods.RDS`.
  The second write would silently overwrite the first. Not verified at runtime; noted
  because it's a visible static pattern a reviewer would want to see.
- **`1_lyric_get_genre_tags_api.Rmd`** — `SPOTIFY_CLIENT_ID`, `SPOTIFY_CLIENT_SECRET`,
  and `LASTFM_KEY` are hardcoded placeholder strings (`"ENTER_ID"`, `"ENTER_SECRET"`,
  `"ENTER_KEY"`). The file-existence proxy says "likely runs" (its data inputs exist),
  but the live API calls in this notebook cannot succeed without real credentials
  being supplied some other way (env vars at run time, a `.Renviron` not tracked here,
  etc.) — flagging since it's a real gap the static proxy can't see.
