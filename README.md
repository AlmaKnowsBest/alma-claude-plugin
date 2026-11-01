# Alma

Alma is an iPhone app for tracking food and nutrition. This plugin connects Claude to your Alma account and adds six skills that work from your food log. They review your week, suggest meals from your pantry, build a grocery list, check protein on a GLP-1 medication, explain your Alma Score, and log meals after you confirm them.

## What you need

- An Alma account with an active membership. Connecting without one stops at sign-in with a message to start a membership in the Alma app.
- The Alma connector, which this plugin points at `https://mcp.alma.food`. In claude.ai and Cowork, connect it from the plugin's Connectors tab. Claude Code connects to it directly. Either way you sign in with your Alma email.

## Skills

| Skill | Ask something like |
|---|---|
| `weekly-nutrition-review` | "How did I eat this week?" |
| `pantry-meal-plan` | "What can I make from my pantry that gets my fiber up?" |
| `grocery-list-builder` | "Build my grocery list for next week." |
| `glp1-protein-check-in` | "Am I getting enough protein on Zepbound?" |
| `log-a-meal` | "Log two eggs and toast for breakfast." |
| `alma-score-explainer` | "Why did my Alma Score drop?" |

In Claude Code the skills are also available as slash commands, for example `/alma:weekly-nutrition-review`.

## How it handles your data

The plugin is a set of instructions plus the address of the Alma connector. It runs no code and stores nothing itself.

When you use it, Claude reads your Alma data through `mcp.alma.food`: profile and timezone, goals, meals and nutrition, Alma Score, weight, workouts, energy check-ins, synced Apple Health metrics, medication and supplement doses, pantry, grocery list, and saved standard days. What Claude can read or change depends on the permissions you approve when you connect.

Claude writes to your Alma account only after you confirm. That covers logging food, saving or logging a standard day, correcting or deleting a food entry, and recording medication or supplement plans and doses. Medication and supplement amounts always come from you, and the skills tell Claude never to suggest doses or prescriptions. For medical questions, talk to your prescriber or clinician.

The grocery list is read-only through the connector, so the grocery skill gives you the list in the chat.

Read Alma's privacy policy at [alma.food/privacy](https://alma.food/privacy).

## License

MIT. See `LICENSE`.
