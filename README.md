# Whop Content Rewards Scraper: Clipping & UGC Campaigns

Scrape the Whop Content Rewards directory: reward per 1K views, budget left, burn rate, platforms, payout type and campaign URLs. Builds a private archive of campaigns that have rotated off the public page, so you can benchmark CPM rates, track budget burn and catch new clipping campaigns.

This repo shows how to call the [Whop Content Rewards Scraper: Clipping & UGC Campaigns](https://apify.com/fayoussef/whop-clipping-campaigns-scraper?fpr=youssef) Apify Actor from your own code: a Python and a JavaScript example, the input they send, and a sample of the output. Everything runs in the Apify cloud, so there is nothing to host, scale or maintain on your side.

- **Run it in the browser:** [fayoussef/whop-clipping-campaigns-scraper on Apify](https://apify.com/fayoussef/whop-clipping-campaigns-scraper?fpr=youssef)
- **Guide and docs:** [automationbyexperts.com/apify/whop-clipping-campaigns-scraper](https://automationbyexperts.com/apify/whop-clipping-campaigns-scraper)
- **Actor ID for the API:** `fayoussef/whop-clipping-campaigns-scraper`

## Use cases

- [Find the highest paying clipping campaigns on Whop](https://apify.com/fayoussef/whop-clipping-campaigns-scraper/examples/high-paying-clipping-campaigns?fpr=youssef): Lists every live Whop Content Rewards campaign paying at least 2 dollars per 1,000 views with more than 1,000 dollars of budget still unspent, sorted by reward. Use it to pick the campaigns where a clip actually gets paid, instead of scrolling a directory that only shows a rotating page of featured ones.
- [Find low competition TikTok clipping campaigns](https://apify.com/fayoussef/whop-clipping-campaigns-scraper/examples/low-competition-tiktok-clipping-campaigns?fpr=youssef): Filters Whop Content Rewards down to TikTok campaigns with 50 or fewer creators already submitting and no application step, so you can start clipping today and compete for views against a small pool. Sorted by fewest creators first.
- [Get alerted when new Whop campaigns launch](https://apify.com/fayoussef/whop-clipping-campaigns-scraper/examples/new-content-rewards-campaigns-alert?fpr=youssef): Monitoring mode: each run returns only the campaigns that were not in the previous run, so a daily schedule becomes an alert feed for fresh clipping and UGC campaigns. Pair it with the Apify Slack or email integration to hear about a new campaign before its budget fills up.

## Quick start

1. Create a free [Apify account](https://console.apify.com/sign-up?fpr=youssef) and copy your API token from [Settings > Integrations](https://console.apify.com/settings/integrations).
2. Set it as an environment variable: `export APIFY_TOKEN=...` (PowerShell: `$env:APIFY_TOKEN="..."`).
3. Edit [`input.json`](input.json) and run one of the examples below.

### Python

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

### JavaScript / Node.js

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

### cURL (plain HTTP)

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

## Pricing

Pay per use on Apify: you are charged per event (results produced), with no subscription to this Actor. The current rate is shown on the [Actor's Store page](https://apify.com/fayoussef/whop-clipping-campaigns-scraper?fpr=youssef). Free-plan runs are capped; an [Apify plan](https://apify.com/pricing?fpr=youssef) unlocks full runs.

## More Actors by AutomationByExperts

- [Canada411 Scraper: Business Phones, Addresses](https://github.com/automationbyexperts/canada411-scraper)
- [thebluebook.com Scraper](https://github.com/automationbyexperts/thebluebook-scraper)
- [Bulk AI Image Generator (NO API KEY)](https://github.com/automationbyexperts/bulk-ai-image-generator)
- [Bulk LLM Runner GPT, Claude, Perplexity, Kimi (No API Key)](https://github.com/automationbyexperts/bulk-llm-runner)
- [AutoTrader Canada Car Scraper: Prices, VIN, Mileage & Dealers](https://github.com/automationbyexperts/autotrader-canada-scraper)
- [Spitogatos.gr Scraper: Greek Property Listings & Agent Phones](https://github.com/automationbyexperts/spitogatos-scraper)
- [Full catalog of our web scraping APIs](https://github.com/automationbyexperts/web-scraping-apis)

## Support

Questions, bugs or a custom scraper: open an issue here, use the Issues tab on the [Apify page](https://apify.com/fayoussef/whop-clipping-campaigns-scraper?fpr=youssef), or email youssefarhan24@gmail.com.

## License

The example code in this repo is MIT licensed. The Actor itself runs on Apify under its own terms.
