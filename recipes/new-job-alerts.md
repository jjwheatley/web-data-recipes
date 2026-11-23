# Get new jobs from target companies every day

Track a list of companies and receive only roles you haven't seen before. This is useful for recruiters, job boards, job seekers and sales teams that treat hiring as a buying signal.

**Tool:** [Career Page Jobs](https://apify.com/squarish_altruism/ats-jobs)

It reads the public job feeds of 12 hiring systems: Greenhouse, Lever, Ashby, SmartRecruiters, Workable, Recruitee, Personio, Teamtailor, Breezy HR, Pinpoint, Rippling and Gem. Workday, Taleo, iCIMS and BambooHR are not supported.

## 1. Paste this input

```json
{
  "companies": [
    "greenhouse:airbnb",
    "https://jobs.ashbyhq.com/ashby"
  ],
  "keywords": ["engineer"],
  "includeDescription": false,
  "onlyNew": true,
  "monitorName": "target-companies"
}
```

Replace the companies with your own. You can use a job-board URL, a shorthand such as `lever:acme`, or a company's careers page if it embeds a supported board. To narrow the results, add `locations`, `departments` or `"remoteOnly": true`.

## 2. Run it once

**The first run returns every current job that matches, and you pay for those.** To limit it, add `"postedWithinDays": 7`. Later runs with the same `monitorName` return only jobs they haven't returned before.

In our test, the first run returned 88 matching jobs ($0.18). An immediate second run returned 0 and cost nothing.

## 3. Put it on a schedule

Save the input as a task, then add the task to a daily schedule in Apify Console.

## 4. Send the jobs somewhere useful

Add an integration to the task, such as Slack, email, a webhook, Zapier, Make or n8n, to pass new jobs into a sheet, CRM or channel. In Zapier, Make or n8n, add a filter step to skip runs with no new jobs.

## What you get

One row per job, in the same format for every hiring system. This is real output:

```json
{
  "ats": "ashby",
  "company": "ashby",
  "title": "Senior Security Engineer - Corporate Security",
  "department": "Security & IT",
  "location": "Remote - European Union",
  "remote": true,
  "postedAt": "2026-11-20T21:29:20.502Z",
  "url": "https://jobs.ashbyhq.com/Ashby/e1032adf-e8ac-4285-ac91-cdadcdf4e7c6",
  "salary": {
    "min": 108000,
    "max": 145000,
    "currency": "EUR",
    "interval": "1 YEAR",
    "summary": "€108K - €145K"
  }
}
```

Salary appears only where the company publishes it.

## Cost

$0.002 per job returned, or $2 per 1,000. Jobs removed by your filters, jobs already seen and companies with no board found are free.
