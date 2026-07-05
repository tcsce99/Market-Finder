# Apify — "First Lead List in 30 Minutes" Walkthrough

_A no-code, step-by-step for pulling a local-business lead list from Google Maps and turning it into a ranked prospect list for the Local Presence track (#1/#2) — or as a deliverable for a lead-list client (#4, local flavor)._

**Worked example:** HVAC contractors in Katy, TX. Swap the **trade** and **suburb** for anything — dentists in Sugar Land, roofers in Cypress, med spas in the Energy Corridor. Steps are identical.

**What you'll end with:** a clean spreadsheet of ~100–200 local businesses with name, phone, website, star rating, and **review count** — sorted so the best prospects (weak online presence = your buyers) float to the top.

---

## Before you start (2 min)

- **Time:** ~30 min the first time, ~10 min after.
- **Cost:** $0 to start. Apify's free plan includes ~$5/month of usage credit — enough for several hundred results. You do NOT need a paid plan to validate.
- **Skill level:** form-filling. If you can fill out an online order form, you can do this. **Do not** touch the "API," "Actor code," or "schedule/integrations" tabs — you don't need them, and that's where real coding would start.
- **Ethics/legal check (your halal-clean rule):** scraping **public Google Maps business listings is fine.** When you later email these businesses, use a real opt-out and honest subject lines (CAN-SPAM). Don't scrape LinkedIn with this. You're clean.

---

## Step 1 — Make a free Apify account (3 min)

1. Go to **apify.com** → Sign up (free). Confirm your email.
2. You land in the **Apify Console**. Left sidebar → click **Store** (this is the library of pre-built scrapers, called "Actors").

## Step 2 — Pick the right Actor (2 min)

1. In Store, search: **`Google Maps Extractor`** (by Apify / "compass").
   - Use **Google Maps Extractor** — it's the simpler, cheaper one, priced per result. Perfect for basic contact + review data.
   - _(There's also a beefier "Google Maps Scraper" — ignore it for now; more knobs, more cost, you don't need them.)_
2. Click the Actor → click the blue **Try for free / Start** button. This opens the input form.

## Step 3 — Fill in the input form (5 min)

You'll see a form. Only these fields matter — leave everything else at default:

| Field | What to put | Notes |
|---|---|---|
| **Search term(s)** | `HVAC contractor` | One clear term. Add a few variants on separate lines if you want: `air conditioning repair`, `AC repair` |
| **Location** | `Katy, TX` | City + state. Or a specific zip like `77494` to stay tight |
| **Language** | `English` | Default is fine |
| **Number of places / Max results** | `150` | Keep it modest the first time to save credit. 100–200 is plenty for one suburb |
| **Max reviews per place** | `0` | ⚠️ **Important — set to 0.** You want the review *count* (which comes automatically), NOT the full text of every review. Scraping review text burns credit fast and you don't need it |

3. Double-check "Max reviews per place" is **0**. This one setting is the difference between using $0.50 and $15 of credit.
4. Click the big **Start / Save & Start** button at the bottom.

## Step 4 — Let it run (2–5 min)

- You'll see a run screen with a log scrolling. It's working. A few minutes for ~150 results.
- When status flips to **SUCCEEDED**, you're done. Click the **Output / Storage** tab (or the "results" preview).

## Step 5 — Export the data (2 min)

1. On the results view, find the **Export** button (top of the results table).
2. Choose **CSV** (or "Export to Google Sheets" if offered — even easier).
3. Download it / open it in **Google Sheets** (File → Import if you downloaded a CSV).

You now have raw data. It has *lots* of columns — that's fine, we'll trim.

## Step 6 — Clean it into a prospect list (8 min)

In Google Sheets, **keep only these columns** (delete the rest):

| Keep this column | Apify usually calls it |
|---|---|
| Business name | `title` |
| Phone | `phone` |
| Website | `website` |
| Star rating | `totalScore` |
| **Review count** | `reviewsCount` |
| Address | `address` |
| Google Maps link | `url` |

Then:
1. **Sort by `reviewsCount`, smallest → largest.** (Select data → Data → Sort range → by reviewsCount, A→Z.)
2. The businesses now at the **top** — few or zero reviews — are your **hottest Local Presence prospects.** They're visibly underserving their profile.
3. Add two columns of your own:
   - **`Website?`** — put "NO" for any blank website cell. No website = even hotter prospect.
   - **`Prospect score`** — simple rule you apply by eye:
     - 🔥 **Hot** = under 25 reviews OR no website
     - 🟡 **Warm** = 25–75 reviews, basic website
     - ⬜ **Skip** = 100+ reviews, clearly already handled (or an established competitor)

That's your list. The 🔥 rows are who you contact first.

## Step 7 — Turn it into outreach (the point of all this)

For each 🔥 prospect, you now have everything for a personalized audit message:
> "Hi [name] — I looked up [business] on Google Maps. You've got **[X] reviews** and you're showing below [a competitor you can see in the same list] for 'AC repair in Katy.' That gap is sending calls to them. I help local HVAC companies fix exactly this. Want a free 1-page breakdown of what's costing you calls?"

You pulled the **[X] reviews** and the competitor comparison straight from your sheet. That specificity is why cold outreach actually gets replies.

---

## Cost reality check

- Free $5/month credit ≈ **several hundred results/month** with reviews set to 0. Enough to prospect multiple suburbs while validating.
- If you scale up and blow through free credit, the smallest paid plan is ~$39/mo — but **don't pay until you have a paying client.** Validate on the free tier.
- ⚠️ **The one way to waste money:** forgetting to set "Max reviews per place" to **0**. Always check it.

## When Apify is NOT the answer

- Need **decision-maker emails at specific companies** (the B2B agency-list flavor of #4)? Use **Apollo.io** instead — cleaner, ToS-safe, better free tier. Apify Maps is for *local business* leads, not corporate contact databases.
- Need to scrape **LinkedIn**? Don't — ToS violation, account bans, and it brushes your ethics constraint.

## Troubleshooting

- **Run failed / 0 results:** your search term + location combo may be too narrow. Broaden location (use the whole city, not one zip) and retry.
- **Weird/messy columns:** ignore the extras; only the 7 columns in Step 6 matter.
- **Credit used up fast:** you almost certainly left "Max reviews per place" above 0. Reset to 0.
- **Duplicates:** in Sheets, Data → Data cleanup → Remove duplicates (by phone or name).

---

_Next asset I can write for you: the full cold-outreach sequence (first message + follow-ups) and the free 1-page audit template you hand a prospect on the call. Say the word and pick your trade + suburb._
