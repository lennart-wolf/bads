# AI log

Tool: Claude Code (Claude Opus) in VS Code. Me = decide what and why, AI = write code.

## Required bullets

- **Most useful prompt:** "First prepare the data: check plausibility, errors and anything that could bias the evaluation, save it to a new file. Then do the analysis, cluster countries into groups with names a management audience understands. Then review the findings and build the shortlist as a table with confidence and reasoning, add graphs where they help."
- **AI got wrong / did not question:** AI read section 8.7 of the case notebook as a leftover solution. Me: no, it's only a template for presenting. Also: the AI first wrote "Ward agrees almost completely" and put Brazil among the emerging economies. The real numbers were Ward 37 of 44 countries, and Brazil sits in "Advanced economies".
- **Changed after checking:** the case says "no missing values", but the check found broken values: Myanmar trade about 0 % of GDP, Nigeria inflation 104 %. Both imputed and flagged. Cluster texts rewritten to match the real numbers.
- **Still my judgement, not the data's:** the programme rules (A/B/C), Liberia vs. Guinea for the last spot, and k = 4 chosen for interpretability.

## Process (caveman)

1. Me: "tl;dr task." AI: reads notebook, explains case.
2. Me: "all files English. 8.7 = how to present, new notebook. prep data, check, save. cluster with easy names. shortlist table + confidence + graphs. caveman log."
3. AI: check data. No NaN, no duplicates. But: Myanmar trade 0.1 %, Nigeria inflation 104 %, Haiti quake 2010. Six crisis countries missing (Somalia, South Sudan, Ethiopia, ...).
4. AI: log income/GDP/child mortality, winsorise trade/inflation/health, standardise → `data/`.
5. AI: PCA. PC1 = need (53 %). Cluster on PC1 to PC4.
6. AI: k-means, try k 2 to 8. k = 2 only rich vs. poor. Pick k = 4: High need, Emerging, Open trade, Advanced.
7. AI: stability. Other k, Ward, GMM, bootstrap. Core of the high-need group stays.
8. AI: 1,000 weighting scenarios. Top 15 = most often in the top 15. 7 high confidence, 8 medium.
9. AI: programme = relative weakness inside the high-need group. 10 A, 4 C, 1 B. 5 close calls.
10. AI: board notebook like 8.7. Look at figures, fix labels and legends.

## Files

- `01_data_preparation.ipynb` → `data/country_data_clean.csv`, `data/country_features_model.csv`
- `02_analysis.ipynb` → `results/*.csv`
- `03_board_recommendation.ipynb` = the talk
