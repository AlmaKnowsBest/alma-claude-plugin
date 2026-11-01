---
name: log-a-meal
description: Log food or drinks to the user's Alma account after they confirm the details, or fix or remove an entry they already logged. Use when the user asks to log, track, add or record a meal, snack or drink, asks to log a whole day or a saved standard day, or wants to correct or delete a food entry.
---

# Log a meal

Confirm first, then log. Never call a write tool for food the user only mentioned, or for a suggestion they have not accepted.

## Steps

1. Call `get_user_profile` and use its `timezone` for times and dates.
2. Turn what they said into items. Each item needs name, quantity, unit, calories, protein, carbs and fat. Add `brand` when known, `fiber_g` when known or estimated, and other nutrients in `micronutrients` with the unit in each key (for example `sodium_mg`, `saturated_fat_g`, `vitamin_d_mcg`). Use label values when the user gives them.
3. Drinks: set `hydration_kind` (`water`, `sparkling_water` or `other`) together with `hydration_amount_ml`, and `caffeine_mg` for coffee, tea, energy drinks and similar. Always set both hydration fields or neither.
4. Show a short confirmation table: item, portion, calories, protein, carbs, fat, plus fiber, caffeine or volume where set, and the meal time. Say the numbers are estimates when they are. Ask one question if a portion is unclear. Do not guess it.
5. Log only after a clear yes.

## Which tool

- One meal: `log_food_items` with a new UUID for `client_operation_id`, `user_confirmed: true`, and `items`. Alma names the meal (Breakfast, Lunch, Dinner, Snack) from its time, so when the user names a meal or a time, ask for the time if needed and always send `consumed_at`. Omit it only when they ate just now. Send an ISO time with the UTC offset for the user's timezone, for example `2026-11-01T08:30:00-04:00`. Times can be up to 365 days back or 30 days ahead.
- A whole day or week: `log_food_batch` with every meal and its time confirmed.
- A saved standard day: `get_food_day_templates`, read the template by `template_id`, confirm the dates and contents, then `log_food_day_template` with its `expected_version`.
- Fix an entry: find its `item_id` in `get_meal_data`, confirm the full replacement (portion and all nutrition), then `update_food_entry`. Any nutrient left out becomes unknown.
- Remove an entry: confirm, then `delete_food_entry`.

Corrections and deletions need the edit permission approved at connect time. If the tool refuses, tell the user to reconnect Alma and approve "Edit and delete your food entries".

On a retry of the same request, reuse the same `client_operation_id` and identical payload. A new request gets a new UUID.

## After logging

Reply in one or two lines with what was logged and the meal's totals. Mention that an entry for a future time shows as a planned log. Offer `open_today` if they want to see the day. Keep it neutral and friendly. No comments on whether the meal was good or bad.
