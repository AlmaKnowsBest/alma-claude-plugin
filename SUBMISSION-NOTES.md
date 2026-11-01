# Submission notes

Status of the Alma plugin against the Claude plugin directory's pre-submission checklist, as of 2026-11-01. The plugin folder is the repository root. Nothing has been pushed or submitted.

## Checklist

| Check | Status |
|---|---|
| Folder contains `.claude-plugin/plugin.json` | Pass |
| One plugin per submission | Pass, single plugin at the root |
| Component paths and files stay inside the plugin folder | Pass, no custom paths |
| Regular files only, no symlinks, submodules or LFS | Pass |
| No `.DS_Store`, `Thumbs.db`, `desktop.ini`, `__MACOSX` | Pass, `.gitignore` blocks `.DS_Store` |
| File and folder names valid on Windows and macOS | Pass |
| Path folders use only letters, digits, `.`, `-` and `_` | Pass |
| No `export-ignore`, `export-subst` or `filter` in `.gitattributes` | Pass, no `.gitattributes` |
| Repo under size and file-count limits; every file under 256 KiB | Pass, all text, a few KB each |
| `name` lowercase ASCII with hyphens | Pass, `alma` |
| Name built on our own product, no reserved word | Pass, `alma` is our brand. Not checked: whether another publisher already uses `alma` |
| `displayName` and `author.name` in one script, no look-alikes | Pass, `Alma` and `Alma` |
| Component keys spelled as the reference does | Pass, components found by default folders |
| `description`, `author`, `version` set | Pass |
| README of 40+ words outside code blocks, says what it does, how to use it, what data it sends | Pass |
| `LICENSE` file or `license` field | Pass, both (MIT) |
| Only text files and complete images | Pass, no binaries |
| MCP servers declared by `url`, no `.mcpb` or `.dxt` | Pass |
| No package launchers or package-source config | Pass, none |
| No credentials in any file; no reading credentials from the user's environment | Pass, OAuth happens on the server |
| `.mcp.json` valid; remote server has `type` `http` and an `https` URL | Pass, `https://mcp.alma.food`, the same URL as the listed Alma connector (MCP is served at `/`) |
| Hooks valid | N/A, no hooks |
| Skills have valid YAML front matter with a single-string `description` | Pass, 6 skills, folder names match `name` |
| Component folders and files spelled exactly | Pass, `skills/<name>/SKILL.md` |
| No top-level `bin/` | Pass |
| README describes everything the plugin runs, sends or fetches | Pass, no code runs; data goes only to the user's Alma account through `mcp.alma.food` |
| `claude plugin validate .` | Pass. Icon added at `.claude-plugin/icon.png` (iOS app icon, 512 px) |
| Portal Validate and security scan | Not run, needs the public repo |
| Behavior test on real prompts (`claude plugin eval`, claude.ai upload) | Not run |

## Open asks for Rami

1. Approve creating a public GitHub repository for this folder and pushing it. The portal validates from a repository.
2. Approve submitting the plugin from the developer portal. The Alma connector listing edit is still in review and was not touched.
3. Pick the listing icon. It is set only once, on the first save or submit in the portal. The candidate is the current iOS app icon, `alma-ios/Alma/Assets.xcassets/AppIcon.appiconset/Prod - Light.png` (1024 px PNG). It would go at `.claude-plugin/icon.png`.
4. Answer the portal's data-handling questions. Suggested answers: the plugin stores nothing and runs no code; the connector reads and, after the member confirms, writes the member's own Alma data (profile, goals, meals, Alma Score, weight, workouts, energy check-ins, Apple Health metrics, medication and supplement doses, pantry, grocery list, saved standard days); access is by OAuth with scopes the member approves; an Alma membership is required; privacy policy at https://alma.food/privacy.
5. Confirm the GLP-1 skill description may name Ozempic, Wegovy, Mounjaro and Zepbound. It helps the skill trigger when people use brand names. Remove them if you want generic names only.
