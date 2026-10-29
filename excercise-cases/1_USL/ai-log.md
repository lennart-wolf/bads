# AI log

Tool: Claude Code (Claude Opus) in VS Code. I decided what to compute and why; the AI wrote the code.

## Required bullets

- **Most useful prompt:** "First prepare the data: check plausibility, errors and anything that could bias the evaluation, and save it to a new file. Then do the analysis and cluster the countries into groups with names a management audience understands. Then review the findings and build the shortlist as a table with confidence and reasoning, with graphs where they help."
- **What the AI got wrong or did not question:** The AI took section 8.7 of the case notebook for a leftover solution. It is only a template for the presentation. In its first draft it also wrote that Ward clustering "agrees almost completely" and listed Brazil as an emerging economy. The numbers showed something else: Ward agrees on 37 of 44 countries, and Brazil is in the "Advanced economies" group.
- **What I changed after checking:** The case says the data has no missing values. The plausibility check still found two errors: Myanmar's trade is about 0 % of GDP, and Nigeria's inflation is 104 %. Both were replaced with typical values from similar countries and flagged. The texts about the clusters were corrected to match the real numbers.
- **What is my judgement, not the data's:** the rules for assigning programmes A, B and C, choosing Liberia over Guinea for the last spot, and using four groups because they are easier to explain.

## How the work went

1. I asked for a short summary of the task. The AI read the notebook and explained the case.
2. My instructions: all files in English, a new notebook for the presentation, data preparation first, clusters with easy names, a shortlist table with confidence and graphs, and a short log.
3. **Data check:** no missing values and no duplicates, but Myanmar's trade data and Nigeria's inflation are clearly wrong, and Haiti's values reflect the 2010 earthquake. Six crisis countries (e.g. Somalia, South Sudan, Ethiopia) are not in the data at all.
4. **Data preparation:** large money values (income, GDP) were put on a log scale, extreme values were capped and all indicators were brought to the same scale. The result was saved in `data/`.
5. **Need:** PCA showed one main dimension that explains 53 % of the differences between countries. It became the need index.
6. **Clusters:** k-means with 2 to 8 groups was tested. Two groups only split rich from poor, so I chose four: High need, Emerging economies, Open trade economies, Advanced economies.
7. **Stability:** different numbers of groups, two other algorithms and 300 resampled datasets all kept the same core of high-need countries.
8. **Shortlist:** the selection was repeated with 1,000 different weightings of the indicators. The 15 countries that made the top 15 most often were chosen: 7 with high and 8 with medium confidence.
9. **Programmes:** each country gets the programme that matches its biggest relative weakness compared with the other high-need countries. Result: 10 × A, 4 × C, 1 × B, with 5 close calls.
10. **Presentation:** a board notebook based on the 8.7 template. All figures were checked visually; labels and legends were fixed.

## Files

- `01_data_preparation.ipynb` → `data/country_data_clean.csv`, `data/country_features_model.csv`
- `02_analysis.ipynb` → `results/*.csv`
- `03_board_recommendation.ipynb` → the talk
