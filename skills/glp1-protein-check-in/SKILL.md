---
name: glp1-protein-check-in
description: Check how protein intake and weight are going for a user on a GLP-1 medication such as semaglutide (Ozempic, Wegovy) or tirzepatide (Mounjaro, Zepbound). Use when the user asks whether they eat enough protein on their GLP-1, wants a check-in since starting the medication, or asks how their weight or appetite has changed since their first dose.
---

# GLP-1 protein check-in

Give a supportive check-in on protein and weight since the user started their GLP-1 medication. This skill reads only. It never gives dose advice.

## Steps

1. Call `get_user_profile` for the timezone.
2. Find the start. Call `get_medication_history` with `days=365` and find the earliest dose of the GLP-1 the user names. If the history is empty, ask when they started. Do not guess from other data.
3. Call `get_health_routines` with `start_date` and `end_date` covering the last 31 days, to see any plan they recorded and the taken or missed events. Missing events mean unknown, never missed.
4. Call `get_goals` and `get_meal_data` for the last 14 days with `detail_level="summary"`. Compare average daily protein with their protein goal.
5. Call `get_weight_history` with `days` covering the time since the start (up to 365).
6. Optional: `get_health_metric_history` with `metric_types=["lean_body_mass", "body_fat_percentage"]` when a smart scale syncs, and `get_energy_history` when they mention energy or appetite.

## What good output looks like

- Start with what is going well, for example a steady protein streak or a stable trend.
- Protein: average per day against their goal, and how many logged days reached it. If no protein goal is set, say so and suggest they set one in Alma or with their care team.
- Weight: change since the start date and the recent trend, from the logged weigh-ins only. If lean mass data exists, report it plainly.
- 2-3 easy protein moves that suit a smaller appetite: protein first at meals, small dense portions such as Greek yogurt, eggs, cottage cheese, tofu or fish, and a protein option for days when eating feels hard. Tie them to foods they already log.

## Hard rules

- Never recommend, change, time or comment on a dose, and never infer a prescription. If the user asks a medical question (dose, side effects, stopping, switching), say this is one for their prescriber.
- Do not set calorie or weight targets for them.
- Recording a dose or plan needs an explicit request with the amount, unit and time supplied by the user. Then show what will be written, get a yes, and use `record_health_doses` or `save_health_routine`. Injection units or mL are never converted to mg. These writes need the health permission approved at connect time. If it is missing, tell the user to reconnect Alma and approve it.
- Keep the tone warm and factual. No comments about willpower, "cheating" or how much they ate.
