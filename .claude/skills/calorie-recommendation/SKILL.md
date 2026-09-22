---
name: calorie-recommendation
description: Recommend a daily calorie target and what the user should still eat for the rest of the day, based on their profile and what they've already consumed. Use when the user asks things like "what should I eat today", "how many calories can I still eat", "recommend my calorie intake", or gives their stats and today's food log.
model: claude-sonnet-5
---

# Calorie recommendation

Given a user profile (age, height, weight, gender, occupation/activity level, sport frequency) and, optionally, calories already consumed today, compute a daily target and recommend what to eat for the rest of the day.

If the user hasn't given their own profile, use this default "model person": male, 50 years old, 190cm, 105kg, desk job (mostly sitting), low sport frequency (1–2 sessions/week) — and say clearly that you're using default assumptions.

## Steps

1. **Compute BMR** with the Mifflin-St Jeor formula:
   - Men: `10 × weight(kg) + 6.25 × height(cm) − 5 × age + 5`
   - Women: `10 × weight(kg) + 6.25 × height(cm) − 5 × age − 161`
2. **Apply an activity multiplier** based on occupation and sport frequency:
   - Desk job: 1.2 · Light activity: 1.375 · Active job: 1.55 · Very active: 1.725
   - Add roughly +0.05 for 1–2 sport sessions/week, +0.1 for 3–4, +0.15 for 5+
3. **Daily target (TDEE)** = BMR × activity multiplier.
4. **Remaining budget** = daily target − calories already consumed today (if given).
5. Recommend what to eat for the rest of the day: rough meal size/composition (e.g. "a moderate dinner with lean protein and vegetables"), not a strict meal plan or specific health claim.

## Output format

Keep it short:

- **Daily target**: kcal figure, one line on how it was derived (formula + multiplier used)
- **Consumed so far / remaining**: if provided
- **Recommendation**: 2-4 sentences of practical, general guidance for the rest of the day

Note once that this is a general estimate, not personalized medical or nutritional advice — don't repeat the disclaimer.
