# PRD: Roast & Toast Machine (Daily Content Creator)

## Problem
Building a social following needs fresh, shareable posts every day, but writing funny, on-brand content from scratch is slow and hit-or-miss.

## Goal
Apply a user's own comedy guide as a "personal brand lens" to any subject, topic, or news story and produce two editable social posts in seconds: a playful ROAST and a sincere TOAST, both in a chosen comedy persona.

## Users
Students, creators, and small-brand owners growing an audience on X, LinkedIn, or Facebook with light, shareable humor.

## Core features (must have)
1. **Comedy (brand) guide**: text document covering personality, tone, headline/opener style, audience, key channel, call to action, goals, post length, hex color scheme, and image/mood descriptions. Includes multiple `PERSONA:` lines. Uploadable (.txt/.md) and editable in the app. Default length: 40-80 words per post (short-form).
2. **Topic input**: type or paste a person, situation, trend, or news snippet, and pick a persona from a menu built from the guide.
3. **Generation**: server-side call to the chosen LLM provider (Anthropic, OpenAI, or xAI) combining guide + persona + topic; returns a roast and a toast.
4. **Edit & picture**: both posts are editable with live word/character counts; optional image upload with preview; copy buttons.
5. **Archive** (localStorage): topic, persona, date, and final roast/toast; also each saved version of the guide. Warns that data is device-only.

## Content safety
Roasts are affectionate teasing of choices and quirks only. The server prompt forbids targeting race, religion, gender, sexuality, disability, body, health, or other sensitive traits, and forbids slurs and harassment.

## Security requirements
- API key stored only as a server-side environment variable; used only in `/api/generate`; never in browser storage or Git.
- Shared access code required; per-IP hourly limit and daily global cap; input size limits.

## Non-goals (future)
Auto-posting, trending topics, daily email, database archive, AI image generation, multi-user accounts/payments.

## Look & feel
Comedy-club marquee: deep purple #1A0F2E, hot pink #FF3D81, spotlight yellow #FFD23F, cream #FFF4DC; neon glow title, rounded pill buttons.

## Acceptance tests
- Same subject with two different personas yields clearly different voices and respects the length limits.
- Editing the CTA in the guide changes how both posts end.
- Wrong access code is rejected; the 11th request in an hour from one IP is rejected.
- Archive survives refresh; guide saves appear in archive.
- Sensitive-trait bait in the topic (e.g. "roast him for his weight") does not produce a roast on that trait.
- No key visible in page source, network requests, or repo.
