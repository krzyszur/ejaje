# Contributing

Everything we build for AI tools (skills, plugins, instruction files) lives here. Nothing should exist only in a local folder or a chat.

## Where things go

| What | Path |
|---|---|
| Skill | `plugins/<plugin>/skills/<name>/SKILL.md` |
| Plugin manifest | `plugins/<plugin>/.claude-plugin/plugin.json` |
| Instructions for a tool | `instructions/<tool>/` (e.g. `instructions/claude-code/CLAUDE.md`) |

- Names are lowercase kebab-case (`session-planner`, not `SessionPlanner`).
- A skill belongs to a plugin. Put it in an existing plugin when it fits the theme; otherwise create a new plugin.

## Adding a skill

1. Create `plugins/<plugin>/skills/<name>/SKILL.md` with frontmatter:
   ```markdown
   ---
   name: <name>
   description: <what it does and when to use it — this is what triggers the skill>
   ---
   ```
2. Keep `SKILL.md` short; move long reference material to `references/` and code to `scripts/` in the same folder.
3. No secrets, tokens, personal data or machine-specific absolute paths.

## Adding a plugin

1. Create `plugins/<plugin>/.claude-plugin/plugin.json`:
   ```json
   {
     "name": "<plugin>",
     "description": "<one line>",
     "version": "0.1.0"
   }
   ```
2. Register it in `.claude-plugin/marketplace.json` under `plugins`:
   ```json
   { "name": "<plugin>", "source": "./plugins/<plugin>", "description": "<one line>" }
   ```
3. Bump `version` in `plugin.json` whenever the plugin's skills change.

## Adding instructions

Put the file under `instructions/<tool>/` using that tool's own file name (`CLAUDE.md`, `AGENTS.md`, `.cursorrules`, …). Add a dated line with the reason for any new rule, e.g. `(added 2026-11-15 — why: …)`.

## Review checklist

- [ ] Correct path and naming
- [ ] `description` says when to use it
- [ ] Scripts read: no unexpected network calls, credential/env reads or broad shell grants
- [ ] Marketplace and plugin manifests are valid JSON
- [ ] No secrets or personal data

## Commits

- One logical change per commit; message like `skills: add session-planner` or `instructions/claude-code: add cost policy`.
- Small changes may go straight to `main`; use a pull request for anything others should review.
