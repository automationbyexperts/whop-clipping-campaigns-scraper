# Whop Content Rewards Scraper: Clipping & UGC Campaigns, CPM Rates, Budgets & Burn Rate

[![Run on Apify](https://img.shields.io/badge/Apify-Run%20the%20Actor-00A67E?logo=apify&logoColor=white)](https://apify.com/fayoussef/whop-clipping-campaigns-scraper?fpr=youssef)
![CPM](https://img.shields.io/badge/CPM-per%201K%20views-2ea44f)
![Burn rate](https://img.shields.io/badge/Burn%20rate-between%20runs-1C7ED6)
![New campaigns](https://img.shields.io/badge/New%20campaigns-flagged-8B5CF6)
![Export](https://img.shields.io/badge/Export-JSON%20%7C%20CSV%20%7C%20Excel-F59E0B)

> ### ▶️ [Run the Whop Content Rewards Scraper on Apify](https://apify.com/fayoussef/whop-clipping-campaigns-scraper?fpr=youssef)
> Scrape the **Whop Content Rewards** directory of clipping and UGC campaigns: **reward per 1,000 views**, budget left, **burn rate**, platforms, payout type, creator count and rules. Keeps an archive of campaigns that rotate off the page and flags new launches.

**Whop Content Rewards Scraper** turns the Whop Content Rewards directory into a structured dataset of live clipping campaigns for TikTok, YouTube Shorts, Instagram Reels and X. It is built for clippers looking for campaigns that still pay, clipping agencies routing work to creators, brands pricing their own campaign, and analysts of the creator economy. No login, no cookies, no API key. This repository documents the Apify Actor and gives working Python, JavaScript and cURL examples for calling it through the API.

- **Run it in the browser:** [fayoussef/whop-clipping-campaigns-scraper on Apify](https://apify.com/fayoussef/whop-clipping-campaigns-scraper?fpr=youssef)
- **Guide and docs:** [automationbyexperts.com/apify/whop-clipping-campaigns-scraper](https://automationbyexperts.com/apify/whop-clipping-campaigns-scraper)
- **Actor ID for the API:** `fayoussef/whop-clipping-campaigns-scraper`

## What the Whop Content Rewards scraper does

- **Every campaign on the public directory**, with reward per 1K views, total budget, budget spent and budget left.
- **Burn rate**: `budgetSpentDeltaUsd` shows how much each campaign paid out since your last run, so you can tell a campaign that pays from one that stalls.
- **New campaign detection**: `isNew` flags launches since your previous run, and **Only new campaigns** turns the Actor into a feed of fresh campaigns.
- **A campaign archive**: Whop shows about 50 featured campaigns at a time; **Include historical campaigns** keeps every campaign you have seen, even after it rotates off the page.
- **Estimated views remaining** for every campaign.
- **Filters**: minimum reward per 1K views, minimum budget left, platforms, payout type, maximum creators, verified brands and no application required.

## Output fields: what data you get

One row per campaign. The main fields:

| Field | Description |
|---|---|
| `title` / `campaignUrl` | Campaign name and link |
| `rewardPerThousandUsd` | Reward per 1,000 views |
| `totalBudgetUsd` / `budgetSpentUsd` / `budgetLeftUsd` / `progressPercentage` | Budget, spent, left and percent used |
| `budgetSpentDeltaUsd` | Paid out since your last run (burn rate) |
| `socialPlatforms` | TikTok, YouTube, Instagram, X... |
| `estimatedViewsRemaining` | Views the remaining budget can still pay for |
| `payoutType` | How creators are paid |
| `creatorsCount` / `requiresApplication` / `isVerified` | Creators already joined, application needed, verified brand |
| `isNew` / `scrapedAt` | New since last run, and when it was captured |
| `description` / `brand` / `fundedAt` | Campaign rules text, brand and funding date |

## Input

No input is required. Optional filters:

| Field | What it does |
|---|---|
| `searchText` | Keyword filter |
| `platforms` / `payoutTypes` | Social platforms and payout type |
| `minRewardPerThousand` | Minimum reward per 1K views |
| `minBudgetLeftUsd` / `maxProgressPercentage` | Budget still available |
| `maxCreators` | Maximum creators already joined |
| `verifiedOnly` / `noApplicationRequired` | Verified brands, no application |
| `sortBy` / `maxItems` | Sort order and number of campaigns |
| `onlyNewCampaigns` / `includeHistorical` | New launches only, or the full archive |

## Use cases

- **Clippers**: find the highest paying campaigns with the fewest creators.
- **Clipping agencies**: pull the directory on a schedule and route campaigns to creators.
- **Brands and agencies**: set your campaign CPM against what the market pays.
- **Alerts**: get new clipping campaigns in Slack, Telegram or email as they launch.
- **Creator economy analytics**: track CPM by platform, budget burn and campaign lifespan.

Ready-made examples you can run in one click:

- [Find the highest paying clipping campaigns on Whop](https://apify.com/fayoussef/whop-clipping-campaigns-scraper/examples/high-paying-clipping-campaigns?fpr=youssef): Lists every live Whop Content Rewards campaign paying at least 2 dollars per 1,000 views with more than 1,000 dollars of budget still unspent, sorted by reward. Use it to pick the campaigns where a clip actually gets paid, instead of scrolling a directory that only shows a rotating page of featured ones.
- [Find low competition TikTok clipping campaigns](https://apify.com/fayoussef/whop-clipping-campaigns-scraper/examples/low-competition-tiktok-clipping-campaigns?fpr=youssef): Filters Whop Content Rewards down to TikTok campaigns with 50 or fewer creators already submitting and no application step, so you can start clipping today and compete for views against a small pool. Sorted by fewest creators first.

## Quick start

### 1. In the browser (no code)

1. Open the Actor on Apify and click **Try for free**. No input is required.
2. Optionally set a minimum reward per 1K views, platforms or a maximum number of creators.
3. Click **Start**, then browse or download campaigns from the **Output** tab.

### 2. Through the API

1. Create a free [Apify account](https://console.apify.com/sign-up?fpr=youssef) and copy your API token from [Settings > Integrations](https://console.apify.com/settings/integrations).
2. Set it as an environment variable: `export APIFY_TOKEN=...` (PowerShell: `$env:APIFY_TOKEN="..."`).
3. Edit [`input.json`](input.json) and run one of the examples below.

#### Python

```bash
pip install apify-client
python examples/python/run_actor.py
```

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("fayoussef/whop-clipping-campaigns-scraper").call(run_input={'sortBy': 'reward',
 'minRewardPerThousand': 2,
 'minBudgetLeftUsd': 1000,
 'maxItems': 100})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

#### JavaScript / Node.js

```bash
npm install apify-client
node examples/javascript/run_actor.mjs
```

```javascript
import { ApifyClient } from "apify-client";

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor("fayoussef/whop-clipping-campaigns-scraper").call({
    "sortBy": "reward",
    "minRewardPerThousand": 2,
    "minBudgetLeftUsd": 1000,
    "maxItems": 100
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

#### cURL (plain HTTP)

Runs the Actor and returns the dataset items in one synchronous call:

```bash
curl -X POST "https://api.apify.com/v2/acts/fayoussef~whop-clipping-campaigns-scraper/run-sync-get-dataset-items?token=$APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d @input.json
```

Synchronous calls time out after 300 seconds. For larger runs use the client libraries above, or start the run with `POST /v2/acts/fayoussef~whop-clipping-campaigns-scraper/runs` and read the dataset when it finishes.

## Sample output

One record, from [`sample-output.json`](sample-output.json). Export the full dataset as JSON, CSV, Excel or HTML from the Apify Console, or read it through the API as shown above.

```json
{
  "title": "Yomi Denzel Clipping - 1$ par 1000 vues",
  "brand": "Yomi Denzel Clipping",
  "payoutType": "cpm",
  "rewardPerThousandUsd": 1.0,
  "totalBudgetUsd": 238000.0,
  "budgetSpentUsd": 47492.72,
  "budgetLeftUsd": 190507.28,
  "progressPercentage": 19.95,
  "estimatedViewsRemaining": 190507280,
  "socialPlatforms": [
    "instagram",
    "tiktok",
    "youtube"
  ],
  "creatorsCount": 192,
  "requiresApplication": true,
  "isVerified": true,
  "fundedAt": "2026-08-15T10:40:47+00:00",
  "fundedAgo": "9mo",
  "campaignUrl": "https://whop.com/apps/exp_FeigepAu1zjagM/",
  "description": "Clippe le contenu de Yomi Denzel et gagne 1$ pour chaque 1000 vues.",
  "isLive": true,
  "isNew": false,
  "firstSeenAt": "2026-08-20T06:00:00+00:00",
  "lastSeenAt": "2026-09-05T06:00:00+00:00",
  "budgetSpentDeltaUsd": 4.7
}
```

## Integrations and automation

- **Schedule it** hourly or daily: that builds the campaign archive and powers new campaign alerts.
- **Send results** to Google Sheets, Airtable, Slack, a webhook, Make, Zapier or n8n with Apify integrations.
- **Use it from AI agents** through the Apify MCP server.

## FAQ

### What is Whop Content Rewards?
A Whop marketplace where brands pay creators per 1,000 views for clips and UGC posted on TikTok, YouTube Shorts, Instagram Reels and X.

### How do I find Whop clipping campaigns that still pay?
Sort by budget left and look at `budgetSpentDeltaUsd`: a campaign that paid out since your last run is actively paying.

### What reward per 1,000 views should my campaign offer?
Run the Actor and compare `rewardPerThousandUsd` with `creatorsCount` and burn rate for campaigns in your niche and platform.

### Do I need a Whop account or cookies?
No. The Actor reads the public directory.

### Why do I only get about 50 campaigns?
Whop shows logged-out visitors one rotating page of featured campaigns. Schedule the Actor with **Include historical campaigns** and your dataset grows past that.

### Can I use this as a Whop Content Rewards API?
Yes. Call it through the Apify API and get structured JSON.

## Pricing

Pay per use on Apify: you are charged per event (results produced), with no subscription to this Actor. The current rate is shown on the [Actor's Store page](https://apify.com/fayoussef/whop-clipping-campaigns-scraper?fpr=youssef). Free-plan runs are capped; an [Apify plan](https://apify.com/pricing?fpr=youssef) unlocks full runs.

## Related scrapers by AutomationByExperts

- [Canada411 Scraper: Phone Numbers & Addresses](https://github.com/automationbyexperts/canada411-scraper)
- [Bulk AI Image Generator: Nano Banana & GPT Image](https://github.com/automationbyexperts/bulk-ai-image-generator)
- [Bulk LLM Runner: ChatGPT, Claude & Gemini in Bulk](https://github.com/automationbyexperts/bulk-llm-runner)
- [AutoTrader.ca Scraper: Canada Car Listings, VIN & Dealers](https://github.com/automationbyexperts/autotrader-canada-scraper)
- [Spitogatos.gr Scraper: Greek Real Estate Listings](https://github.com/automationbyexperts/spitogatos-scraper)
- [Wallapop Scraper: Spain, France, Italy, Portugal & UK](https://github.com/automationbyexperts/wallapop-scraper)
- [Full catalog of our web scraping APIs](https://github.com/automationbyexperts/web-scraping-apis)

## Support

Questions, bugs or a custom scraper: open an issue here, use the Issues tab on the [Apify page](https://apify.com/fayoussef/whop-clipping-campaigns-scraper?fpr=youssef), or email youssefarhan24@gmail.com.

## License

The example code in this repo is MIT licensed. The Actor itself runs on Apify under its own terms.
