# bridge-insights

The published Insight artefact for the [Bridge](https://github.com/AiT0xin/bridge-app) iOS app.

`insights.json` holds **aggregate figures only**: per brand, how many times it was
mentioned across watch publications and enthusiast forums in a rolling window, and
an estimated sentiment for those mentions.

## What is not in here

No user data. No personal data. No post text, author names or usernames. No
application source. Bridge has no accounts and collects nothing about the people
using it, and nothing about a reader is involved in producing this file.

The source text is read, aggregated and discarded by a scheduled job. Only the
counts below survive it.

## Format

```json
{
  "schemaVersion": 1,
  "generatedAt": "2026-08-09T21:14:00Z",
  "windowDays": 7,
  "sources": ["Hodinkee", "WatchUSeek", "..."],
  "brands": [
    { "id": "rolex", "mentions": 18, "scoredMentions": 15, "sentiment": 0.40 }
  ]
}
```

`sentiment` runs from -1 to +1 and is **absent** when too few mentions carried an
opinion to average. Absent is not the same as zero, and the app renders the two
differently.

Display labels are not in this file. The app resolves every `id` against its own
catalogue and ignores ids it does not recognise, so this artefact cannot put
arbitrary text on anyone's screen.

## Accuracy

Mention counts are exact string matching. Sentiment is estimated by three models
(VADER, TweetNLP RoBERTa, nlptown BERT) and will sometimes be wrong. The sample is
watch media and enthusiast forums, which is not the general public, and coverage of
that kind skews positive. Differences between brands carry more meaning than any
single figure.

Generated automatically. Do not edit by hand.
