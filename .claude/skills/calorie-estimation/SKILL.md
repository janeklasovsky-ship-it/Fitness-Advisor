---
name: calorie-estimation
description: Estimate the calorie content of a food or drink from a free-text description. Use when the user asks things like "how many calories in...", "estimate calories for...", "guess the calories of this meal", or pastes a description of what they ate/drank and wants a kcal figure.
model: claude-sonnet-5
---

# Calorie estimation

Given a free-text description of food and/or drink (may include portion size, brand, or preparation method, or may be vague), produce a calorie estimate.

## Steps

1. Parse the description into distinct food/drink items and their apparent portions (e.g. "2 slices of pizza and a coke" → pizza x2 slices, coke x1).
2. If a portion size isn't given, assume a typical/average restaurant-or-home portion for that item and say so explicitly.
3. Estimate calories per item using general nutritional knowledge, then sum them.
4. Only ask a clarifying question if the description is too vague to produce any reasonable estimate (e.g. just "food"). Otherwise, estimate first and note assumptions rather than blocking on questions.

## Output format

Keep it short:

- **Total estimate**: a single kcal number (or a tight range, e.g. "550–650 kcal")
- **Breakdown**: one line per item with its estimated kcal
- **Assumptions**: portion sizes or preparation methods you assumed

Do not add medical, dietary, or health disclaimers beyond one short line noting this is a rough estimate, not verified nutritional data.
