# GBP Audit: a free Claude skill for local businesses

Want to know if AI search can find your business? This free Claude skill checks your
Google Business Profile and grades it. You give it your business name and city. It does
the rest.

It scores your profile out of 100 on the three things AI looks at before it recommends a
local business: how complete your profile is, your categories, and your reviews. Then it
grades you A to F and hands you a short list of fixes, ranked by impact.

The grade is real. The skill only scores what it can actually read from your public Google
listing. It never makes up a number.

---

## What you need

- A Claude account. The free plan works.
- Web search turned on in Claude. The skill needs it to look up your listing.

That is it. There is nothing to install on your computer. No code. No Python.

---

## How to add the skill to Claude

This works on the Claude website (claude.ai) and the Claude desktop app.

1. **Download the skill file.** Get `gbp-audit.zip` from this page (click it, then download).
2. In Claude, open **Settings**.
3. Go to **Capabilities**, then **Skills** (on some accounts it is under **Customize**).
4. Click **Create skill**, then upload the `gbp-audit.zip` file you downloaded.
5. Done. The skill is now in your Claude.

If you do not see a Skills option, make sure code execution is turned on in Settings first.

---

## How to run it

1. Turn on **web search** in Claude (look for the web or search toggle near the chat box).
2. Type this, with your own business:

   > Audit my Google Business Profile for {your business name} in {your city}.

3. Claude will find your listing, score it, and show your grade with your top fixes.

If more than one business shares your name, Claude will ask you which one. That is the only
question it asks.

---

## What you get

- A real grade out of 100, A to F.
- A score for each area: completeness, categories, and reviews.
- Your top three fixes, written in plain language, ranked by what helps most.

---

## What this checks, and what it does not

This skill checks your **Google Business Profile** only. That profile feeds Google's own AI
search, like AI Overviews and Gemini.

It does not check Bing, Facebook, Yelp, your website, or Reddit. Those matter for ChatGPT and
Perplexity, but they are a separate job. A strong Google grade is a great start, not the whole
picture.

---

Built by Alex at [Viziblty](https://viziblty.com). Helping local businesses get found in AI search.
