# Transcribe podcast episodes to text and subtitles

Turn the latest episodes of a podcast into searchable text with timestamps, plus SRT and VTT subtitle files.

**Tool:** [Audio & Video Transcription](https://apify.com/squarish_altruism/transcribe)

> **Don't put this recipe on a schedule.** The tool doesn't yet remember which episodes it has transcribed, so a scheduled run would transcribe and charge for the same episodes again.

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

## 2. Run the full job

When the sample looks good, raise the limits:

```json
{
  "sources": ["https://feeds.npr.org/510289/podcast.xml"],
  "maxEpisodesPerFeed": 3,
  "maxMinutesPerFile": 180,
  "language": "en"
}
```

Setting the language improves accuracy. Only transcribe media you have the right to process.

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
