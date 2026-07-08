[Bestbuy Scraper](https://apify.com/fatihai-tools/bestbuy-scraper?fpr=data)

# Best Buy Scraper - Product Data Extraction

This scraper extracts product data from Best Buy's public pages, including product names, prices, and availability. It's useful for businesses that need to monitor product prices or gather market research data.

## Features

- Fast and efficient scraping using got-scraping
- Built-in proxy support to avoid blocks
- Automatic pagination handling
- Pay-per-result pricing (only pay for what you get)
- Rate limiting to respect target site
- Retry logic for reliability

## Output Data

Each result contains:

- **product_name**
- **price**
- **availability**
- **product_id**
- **brand**
- **model**

## Use Cases

- Market research
- Price monitoring

## Input Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `searchQuery` | string | Search term to find items |
| `maxItems` | integer | Maximum results (default: 100) |
| `proxy` | object | Proxy configuration |

## Example Output

```
{
    "product_name": "example value",
    "price": "example value",
    "availability": "example value",
    "product_id": "example value",
    "brand": "example value",
    "model": "example value",
    "scrapedAt": "2026-02-22T12:00:00.000Z"
}
```

## Pricing

This actor uses pay-per-result pricing:

- **$0.01 per result** - you only pay for scraped data
- **$0.05 per actor start**

## Tips

- Start with a small `maxItems` (10-20) to test
- Use proxy for best results and to avoid rate limits
- The scraper respects rate limits automatically

## Support

If you have any issues, please open an issue on the actor page.