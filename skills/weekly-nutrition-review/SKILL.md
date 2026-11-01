---
name: weekly-nutrition-review
description: Review the user's last week of eating from their Alma log. Use when the user asks how they ate this week, wants a weekly recap or check-in, asks whether they are hitting their protein, fiber or calorie goals, or asks what to change next week.
---

# Weekly nutrition review

Read the week from Alma, compare it with the user's goals, and give 2-3 specific moves for next week. This skill only reads. Do not call any write tool.

## Steps

1. Call `get_user_profile`. Use its `timezone` for every date below.
2. Pick the range: the 7 full days ending yesterday in the user's timezone, as `start_date` and `end_date` (YYYY-MM-DD). If the user asks to include today, end on today and say today is still in progress.
3. Call these with the same range:
   - `get_goals` (no arguments).
   - `get_meal_data` with `detail_level="detailed"`.
   - `get_alma_score_data` with `detail_level="detailed"`.
4. Optional, only when it helps the answer: `get_weight_history` with `days=30` for the trend, `get_workout_history` for the same range when the user trains, `get_energy_history` when they mention energy.

## How to read the data

- Compare averages against the user's own goals from `get_goals`. When there is no goal for a nutrient, say so and label any number you use as a general reference, not their target.
- Count only days with logged meals (`days_with_data`). Do not treat an unlogged day as a zero-intake day, and do not comment on how often they logged.
- Micronutrients: check the top-level `micronutrient_data_available` flag first. If it is false, skip micronutrient gaps. If it is true, use `micronutrient_coverage_pct` to say how complete the picture is, and only name a gap when coverage is reasonable.
- Alma Score: report the week's level and which of the 10 categories helped or held it back. Tie each point to foods the user actually logged.

## What good output looks like

Keep it short and lead with what went well.

1. One line on the week: days logged, average calories and protein against goal, Alma Score.
2. Wins: 1-2 things they did that moved them toward a goal, with the foods behind them.
3. Gaps: protein, fiber and any clear micronutrient gap, each with the number and the goal.
4. Next week: 2-3 moves, each one concrete and tied to a gap. Name a food, a meal and a quantity, for example "add a cup of lentils to two lunches, about 15 g of fiber each time". Prefer foods they already eat or have logged.

Frame every point as something to add or try. Never scold, rank days as good or bad, or comment on logging gaps. If the week has fewer than 3 logged days, say the picture is partial and keep advice light.
