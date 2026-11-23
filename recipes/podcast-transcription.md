# Transcribe every new podcast episode automatically

Get each new episode as searchable text with timestamps, plus SRT and VTT subtitle files. You pay only for episodes that are new.

**Tool:** [Audio & Video Transcription](https://apify.com/squarish_altruism/transcribe)

## 1. Try one minute first

```json
{
  "sources": ["https://feeds.npr.org/510289/podcast.xml"],
  "maxEpisodesPerFeed": 1,
  "maxMinutesPerFile": 1,
  "language": "en"
}
```

Replace the feed with your own. You can use a podcast RSS feed, an Apple Podcasts show link, or a direct audio or video file. YouTube, TikTok and Spotify links are not supported. This test costs $0.01.

## 2. Turn on new episodes only

When the sample looks good, use this input:

```json
{
  "sources": ["https://feeds.npr.org/510289/podcast.xml"],
  "onlyNewEpisodes": true,
  "monitorName": "my-podcasts",
  "maxEpisodesPerFeed": 1,
  "maxMinutesPerFile": 180,
  "language": "en"
}
```

Keep the same `monitorName` on every run, because that is how the tool remembers what it has done.

- **The first run** transcribes the newest episode. Older episodes are ignored, so you don't pay for the back catalogue. To start with more, raise `maxEpisodesPerFeed`.
- **Later runs** transcribe only episodes published since. A run with nothing new costs nothing.
- **Several new episodes at once:** any above `maxEpisodesPerFeed` are picked up on the next run.

In our test, the first run transcribed one episode, an immediate second run found nothing and charged nothing, and a simulated new episode was transcribed once.

## 3. Put it on a schedule

Save the input as a task, then add the task to a **daily** schedule in Apify Console. Leave enough time for one run to finish before the next starts, because overlapping runs could both pick up the same new episode.

## 4. Send the transcripts somewhere useful

Add an integration to the task, such as Slack, email, a webhook, Zapier, Make or n8n, to pass each transcript to your notes, CMS or AI tool. In Zapier, Make or n8n, add a filter step to skip runs with no new episodes.

Only transcribe media you have the right to process.

## What you get

One row per file, with links to SRT, VTT and TXT files. This is real output from a public-domain speech clip:

```json
{
  "durationSeconds": 11,
  "billedMinutes": 1,
  "engine": "local:whisper-base",
  "language": "en",
  "words": 22,
  "text": "And so my fellow Americans ask not what your country can do for you, ask what you can do for your country.",
  "segments": [
    {
      "start": 0,
      "end": 7.6,
      "text": "And so my fellow Americans ask not what your country can do for you,"
    }
  ]
}
```

## Cost

| Engine | Price per audio minute | A 30-minute episode |
|---|---|---|
| Built-in Whisper | $0.01 | $0.30 |
| Your own Groq or OpenAI-compatible key | $0.002, plus your provider's charges | $0.06, plus your provider's charges |

Files that fail to download and minutes beyond `maxMinutesPerFile` are free.
