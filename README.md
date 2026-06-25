[Hackernews Scraper](https://apify.com/skystone_labs/hackernews-scraper?fpr=data)

# Hacker News Scraper

Extract stories, comments, and discussion data from [Hacker News](https://news.ycombinator.com). Pay only for successfully scraped items ($1 per 1,000 items).

## Features

- **Fast extraction** - Optimized for speed with lightweight page parsing
- **Story data** - Titles, links, scores, authors, comment counts
- **Comment extraction** - Optional full comment thread scraping
- **Type detection** - Identifies stories, Ask HN, Show HN, and jobs
- **Pagination** - Automatically follows "More" links for deeper scraping

## Use Cases

- Tech trend analysis and monitoring
- Content research for newsletters
- Developer community sentiment analysis
- Startup and launch tracking
- Academic research on tech communities

## Input Parameters

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `startUrls` | array | - | HN URLs to scrape (front page, new, ask, show, jobs) |
| `maxResults` | integer | 100 | Maximum items to scrape (0 = unlimited) |
| `extractComments` | boolean | false | Extract comment threads from stories |
| `useCamoufox` | boolean | false | Enable anti-detect browser (not needed for HN) |

## Output Schema

```
{
  "url": "https://news.ycombinator.com/item?id=12345",
  "title": "Show HN: My new open source project",
  "link": "https://github.com/example/project",
  "score": 234,
  "author": "pg",
  "commentCount": 89,
  "age": "3 hours ago",
  "rank": 1,
  "type": "show",
  "scrapedAt": "2024-01-15T10:30:00.000Z"
}
```

## Pricing

**$0.001 per successfully scraped item** ($1 per 1,000 items)

No charges for failed requests.

## Example Usage

```
{
  "startUrls": [
    {"url": "https://news.ycombinator.com/"},
    {"url": "https://news.ycombinator.com/newest"}
  ],
  "maxResults": 200,
  "extractComments": false
}
```

## Limitations

- HN may rate-limit very aggressive scraping
- Comment extraction increases scraping time significantly
- Very old stories may have limited data

## Support

For issues or feature requests, please contact SkyStone Labs support.