[Bestbuy Scraper](https://apify.com/sovereigntaylor/bestbuy-scraper?fpr=data)

# Best Buy Product Scraper

Scrape Best Buy product listings from search results and individual product pages. Extract full product details including titles, current and original prices, star ratings, review counts, availability status, brand names, SKU numbers, model numbers, detailed specifications, image URLs, and direct product links.

## Features

- **Multi-source data extraction** -- uses JSON-LD structured data, embedded application state (`__NEXT_DATA__`, `__INITIAL_STATE__`), and HTML parsing for maximum reliability
- **Full product details** -- title, price, original price, savings, rating, reviews, availability, brand, SKU, model, specs, images, URL, description
- **Three scraping modes** -- keyword search, category browsing, and direct product URL scraping
- **Multi-keyword search** -- provide multiple search terms and scrape them all in one run
- **Price filtering** -- set a maximum price to only capture products within your budget
- **Category filtering** -- narrow results by Best Buy department (30+ categories supported)
- **Smart pagination** -- automatically follows Best Buy search pages (up to 42 pages per search)
- **Product page enrichment** -- optionally fetches individual product pages for full specifications
- **Anti-bot handling** -- rotates 12 realistic User-Agent strings with full browser headers
- **Deduplication** -- skips duplicate products across pages and search terms using SKU/title tracking
- **CAPTCHA detection** -- detects blocks and stops gracefully, preserving all data collected
- **Proxy support** -- optional Apify proxy configuration (residential proxies recommended)
- **Pay-per-event** -- $0.004 per product scraped

## Use Cases

### Price Monitoring and Alerts

Track Best Buy product prices over time to detect sales, price drops, clearance events, and seasonal deals. Build automated price drop alerts for specific products or categories.

### Competitor Analysis

Compare pricing, ratings, and availability across Best Buy's product catalog. Monitor how competitor products are positioned and priced. Track new product launches.

### Product Research and Market Analysis

Evaluate market demand by analyzing review counts, ratings, brand distribution, and price ranges. Identify product gaps, trending categories, and consumer preferences.

### E-commerce Intelligence

Gather product catalog data for assortment planning, inventory optimization, and cross-retailer price comparison. Feed data into business intelligence tools.

### Deal Finding and Arbitrage

Find products with large discounts, open-box deals, clearance items, and underpriced products for resale or personal use. Monitor savings percentages across categories.

### Brand and SKU Monitoring

Track how your brand's products appear on Best Buy -- pricing accuracy, availability status, review sentiment, and competitive positioning.

### Specification Comparison

Collect detailed product specifications for technical comparison across brands and models. Ideal for electronics research and review sites.

## Input

| Field | Type | Default | Description |
| --- | --- | --- | --- |
| `searchTerms` | Array of Strings | `["laptop"]` | List of search keywords to scrape |
| `productUrls` | Array of Strings | `[]` | Direct Best Buy product page URLs to scrape |
| `category` | String | `""` | Category/department filter (see list below) |
| `maxPrice` | Integer | `0` | Max price filter in USD (0 = no limit) |
| `maxResults` | Integer | `500` | Max products to scrape (0 = unlimited) |
| `proxy` | Object | *(none)* | Apify proxy configuration |

### Supported Categories

Computers & Tablets, Laptops, Desktops, Tablets, TV & Home Theater, TVs, Cell Phones, Audio, Headphones, Speakers, Cameras & Camcorders, Video Games, Gaming, Appliances, Smart Home, Wearable Technology, Car Electronics, Movies & Music, Musical Instruments, Office Supplies, Printers, Networking, Storage, Monitors, PC Gaming, Drones, Electric Transportation.

You can also pass a Best Buy category ID directly (e.g., `abcat0500000`).

## Input Examples

### Basic laptop search

```
{
    "searchTerms": ["laptop"],
    "maxResults": 50
}
```

### Multiple search terms with price filter

```
{
    "searchTerms": ["4k tv", "oled tv", "gaming monitor"],
    "maxPrice": 1000,
    "maxResults": 200
}
```

### Category-filtered search

```
{
    "searchTerms": ["wireless earbuds"],
    "category": "Audio",
    "maxResults": 100
}
```

### Direct product URL scraping

```
{
    "productUrls": [
        "https://www.bestbuy.com/site/apple-macbook-air-15-laptop-m3-chip-8gb-memory-256gb-ssd/6565837.p",
        "https://www.bestbuy.com/site/samsung-65-class-s90d-series-oled-4k-smart-tizen-tv/6576506.p"
    ],
    "maxResults": 10
}
```

### Large scrape with residential proxies

```
{
    "searchTerms": ["gaming laptop", "gaming desktop", "gaming monitor"],
    "category": "PC Gaming",
    "maxResults": 1000,
    "proxy": {
        "useApifyProxy": true,
        "apifyProxyGroups": ["RESIDENTIAL"]
    }
}
```

### Budget electronics under $200

```
{
    "searchTerms": ["bluetooth speaker", "wireless mouse", "usb-c hub"],
    "maxPrice": 200,
    "maxResults": 300
}
```

## Output

Each product is saved to the default dataset with the following fields:

```
{
    "title": "Apple MacBook Air 15\" Laptop - M3 chip - 8GB Memory - 256GB SSD - Midnight",
    "price": 1049.99,
    "originalPrice": 1299.99,
    "savings": 250.00,
    "savingsPercent": "19%",
    "rating": 4.8,
    "reviews": 3421,
    "availability": "In Stock",
    "brand": "Apple",
    "sku": "6565837",
    "model": "MRXN3LL/A",
    "specs": {
        "Processor": "Apple M3 chip",
        "Memory": "8GB unified memory",
        "Storage": "256GB SSD",
        "Display": "15.3-inch Liquid Retina",
        "Battery Life": "Up to 18 hours",
        "Weight": "3.3 pounds",
        "Operating System": "macOS"
    },
    "images": [
        "https://pisces.bbystatic.com/image2/BestBuy_US/images/products/6565/6565837_sd.jpg"
    ],
    "url": "https://www.bestbuy.com/site/apple-macbook-air-15-laptop-m3-chip-8gb-memory-256gb-ssd/6565837.p",
    "description": "MacBook Air sails through work and play with the powerful M3 chip...",
    "currency": "USD",
    "searchTerm": "macbook air",
    "scrapedAt": "2026-03-01T12:00:00.000Z"
}
```

### Output Fields

| Field | Type | Description |
| --- | --- | --- |
| `title` | String | Full product title |
| `price` | Number/null | Current selling price in USD |
| `originalPrice` | Number/null | Original or "was" price (if discounted) |
| `savings` | Number/null | Dollar amount saved |
| `savingsPercent` | String/null | Percentage discount (e.g., "19%") |
| `rating` | Number/null | Average star rating (0.0 - 5.0) |
| `reviews` | Number | Number of customer reviews |
| `availability` | String | Stock status: In Stock, Out of Stock, Pre-order, Pickup Only, Ships to Home, Backordered, Clearance, Open Box, Refurbished |
| `brand` | String/null | Product brand name |
| `sku` | String/null | Best Buy SKU number |
| `model` | String/null | Manufacturer model number |
| `specs` | Object | Key-value pairs of product specifications |
| `images` | Array | Product image URLs |
| `url` | String | Direct link to product page |
| `description` | String/null | Product description (up to 1000 chars) |
| `currency` | String | Currency code (always "USD") |
| `searchTerm` | String | The search term or "direct-url" |
| `scrapedAt` | String | ISO 8601 timestamp |

## Dataset Views

The actor provides three pre-configured dataset views:

1. **Products** -- full product table with title, price, rating, reviews, availability, brand, SKU, model, and URL
2. **Price Comparison** -- focused view showing title, current price, original price, savings amount, savings percentage, brand, and rating
3. **Specifications** -- technical view with title, brand, model, SKU, specifications object, price, and URL

## Performance Tips

1. **Use residential proxies** -- Best Buy has anti-bot protections. Residential proxies are strongly recommended for scraping more than 50 products. Set `proxy: { "useApifyProxy": true, "apifyProxyGroups": ["RESIDENTIAL"] }`.
2. **Start small** -- test with `maxResults: 10` first to verify the scraper works for your search terms and categories.
3. **Be specific with search terms** -- "gaming laptop RTX 4060" returns more relevant results than "laptop" and requires fewer pages.
4. **Use the price filter** -- setting `maxPrice` reduces the number of products to process, making scrapes faster and cheaper.
5. **Use category filters** -- narrowing by category improves result relevance and reduces pages scraped.
6. **Multiple search terms** -- instead of one broad search, use multiple specific terms for better coverage (e.g., `["macbook air", "macbook pro", "imac"]` instead of `["apple computer"]`).
7. **Direct URLs for specific products** -- if you already know which products you want, use `productUrls` for the fastest and most reliable scraping.
8. **Off-peak scraping** -- Best Buy's anti-bot systems are less aggressive during off-peak hours (late night / early morning US time zones).

## Rate Limiting and Blocks

Best Buy employs anti-bot protections including Akamai Bot Manager. This actor handles them by:

- Rotating 12 realistic browser User-Agent strings per request
- Sending complete browser headers (sec-ch-ua, sec-fetch-*, referer, cookies, etc.)
- Limiting to 20 requests/minute by default
- Adding random delays (300-1500ms) between requests to mimic human browsing
- Detecting CAPTCHA, challenge, and block pages with graceful shutdown
- Supporting proxy rotation via Apify's residential proxy infrastructure
- Retrying failed requests up to 3 times with exponential backoff

If you see "Anti-bot protection detected" in the logs, the scraper saves all data collected so far and exits cleanly. Switch to residential proxies to resolve this.

## Pricing (Pay Per Event)

This actor uses Apify's pay-per-event pricing model. You are charged **$0.004 per product** successfully scraped and saved to the dataset. There is no charge for failed requests, filtered-out products, or duplicate products.

Example costs:

- 100 products: $0.40
- 500 products: $2.00
- 1,000 products: $4.00
- 5,000 products: $20.00

## Legal Notice

This actor is provided as a technical tool for data collection. Users are responsible for ensuring their use complies with Best Buy's Terms of Use, robots.txt directives, and all applicable laws including the Computer Fraud and Abuse Act (CFAA). This tool is designed for personal research, price monitoring, and legitimate business analysis purposes. Please review Best Buy's Terms of Service before use. Do not use this tool to scrape personal data or for any purpose that violates applicable privacy regulations.

## Integration — Python

```
from apify_client import ApifyClient

client = ApifyClient("YOUR_API_TOKEN")
run = client.actor("sovereigntaylor/bestbuy-scraper").call(run_input={
    "searchTerm": "bestbuy",
    "maxResults": 50
})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(f"{item.get('title', item.get('name', 'N/A'))}")
```

## Integration — JavaScript

```
import { ApifyClient } from 'apify-client';
const client = new ApifyClient({ token: 'YOUR_API_TOKEN' });

const run = await client.actor('sovereigntaylor/bestbuy-scraper').call({
    searchTerm: 'bestbuy',
    maxResults: 50
});

const { items } = await client.dataset(run.defaultDatasetId).listItems();
items.forEach(item => console.log(item.title || item.name || 'N/A'));
```