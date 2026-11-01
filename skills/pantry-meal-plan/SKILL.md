---
name: pantry-meal-plan
description: Suggest meals from what the user already has at home that close their nutrient gaps. Use when the user asks what to cook or eat from their pantry or fridge, wants meal ideas for the next few days, or wants a meal plan that helps with protein, fiber or another goal.
---

# Pantry meal plan

Suggest a few meals built from the user's Alma pantry that close the gaps in their recent eating. Write nothing to Alma unless the user confirms.

## Steps

1. Call `get_user_profile` for the timezone and context.
2. Call `get_pantry_items`. If `has_data` is false, ask what they have on hand, or offer meals from common staples and say so.
3. Find the gaps. Call `get_goals`, then `get_meal_data` for the last 7 days (`days=7`, `detail_level="detailed"`). Note average protein, fiber and calories against goal, and any micronutrient gap when `micronutrient_data_available` is true.
4. If the user asks for a whole day, call `get_food_day_templates` to see whether a saved standard day already fits.

## What to suggest

- Give 3 meals by default, or the number the user asks for.
- Build each meal mainly from pantry items. List anything they would need to buy separately, kept short.
- For each meal give: name, ingredients with amounts, a few steps, and estimated calories, protein, carbs, fat and fiber per serving. Label the numbers as estimates.
- Say which gap each meal helps with, for example "about 35 g protein, which covers most of the gap at dinner".
- Respect what the profile and goals say about the user. Do not assume a diet they have not stated.

## If the user wants to log or save

Only act on a clear request, after showing exactly what will be written.

- Log a meal they ate or will eat: follow the `log-a-meal` skill, with `log_food_items`.
- Log a planned day or week: confirm every meal, date, time, portion and nutrition total, then call `log_food_batch`. Dates can be up to 30 days ahead. Tell the user future entries show in Alma as planned logs.
- Save a reusable standard day: confirm the name, each meal's local time (HH:MM) and full food snapshots, then call `save_food_day_template`. Saving does not log food.

Every write needs a new UUID for `client_operation_id` and `user_confirmed: true`. Reuse the same UUID and payload only when retrying the same request.
