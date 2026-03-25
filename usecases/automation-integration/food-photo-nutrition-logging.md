---
title: "OpenClaw AI Nutrition Analysis: Log Meal Photos with Haver"
slug: food-photo-nutrition-logging
summary: "This case uses openclaw-nutrition and Haver so users can log meals from chat or food photos into daily calorie and macro records without manual diary entry."
whatItDoes: "Uses the openclaw-nutrition skill with the Haver backend to accept meal text or images and write them into daily nutrition logs."
category: automation-integration
difficulty: intermediate
tags:
  - food-photo-analysis
  - nutrition-tracking
  - meal-logging
  - calorie-logging
  - health-coaching
targetUser:
  - Nutrition coaches
  - Health-conscious users
  - Wellness product teams
skillsUsed:
  - name: openclaw-nutrition
    href: https://clawhub.ai/Yuvasee/openclaw-nutrition
updatedAt: "2026-03-25"
published: true
---

## What it does
`openclaw-nutrition` uses the Haver backend to accept meal text or food photos, log calories and macros, and store entries in date-based daily nutrition records. The same flow also supports weight tracking, daily summaries, and AI coaching.

## Skills You Need
- [openclaw-nutrition](https://clawhub.ai/Yuvasee/openclaw-nutrition)

## Pain Point
The core problem with food tracking is not nutrient lookup but logging friction. Users have to reopen an app, search foods, estimate portions, and maintain a diary several times a day, which is where the habit breaks down.

## Core value of this case
Nutrition tracking becomes a natural OpenClaw conversation instead of a separate diary workflow. A user can send a sentence or a meal photo, have the system log it automatically, and continue directly into summaries or coaching without switching tools.

## Typical scenarios
- A personal user logs breakfast and lunch with short text or meal photos and checks remaining calories and macros later in the day.
- A nutrition coach gives clients a conversational logging flow first, then reviews summaries instead of chasing manual food diaries.
- A wellness builder prototypes a camera-first nutrition coach with this skill before investing in a dedicated mobile app.

## How to setup
1. Install the skill with `clawhub install Yuvasee/openclaw-nutrition`, or add `openclaw-nutrition` from ClawHub.
2. Register with Haver using `POST /api/register` and obtain the per-user API key prefixed with `hv_`.
3. Complete onboarding by setting timezone, profile data, activity level, and nutrition goals.
4. Start logging meals with `POST /api/me/nutrition/log`; the skill docs show that this endpoint can take text and optional `images`.
5. Use `GET /api/me/nutrition/summary` to pull daily or range-based summaries once entries have been logged.
6. You can also use the Telegram bot `@haver_sheli_bot` as a hosted entry point for the same backend.

## Related Links
- [Haver](https://haver.dev/)
- [ClawHub: openclaw-nutrition](https://clawhub.ai/Yuvasee/openclaw-nutrition)
- [GitHub: Yuvasee/openclaw-nutrition](https://github.com/Yuvasee/openclaw-nutrition)
- [Telegram: @haver_sheli_bot](https://t.me/haver_sheli_bot)
- [OpenClaw Docs: Skills CLI](https://docs.openclaw.ai/cli/skills)

## FAQ

### Does it support food-photo input?
Yes. Haver explicitly advertises photo recognition, and the skill docs show `POST /api/me/nutrition/log` and `POST /api/me/chat` with optional `images`.

### Does it automatically write to Google Sheets or n8n?
There is no documented Google Sheets or n8n integration. The documented behavior is automatic logging into Haver's nutrition-tracking backend, plus summaries and coaching flows.

### What are the documented limits?
It is not a medical nutrition tool and does not cover workout logging, water tracking, barcode scanning, or deleting logged meals. It fits daily nutrition tracking better than a full health-record system.
