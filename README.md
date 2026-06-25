[Hackernews Scraper](https://apify.com/sovereigntaylor/hackernews-scraper?fpr=data)

# Hacker News Scraper

Scrape Hacker News stories using the official Firebase API. Fetch top, new, best, ask, show, or job stories with scores, authors, and comments. No IP blocking — uses HN's public API.

## Features

- Scrape top, new, best, ask, show, and job stories
- Uses official HN Firebase API (100% reliable, no blocking)
- Extract titles, URLs, scores, authors, timestamps
- Get comment counts and optionally fetch top comments
- Lightning fast (2-5 seconds for 30 stories)
- Configurable result limits (up to 500)

## Input

| Field | Type | Default | Description |
| --- | --- | --- | --- |
| mode | string | "top" | Story category: top, new, best, ask, show, jobs |
| maxResults | number | 30 | Max stories to return (1-500) |
| includeComments | boolean | false | Fetch top 5 comments per story |

## Output

```
{
  "rank": 1,
  "title": "Show HN: I built an AI code editor",
  "url": "https://example.com/ai-editor",
  "score": 542,
  "author": "developer123",
  "commentCount": 187,
  "time": "2026-03-01T10:30:00Z",
  "type": "story",
  "hnUrl": "https://news.ycombinator.com/item?id=12345"
}
```

## Use Cases

- **Tech Trend Monitoring**: Track what developers are talking about
- **Content Curation**: Find top-performing tech articles
- **Competitive Intelligence**: Monitor mentions of products or companies
- **Market Research**: Analyze developer sentiment and interests
- **Data Analysis**: Build datasets of tech news over time

## Pricing

Pay per result — you only pay for what you scrape. See the Pricing tab for details.

## Example

Get top 50 stories with comments:

```
{
  "mode": "top",
  "maxResults": 50,
  "includeComments": true
}
```

## Integration — Python

```
from apify_client import ApifyClient

client = ApifyClient("YOUR_API_TOKEN")
run = client.actor("sovereigntaylor/hackernews-scraper").call(run_input={
    "searchTerm": "hackernews",
    "maxResults": 50
})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(f"{item.get('title', item.get('name', 'N/A'))}")
```

## Integration — JavaScript

```
import { ApifyClient } from 'apify-client';
const client = new ApifyClient({ token: 'YOUR_API_TOKEN' });

const run = await client.actor('sovereigntaylor/hackernews-scraper').call({
    searchTerm: 'hackernews',
    maxResults: 50
});

const { items } = await client.dataset(run.defaultDatasetId).listItems();
items.forEach(item => console.log(item.title || item.name || 'N/A'));
```