# Get alerted when a competitor's website changes

Watch pricing, terms or landing pages and receive only the pages that changed, with the added and removed text and a highlighted screenshot.

**Tool:** [Website Change Monitor](https://apify.com/squarish_altruism/page-change-monitor)

## 1. Paste this input

```json
{
  "urls": [
    { "url": "https://example.com/pricing" },
    { "url": "https://example.com/terms" }
  ],
  "monitorName": "competitor-pricing",
  "compareTo": "previous",
  "onlyChanged": true
}
```

Replace the URLs with the exact pages you want to watch. Keep the same `monitorName` on every run, because that is how each run finds its previous capture.

## 2. Run it once

The first run saves a starting capture of each page. **With `onlyChanged` on, its results are empty, and that's expected.** Later runs report pages that differ from the previous capture.

## 3. Put it on a schedule

Save the input as a task, then add the task to a schedule in Apify Console. Daily suits most pricing and policy pages.

## 4. Send yourself the changes

Add an integration to the task, such as Slack, email, a webhook, Zapier, Make or n8n, that fires when a run succeeds. In Zapier, Make or n8n, add a filter step to skip runs with empty results.

## What you get

This is real output from a test page whose content changes on every load:

```json
{
  "status": "changed",
  "changeTypes": ["text"],
  "changedPercent": 0.032,
  "textChanged": true,
  "textAdded": ["\"uuid\": \"08c9f263-ca90-4807-849a-4a2bb6f0a7b3\""],
  "textRemoved": ["\"uuid\": \"c6720705-ed47-4b6c-b9c2-d93ef260e2b3\""],
  "statusCode": 200,
  "device": "laptop"
}
```

Changed pages also include links to the current, previous and highlighted diff screenshots.

## Cost

$0.004 per page checked, including the first capture. Pages that fail to load are free.

| Pages | How often | Checks a month | Cost a month |
|---|---|---|---|
| 10 | Daily | 300 | $1.20 |
| 10 | Hourly | 7,200 | $28.80 |

## Avoiding false alarms

If part of a page changes on every visit, such as an ad or a visitor counter, hide it with CSS selectors:

```json
{ "ignoreSelectors": [".ad-banner", "#live-visitors"] }
```
