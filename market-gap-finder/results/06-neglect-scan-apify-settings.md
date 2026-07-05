# Multi-Trade "Neglect Scan" — exact Apify settings

_Goal: pull Google Maps data for several trades at once, then rank which trade/area has the MOST weak profiles = the easiest market to sell Local Presence into._

**The whole idea:** you proved garage-door-Cypress is well-served (most profiles already strong). Now you compare trades side-by-side on one number — **% of businesses with weak profiles** — and attack the weakest market.

---

## Step 1 — Actor + where to put settings

1. Apify Console → **Store** → open **`Google Maps Scraper`** OR **`Google Maps Extractor`** (both by "compass"). **Either works** — they return the same base data (name, category, review count, rating, website, phone). On current free-plan pricing the **Scraper is marginally cheaper** ($4 vs $5 per 1,000 places), but for a ~160-place scan that's the difference between $0.64 and $0.80 — negligible. Pick either → **Try for free**.
2. ⚠️ **CRITICAL — do NOT enable any add-ons.** Both actors upsell optional enrichment lines: "Business leads enrichment" (**$100/1,000** on free!), "Company contacts enrichment," "Additional place details." You need **none** of them — the base **"Scraped place"** tier already includes review count + category. Enabling the leads add-on would torch your credit.
3. You'll see an **input form** (fields with labels). Match the labels below. If you prefer, click the **"JSON" / raw input** tab and paste the block in Step 3 instead — same result.

## Step 2 — Fill the form (match by label)

| Form field (label) | Value | Why |
|---|---|---|
| **Search terms** (one per line) | see list below | Each line = one trade to scan |
| **Location** | `Cypress, TX` | Run again later with `Katy, TX` to compare areas |
| **Max places per search** | `40` | Enough to judge a market; keeps credit low |
| **Language** | `English` | — |
| **Skip closed places** | ✅ on | Ignores dead listings |
| **Reviews / scrape reviews** | **leave OFF / 0** | ⚠️ You only need the review **count** (comes free). Scraping review text burns credit fast |

**Search terms to queue (paste one per line):**
```
fence contractor
tree service
junk removal
appliance repair
pool service
handyman
pressure washing
```
_(Drop any you don't want. Fewer terms = less credit. I'd start with the first 4.)_

## Step 3 — (Optional) JSON input instead of the form

If you use the raw **JSON** tab, paste this:
```json
{
  "searchStringsArray": [
    "fence contractor",
    "tree service",
    "junk removal",
    "appliance repair"
  ],
  "locationQuery": "Cypress, TX",
  "maxCrawledPlacesPerSearch": 40,
  "language": "en",
  "skipClosedPlaces": true
}
```
Then click **Start**. (Field names shown are the Extractor's keys; if a name differs in your version, just use the form in Step 2 — it's the same settings.)

## Step 4 — Run + export

- Click **Start**, wait for **SUCCEEDED** (a few minutes for ~160 results across 4 trades).
- **Export → CSV**, or **Export to Google Sheets** if offered.

## Step 5 — Turn the export into a neglect score

In Google Sheets, keep these columns (delete the rest):

| Keep | Extractor field |
|---|---|
| Business name | `title` |
| Trade searched | `searchString` (tells you which term found it) |
| Category | `categoryName` |
| Review count | `reviewsCount` |
| Rating | `totalScore` |
| Website | `website` |
| Phone | `phone` |
| Maps link | `url` |

Then add one column called **`WEAK?`** and mark a row weak (put a `1`) if **ANY** of these is true:
- `reviewsCount` **< 30**, OR
- `website` is **blank**, OR
- `categoryName` **doesn't match the trade** (e.g. a garage-door business listed as "Business center" — the exact gap you already found).

## Step 6 — Compare trades and pick the winner

Make a tiny summary table (one row per trade):

| Trade | # businesses | # WEAK | **% weak** |
|---|---|---|---|
| fence contractor | 40 | 18 | **45%** |
| tree service | 40 | 22 | **55%** |
| junk removal | 40 | 9 | 23% |
| appliance repair | 40 | 14 | 35% |

_(To get % weak fast: `=COUNTIF(range,1)/COUNT(range)` per trade, or just filter by trade + sum the WEAK column.)_

**Decision rule:**
- **> ~40% weak = strong market.** Lots of fixable profiles = easy pitch. Attack it.
- **20–40% = workable**, lead with the category-fix angle.
- **< 20% = saturated** (like garage-door-Cypress was). Skip.

Whichever trade has the **highest % weak** is your beachhead. Then within it, sort by `reviewsCount` ascending → the top rows are your first outreach targets (after a quick manual eyeball to rule out shells, like you did).

---

## Cost check
- Free ~$5/mo credit covers **hundreds of results** with reviews OFF. 4 trades × 40 = 160 results is well within it.
- ⚠️ Only real waste risk: leaving review-scraping ON. Keep it off.
- Don't upgrade to a paid plan until a client is paying you.

## What Apify still WON'T do (you do this part)
- **Spot shells / virtual offices** (the Sola-Salons-address trick) — eyeball the top prospects on Maps before outreach.
- **Judge posting cadence / Q&A / photo recency** — check the real profile for your final audit.
Apify gives clean *inputs*; the *judgment* stays yours.

---

_Next: once you've picked the highest-%-weak trade, I'll write the cold outreach + the free 1-page audit for that trade._
