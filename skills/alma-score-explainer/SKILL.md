---
name: alma-score-explainer
description: Explain the user's Alma Score and what moved it. Use when the user asks what their Alma Score means, why it went up or down, which food categories pull it down, or how to raise it.
---

# Alma Score explainer

The Alma Score runs from 0 to 100 and measures diet quality across 10 categories: vegetables, fruit, whole grains, nuts and legumes, omega-3s, healthy fats, processed meat, sugar, sodium and alcohol. The first six add points. The last four take points away at higher intakes. Do not describe a formula beyond what the tools return.

## Steps

1. Call `get_user_profile` for the timezone.
2. Call `get_alma_score_data` with `detail_level="detailed"` for the period the user asks about (default: the last 7 days). For "why did it change", also call it for the previous period of the same length.
3. Call `get_meal_data` for the same period with `detail_level="detailed"` to find the foods behind each category.
4. If the response says no score data was found, say there are no scored days in that range and suggest a range with logged meals.

## What good output looks like

- The score for the period, and the change from the previous period when asked.
- The 1-2 categories that helped most and the 1-2 that held it back, each tied to foods they logged.
- 2 easy swaps or additions that would lift a weak category, using foods close to what they already eat, for example "add a handful of walnuts to breakfast for nuts and omega-3s".

Frame everything as gains. Do not label foods or days as bad. Read-only: do not call any write tool.
