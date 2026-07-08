[Bestbuy Scraper](https://apify.com/benthepythondev/bestbuy-scraper?fpr=data)

# Best Buy Scraper

Extract product data from Best Buy including prices, deals, ratings, reviews, specifications, and availability.

## Features

- **Search Mode**: Search products by keywords with filters
- **Category Mode**: Scrape entire product categories
- **Direct URLs Mode**: Scrape specific product pages
- **Price Filtering**: Set min/max price range
- **Brand Filtering**: Filter by specific brands
- **Rating Filtering**: Only get products above a minimum rating
- **Deal Hunting**: Filter for on-sale or open-box items only
- **Detailed Specs**: Optionally scrape full product specifications

## Use Cases

- **Price Monitoring**: Track Best Buy prices for price drop alerts
- **Market Research**: Analyze product pricing and ratings
- **Competitor Analysis**: Compare electronics pricing
- **Deal Hunting**: Find the best sales and open-box deals
- **Inventory Tracking**: Monitor product availability

## Output Data

Each product includes:

| Field | Description |
| --- | --- |
| skuId | Best Buy SKU ID |
| title | Product name |
| brand | Brand name |
| modelNumber | Model number |
| price | Current price |
| originalPrice | Regular price (if on sale) |
| savings | Dollar savings |
| savingsPercent | Percentage savings |
| onSale | Whether item is on sale |
| rating | Customer rating (1-5) |
| reviewCount | Number of reviews |
| url | Product page URL |
| imageUrl | Main product image |
| availability | Pickup/shipping availability |
| specifications | Detailed specs (if enabled) |
| features | Product features list |
| scrapedAt | Timestamp |

## Example Input

```
{
  "mode": "search",
  "searchQuery": "gaming laptop",
  "minPrice": 800,
  "maxPrice": 1500,
  "brands": ["ASUS", "MSI", "Razer"],
  "minRating": 4,
  "onSaleOnly": true,
  "maxProducts": 50
}
```

## Pricing

Pay only for results - $5.00 per 1,000 products scraped.