# Fitness Advisor

A small practice project for Claude Code skills. Two things live here, kept deliberately separate:

1. **`index.html`** — the actual Fitness Advisor app. A single self-contained static page (inline CSS/JS, no build step, no external scripts, no live AI calls). It lets the user set a profile, log food/drink, and see a calorie budget with simple charts, using a small built-in keyword lookup table to guess calories and rule-based logic to compute the daily goal and suggestions.
   - **Constraint: keep everything in `index.html`.** Do not add separate `.js`/`.css` files or a build step — this is intentional, to keep the project trivially hostable (e.g. GitHub Pages) and simple to reason about.
2. **Two Claude Code skills** (below) — used by chatting with Claude Code in this repo, not by the static page. This is where real AI reasoning about calories happens, as opposed to `index.html`'s simple hardcoded heuristic.

## Skills

- **[calorie-estimation](.claude/skills/calorie-estimation/SKILL.md)** — estimate calories for a described food/drink. Triggers on things like "how many calories in...", "estimate calories for...".
- **[calorie-recommendation](.claude/skills/calorie-recommendation/SKILL.md)** — recommend a daily calorie target and what to eat for the rest of the day given a profile (and optionally today's intake). Triggers on things like "what should I eat today", "how many calories can I still eat".

Both skills use the `claude-sonnet-5` model and default to the same "model person" as `index.html`'s pre-filled profile: male, 50 years old, 190cm, 105kg, desk job, low sport frequency — used only when the user hasn't given their own stats.

## Notes

- No backend, no API keys, no dependencies. Everything runs client-side or inside a Claude Code chat session.
- The `#ad-slot` div in `index.html` is a placeholder for future ad/commercial content — not wired to any ad network.
