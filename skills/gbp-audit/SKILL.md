---
name: gbp-audit
description: Free self-audit of a local business's Google Business Profile, scored for AI-driven local search. Give it a business name and city; it researches the public Google listing with web search, scores the profile out of 100 across completeness, categories, and reviews, grades it A to F, and returns a ranked list of plain-language fixes. Use when someone says "audit my Google Business Profile", "/gbp-audit", "check my GBP", "score my Google profile", "is my Google listing optimized", or wants a free self-audit of a local/small business's Google profile. Runs in any Claude with web search on (claude.ai or Claude desktop). No install, no setup, no Python.
---

# gbp-audit

A free self-audit of a local business's **Google Business Profile (GBP)**. The user gives a
business name and city. You research the public Google listing, score it, grade it A to F, and
hand back the highest-impact fixes in plain language.

You do all the work with **web search and web fetch**. There is nothing to install. The user only
answers "which business" and, if needed, "which one of these listings".

**The grade must be real.** Only score a field from data you actually read in a search result or
fetched page. Never invent a rating, a review count, a category, or any number. If you cannot read
a field, say so and turn it into a fix. There is no fabrication anywhere in this skill.

**Scope: the Google Business Profile listing only.** Completeness, categories, reviews. This does
not audit Bing, Facebook, Yelp, the business website, or Reddit. Those drive ChatGPT and Perplexity
visibility and are out of scope here. Say so in the report so the owner is not misled into thinking
a strong GBP score means they are visible everywhere.

---

## Phase 0 — Web search check

You need web search to run this. If web search is off or unavailable, tell the user in one line:
"Turn on web search in your Claude settings, then ask me again." Do not fall back to asking the
user to look up their own profile details. This skill does the research, not the user.

## Phase 1 — Intake

Ask once: **business name** and **city or area**. Nothing else.

## Phase 2 — Find and disambiguate

Web search for `"{business} {city}"` and `"{business} {city} google maps reviews"`. Collect the
candidate Google listings (name + city + a link).

- **0 candidates** → ask the user to paste their Google Maps link, then continue.
- **exactly 1** → use it.
- **2 or more** → show a short numbered list and ask which one. Never auto-pick. A same-name
  business in another city is the classic wrong answer. This is the only follow-up question you are
  allowed to ask.

## Phase 3 — Read the public profile (cite every field)

From the Google knowledge panel, the Maps listing, and the search results, read only what you can
actually see. For each scored field, note where you read it. **Never guess.**

Read these (all are normally public):
- **Primary category** (e.g. "Plumber", "Family law attorney").
- **Average rating** and **total review count**.
- **Newest review date** if it shows in the results (best effort).
- **Website** linked or not.
- **Hours** set or not.
- **Phone** present or not.
- **Business description** present, and roughly how long.

If a field genuinely does not appear anywhere you can read, mark it **not readable** and let it
become a fix. Do not score a number you did not see.

## Phase 4 — Score

Score the rubric below. It is deterministic: the same readable inputs always give the same score.
Produce a total out of 100, a letter grade, the three dimension subtotals, and the top 3 fixes.

## Phase 5 — Write the fixes in plain language

Rewrite each top fix as one encouraging "do this next" sentence. Keep every line the user reads at
**Flesch-Kincaid grade 8 or lower**. Short sentences. No jargon. No em dashes. Spell out single
digit numbers.

## Phase 6 — Report

Show the full scorecard inline using the layout below. Then offer to format it as a clean document
the user can copy or download. The report is the only output.

---

## The rubric (100 points, 3 dimensions)

Every sub-factor here is something you can read from a normal public Google search. There are no
hidden fields. Grade bands: **A 85-100 · B 70-84 · C 55-69 · D 40-54 · F 0-39.**

### A — Profile Completeness (28)
| Sub-factor | Points |
|---|---|
| Website linked | 10 |
| Hours set | 8 |
| Phone present | 5 |
| Description present (about 250+ characters) | 5 |

### B — Categories (27)
| Sub-factor | Points |
|---|---|
| Primary category set | 15 |
| Primary is specific, not a generic umbrella like "Store" or "Establishment" | 12 |

### C — Review Signals (45)
| Sub-factor | Points |
|---|---|
| Volume: 100+ = 18, 50-99 = 14, 25-49 = 10, 10-24 = 6, 1-9 = 3, 0 = 0 | 18 |
| Avg rating: 4.5+ = 17, 4.0-4.49 = 12, 3.5-3.99 = 7, above 0 = 3, none = 0 | 17 |
| Newest review: 14 days or less = 10, 30d = 8, 90d = 5, 180d = 2, older or not readable = 0 | 10 |

If you could not read a field, it scores 0 and you disclose it in the report. You never assign a
number you did not actually see.

### Top-3 fixes — leverage ranking
For each sub-factor below its max: `leverage = points_lost x multiplier`. Multipliers: **no primary
category 4x; thin, stale, or low-rated reviews (volume, rating, recency) 3x; generic primary
category 2x; everything else 1x.** Sort descending, take the top 3, write each as a plain
do-this-next sentence.

### Research grounding (verified 2026-05-21)
- Primary category is the strongest local-pack ranking factor; review volume, rating, and recency
  are top-weighted (Whitespark 2026 Local Search Ranking Factors).
- ChatGPT searches Bing in real time and leans on Facebook, Yelp, and TripAdvisor; it does not read
  the GBP directly. A strong GBP helps Google's own AI surfaces (AI Overviews and Gemini), which is
  why the scope note matters.

---

## Report layout

```
# Google Business Profile Audit: {Business}
{City} · {date} · Grade {grade} · {total}/100

{one-line plain verdict}

## Score by area
A Profile completeness   {bar}  {n}/28
B Categories             {bar}  {n}/27
C Reviews                {bar}  {n}/45

## Your top 3 fixes (biggest impact first)
1. {plain fix sentence}
2. ...
3. ...

## Full detail
{table: factor | got/max | what I read}

## About this audit
This audit covers your Google Business Profile, which feeds Google's AI search (AI Overviews and
Gemini). ChatGPT and Perplexity rely more on other sources like Bing, Facebook, and Yelp, which are
outside this audit. Everything scored here was read live from your public Google listing. Anything I
could not read is listed as a fix, not guessed.
```

---

## Critical rules
- **Never fabricate.** Score a field only from data you actually read; cite where you read it. If
  you cannot read it, disclose it and make it a fix. The grade the user sees is the real one.
- **GBP only.** Completeness, categories, reviews. Nothing about Bing, Facebook, Yelp, the website,
  or Reddit, beyond the one-line scope note.
- **Disambiguate, never assume.** More than one candidate means you ask which. Wrong city is the top
  failure.
- **The user does not do the research.** You use web search. The only questions you may ask are the
  business + city at intake and, if needed, which listing.
- **Public-facing copy is Flesch-Kincaid 8 or lower.** No jargon. No em dashes.
- **One output** — the report.
