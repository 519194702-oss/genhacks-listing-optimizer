# ListingLens — Bilingual Amazon Listing Optimizer

GenHacks 2026 · Track: **AI, Agentic Systems, Cybersecurity, and Dev Tools**

Paste a draft Amazon listing and get back an optimized version in **English and Chinese** (true localization, not literal translation), plus an SEO score with a before/after breakdown and concrete fixes.

Built by an e-commerce operator: the optimization rules come from real listing work (JD.com flagship store, Amazon listing copywriting) — keyword-first titles, benefit-led bullets, honest specs.

## What it does

- **Input:** product title, up to 5 bullet points, description, target keywords.
- **Optimize (built-in rules engine, no key needed):**
  - English title rebuilt keyword-first (≤ 200 chars), 5 benefit-led bullets, rewritten description.
  - Chinese version localized for Chinese buyers (Taobao/JD-style copy, e.g. 保冷/保温 claims, 食品级不锈钢, 防漏吸管盖).
  - SEO score 0–100 with a breakdown (keyword coverage, title length, bullet completeness, readability) and specific fix suggestions. Shows before → after.
  - Copy buttons for every output block.
- **Optional live AI (BYOK):** paste your own OpenAI API key to get GPT-4o-mini rewrites instead of the rules engine. The key is stored only in your browser (localStorage, only if you tick the box) and is sent only to `api.openai.com`. If the AI call fails, it falls back to the rules engine. No key is ever bundled with the app.
- **Sample product:** one click loads a weak water-bottle listing — watch it go from 40 → 95.

## Run it

Static site, no build step, no dependencies. Any of these works:

```bash
# from this folder
python3 -m http.server 8000
# then open http://localhost:8000
```

Or open `index.html` directly in a browser, or host it on GitHub Pages.

## Files

- `index.html` — page structure
- `styles.css` — styling
- `app.js` — rules engine (fact extraction, scoring, EN optimizer, CN localizer), BYOK client, UI wiring. Pure logic is exported for Node (`module.exports`) so the engine can be tested headlessly: `node -e "const m=require('./app.js'); console.log(m.optimizeListing(m.SAMPLE))"`.
- `README.md` — this file

## Honest notes

- The rules engine's spec claims (e.g. "24-hour cold / 12-hour hot") are standard category templates — verify them against the real product before publishing a listing.
- The demo score is computed by the same engine that writes the copy, so it measures rule compliance, not marketplace ranking.
- The Chinese localizer is template-based (fact-driven). For arbitrary products it stays honest by only using facts found in the input; the BYOK path gives fuller rewrites.

## License

MIT
