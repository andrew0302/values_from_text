# ERRORS — Phase 0 Diagnostic Baseline

**Summary:** 23 ✅ pass · 3 ❌ fail (independent) · 0 ⛔ blocked-by-upstream · 0 ⏱ long-runners

Run: 2026-08-14 · HEAD `a160c6f` · tag `baseline-pre-phase0`  
R 4.4.2 · macOS aarch64 · renv absent · all caches present (no from-scratch refits)

---

| # | Notebook | Status | Runtime | Error (file:line, message) | Note |
|---|----------|--------|---------|---------------------------|------|
| 1 | `_notebooks/text/0_survey_flow.qmd` | ✅ pass | 3s | — | |
| 2 | `_notebooks/text/1_lyric_get_genre_tags_api.Rmd` | ❌ fail | 5s | chunk 1 (setup→unnamed-chunk-1): `get_spotify_access_token()` — "Could not authenticate: Invalid client" | Credentials are placeholder values ("ENTER_ID"/"ENTER_SECRET"). `artist_tags.RDS` already cached; this notebook need not run again unless the cache is stale. |
| 3 | `_notebooks/text/2_lyric_bin_labels.Rmd` | ✅ pass | 1s | — | |
| 4 | `_notebooks/participant/00_descriptives/00_pilot_demographics_data_format.qmd` | ✅ pass | 2s | — | |
| 5 | `_notebooks/participant/03_inter_rater_reliability/01_pilot_2_estimate_boot_reliabilities.Rmd` | ✅ pass | 252s | — | Slowest notebook; bootstraps from cached subsamples. |
| 6 | `_notebooks/participant/03_inter_rater_reliability/02_pilot_2_estimate_summary_reliabilities.Rmd` | ✅ pass | 4s | — | |
| 7 | `_notebooks/participant/05_variable_importance/0_data_format.Rmd` | ✅ pass | 2s | — | |
| 8 | `_notebooks/participant/03_inter_rater_reliability/04_wave_2_estimate_summary_reliabilities.Rmd` | ✅ pass | 21s | — | |
| 9 | `_notebooks/participant/00_descriptives/01_pilot_demographics.qmd` | ❌ fail | 2s | Lines 21-26 (chunk 2): `object 'pilot_2_demog_df' not found` in `nrow(pilot_2_demog_df)` | Notebook loads `pilot_2_demog_dfs` (plural list) from RDS but then references `pilot_2_demog_df` (singular df) which is never assigned. Both RDS files exist on disk; the singular one is not read. |
| 10 | `_notebooks/participant/00_descriptives/02_pilot_lyrics_questions.qmd` | ✅ pass | 2s | — | |
| 11 | `_notebooks/participant/00_descriptives/03_main_descriptives.qmd` | ✅ pass | 5s | — | |
| 12 | `_notebooks/participant/01_quiz_results/01_quiz_results.qmd` | ✅ pass | 3s | — | |
| 13 | `_notebooks/participant/02_subjectivity_confidence/02_pilot_subjectivity_confidence.qmd` | ✅ pass | 3s | — | |
| 14 | `_notebooks/participant/02_subjectivity_confidence/02_main_subjectivity_confidence.qmd` | ✅ pass | 11s | — | |
| 15 | `_notebooks/participant/03_inter_rater_reliability/03_pilot_rater_number_estimation.qmd` | ❌ fail | 5s | Lines 354-369 (chunk 12): `could not find function "plot_summary_by_metric"` | Helper function missing from notebook environment. Function is called inside `.main()` after 22/31 chunks complete. Likely defined in an un-sourced file or removed during an earlier refactor. |
| 16 | `_notebooks/participant/03_inter_rater_reliability/04_pilot_rater_lmer_analysis.qmd` | ✅ pass | 6s | — | |
| 17 | `_notebooks/participant/03_inter_rater_reliability/05_wave_2_reliabilities.Rmd` | ✅ pass | 3s | — | |
| 18 | `_notebooks/participant/03_inter_rater_reliability/06_wave_2_precision.Rmd` | ✅ pass | 4s | — | |
| 19 | `_notebooks/participant/04_mds_plots/2_MDS_plots.Rmd` | ✅ pass | 4s | — | |
| 20 | `_notebooks/participant/05_variable_importance/1_preliminary_analysis.Rmd` | ✅ pass | 4s | — | |
| 21 | `_notebooks/participant/05_variable_importance/2_lyric_model_selection.Rmd` | ✅ pass | 3s | — | |
| 22 | `_notebooks/participant/05_variable_importance/3_speech_model_selection.Rmd` | ✅ pass | 92s | — | Re-saves `wave_2_speeches_combined_mod.RDS` from cached rung-1 model. |
| 23 | `_notebooks/participant/05_variable_importance/4_lyric_model_analysis.Rmd` | ✅ pass | 138s | — | Runs emmeans over cached lyric models. |
| 24 | `_notebooks/participant/05_variable_importance/5_speech_model_analysis.Rmd` | ✅ pass | 53s | — | Reads old `wave_2_speeches4_mod.RDS` (known Phase 3 bug); passes because cache exists. |
| 25 | `_notebooks/participant/05_variable_importance/6_RRA_descriptives.Rmd` | ✅ pass | 6s | — | |
| 26 | `_notebooks/text/3_appendix_A.qmd` | ✅ pass | 5s | — | |

---

## Failures to fix in Phase 1

### ❌ #9 — `01_pilot_demographics.qmd`
**Fix:** Add `pilot_2_demog_df <- readRDS(here("_data", "_intermediary_data", "demog_dfs", "pilot_2_demog_df.RDS"))` to the setup chunk (the singular-df RDS already exists; it's just not being loaded).

### ❌ #15 — `03_pilot_rater_number_estimation.qmd`
**Fix:** Locate or restore the `plot_summary_by_metric()` function. It is called inside `.main()` at chunk 12 (lines 354-369). Check git history or archive notebooks for where it was defined.

### ❌ #2 — `1_lyric_get_genre_tags_api.Rmd`
**Decision needed:** The `artist_tags.RDS` cache is complete and this notebook requires live Spotify/Last.fm credentials to run. Options: (a) accept as permanently cache-dependent and document that real credentials are needed to re-run it, or (b) restructure the notebook to skip the API fetch when `artist_tags.RDS` is already present. Not a blocking issue for other notebooks.
