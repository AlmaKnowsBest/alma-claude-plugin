---
name: grocery-list-builder
description: Build a shopping list from the user's nutrient gaps, their Alma pantry and their existing Alma grocery list. Use when the user asks for a grocery or shopping list, asks what to buy this week, or wants a list for a meal plan.
---

# Grocery list builder

Build one grouped shopping list in the chat. The Alma connector can read the grocery list but cannot add to it, so never say items were added to Alma.

## Steps

1. Call `get_user_profile` for the timezone.
2. Call `get_grocery_list` with `include_completed=false` to see what is already on their list.
3. Call `get_pantry_items` to see what they already have.
4. Find the gaps: `get_goals`, then `get_meal_data` for the last 7 days with `detail_level="summary"`, or `detailed` when you need foods or micronutrients. If a meal plan from this chat exists, use its ingredients instead.

## Build the list

- Skip anything already in the pantry unless the plan needs more of it.
- Keep items that are already on their Alma grocery list and mark them "(on your list)", so the user sees one complete list.
- Add items that close the gaps, for example beans, oats or berries for fiber, or eggs, yogurt, tofu or fish for protein. Prefer foods they already log.
- Give quantities for a week, or for the meal plan when there is one.
- Group by store section: produce, protein, dairy and eggs, grains and bread, pantry and canned, frozen, other.

## What good output looks like

- One line on what the list is built for, for example "covers 4 dinners and adds about 10 g fiber a day".
- The grouped list as plain checkboxes, ready to copy.
- A short note on which items fill which gap.

Keep it to the list. Do not shame past choices or mention foods to avoid unless the user asks.
