[Hackernews Scraper](https://apify.com/cryptosignals/hackernews-scraper?fpr=data)

# Hacker News Scraper: Stories, Comments & Users Free

The most comprehensive **Hacker News scraper** on Apify. Extract HN stories, comments, and user profiles at scale. Search Hacker News posts by keyword. Export to JSON, CSV, or Excel. Built on the official HN Firebase API for maximum reliability.

## Why Use This Hacker News Scraper?

- **Tech Trend Analysis** - Track what's trending on Hacker News. Monitor emerging technologies, frameworks, and tools before they go mainstream.
- **Startup Scouting** - Discover new startups from Show HN and Launch HN posts. Get early intelligence on companies before they hit the press.
- **Hiring Intelligence** - Monitor "Who is Hiring" threads and job postings. Analyze which companies are hiring and for what roles.
- **Competitive Research** - Track mentions of competitors, products, or technologies. See what the developer community thinks.
- **Content Curation** - Build datasets of top-performing HN content. Understand what resonates with the tech community.
- **Academic Research** - Analyze HN data for sentiment analysis, trend detection, and community dynamics research.

## Features

| Feature | Description |
| --- | --- |
| **6 Story Categories** | Top, New, Best, Ask HN, Show HN, Jobs |
| **Full-Text Search** | Search HN posts via Algolia API |
| **Comment Trees** | Fetch full comment threads for any story |
| **User Profiles** | Get karma, about, and submission counts |
| **Pagination** | Control output size with maxItems |
| **Concurrent Fetching** | Fast parallel requests with rate limiting |
| **Multiple Export Formats** | JSON, CSV, Excel, XML via Apify |

## Input Configuration

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `category` | string | `"top"` | Story category: `top`, `new`, `best`, `ask`, `show`, `jobs`, or `search` |
| `searchQuery` | string | `""` | Search query (required when category is `search`) |
| `maxItems` | integer | `100` | Maximum stories to return (1-500) |
| `includeComments` | boolean | `false` | Fetch comment trees for each story |
| `maxCommentsPerStory` | integer | `50` | Max comments per story |
| `scrapeType` | string | `"stories"` | Output type: `stories`, `users`, or `both` |

## Output - Stories

```
{
  "id": 12345678,
  "title": "Show HN: I built an AI-powered code reviewer",
  "url": "https://example.com/project",
  "text": null,
  "author": "techfounder",
  "score": 342,
  "commentCount": 156,
  "createdAt": "2025-12-15T10:30:00.000Z",
  "storyType": "show",
  "hnUrl": "https://news.ycombinator.com/item?id=12345678"
}
```

## Output - Users

```
{
  "username": "techfounder",
  "karma": 15420,
  "about": "Building cool stuff. Previously at BigCorp.",
  "createdAt": "2015-03-10T08:00:00.000Z",
  "submittedCount": 892
}
```

## Output - Comments (when includeComments is true)

```
{
  "id": 12345679,
  "author": "commenter1",
  "text": "This is a great project! I've been looking for something like this.",
  "createdAt": "2025-12-15T11:00:00.000Z",
  "parentId": 12345678
}
```

## Example Use Cases

### Get Top 50 HN Stories

```
{
  "category": "top",
  "maxItems": 50
}
```

### Search for AI Startup Posts

```
{
  "category": "search",
  "searchQuery": "AI startup launch",
  "maxItems": 100
}
```

### Get Ask HN with Comments

```
{
  "category": "ask",
  "maxItems": 20,
  "includeComments": true,
  "maxCommentsPerStory": 100
}
```

### Get Stories + Author Profiles

```
{
  "category": "best",
  "maxItems": 30,
  "scrapeType": "both"
}
```

## API Usage Examples

### JavaScript

```
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: 'YOUR_API_TOKEN' });
const run = await client.actor('cryptosignals/hackernews-scraper').call({
    category: 'top',
    maxItems: 50,
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

### Python

```
from apify_client import ApifyClient

client = ApifyClient("YOUR_API_TOKEN")
run = client.actor("cryptosignals/hackernews-scraper").call(run_input={
    "category": "top",
    "maxItems": 50,
})
items = list(client.dataset(run["defaultDatasetId"]).iterate_items())
print(items)
```

### cURL

```
curl "https://api.apify.com/v2/acts/cryptosignals~hackernews-scraper/runs" \
  -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  -d '{"category": "top", "maxItems": 50}'
```

## About the Data Source

This scraper uses the **official Hacker News Firebase API** ([https://github.com/HackerNews/API](https://github.com/HackerNews/API)) and the **Algolia HN Search API** for keyword search. These are public, free APIs provided by Y Combinator. No scraping of the website is involved -- all data comes from official endpoints, ensuring reliability and compliance.

## FAQ

**Q: Is this scraper free to use?**
A: The actor itself is free. You only pay for Apify compute units based on your plan.

**Q: How often is the data updated?**
A: The HN API provides real-time data. Stories and scores are current at the time of scraping.

**Q: Can I scrape historical data?**
A: Use the search feature to find older posts by keyword. The Firebase API only provides current story lists.

**Q: Why are some comments missing?**
A: Deleted or dead (flagged) comments are filtered out automatically.

**Q: What's the rate limit?**
A: The official HN API has no documented rate limit. The scraper uses concurrent requests with sensible batching.

**Q: Can I schedule this to run automatically?**
A: Yes! Use Apify's scheduling feature to run the scraper hourly, daily, or on any custom schedule.

## Tags

hacker news, hn scraper, tech news, startup intelligence, developer tools, comment scraper, user profiles, tech trends, Y Combinator, hackernews api, hn data extraction