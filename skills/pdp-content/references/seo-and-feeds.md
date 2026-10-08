# PDP SEO, Structured Data & Technical Essentials

## On-page SEO for product pages
- **Search intent on a PDP is transactional.** The page must make buying easy and answer the purchase questions. Don't turn PDPs into blog posts.
- **Keywords come from shopper language:** search terms, retailer search data, reviews. Use them naturally in the title, H1, first sentence and bullets. Keyword density is not a meaningful target. Stuffing hurts both readability and rankings.
- **Uniqueness.** Manufacturer-supplied descriptions reused across many sites are duplicate content. Write unique copy for brand.com and for priority SKUs at least.
- **Variants:**
  - Prefer one canonical parent page with selectable variants where the variants differ only in color or size.
  - Give variants their own indexable pages only when shoppers search for them specifically and the pages carry distinct content.
- **Internal links:** breadcrumbs that follow the primary category, links to related and complementary products, and links back to the category.

## Structured data (JSON-LD) for brand.com
Mark up only what is visible on the page, and keep it consistent with the page and the feed.

**Product properties:**
- `name`, `image`, `description`, `sku`, `brand`
- identifiers: `gtin`, `mpn`
- `offers`: an `Offer` with `price`, `priceCurrency`, `availability` and `url`, plus `itemCondition` where relevant
- `aggregateRating` and `review`: **only** if genuine, first-party reviews are displayed on the page
- `shippingDetails` (`OfferShippingDetails`) and `hasMerchantReturnPolicy` (`MerchantReturnPolicy`) where applicable

**Variants:** `ProductGroup` with `variesBy` and `hasVariant`, linking each variant `Product`.

**Also:** `BreadcrumbList`.

```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "<from attr.product_name>",
  "image": ["<url>"],
  "description": "<visible description>",
  "sku": "<attr.sku>",
  "gtin": "<attr.gtin — only if it exists>",
  "brand": { "@type": "Brand", "name": "<attr.brand>" },
  "offers": {
    "@type": "Offer",
    "url": "<canonical url>",
    "priceCurrency": "USD",
    "price": "<from commerce system>",
    "availability": "<from commerce system, as a schema.org ItemAvailability URL, e.g. https://schema.org/InStock>",
    "itemCondition": "https://schema.org/NewCondition"
  }
}
```

**Rules:**
- Never fabricate ratings, reviews, GTINs or prices.
- Validate the markup with a structured-data testing tool, such as Google's Rich Results Test or the Schema.org validator.
- After launch, monitor the merchant listing and product snippet reports in Search Console.
- Don't promise FAQ or HowTo rich results. HowTo rich results were retired in 2023, and Google has since stopped showing FAQ rich results in Search (verify current status in Google Search Central). Markup is still valid schema.org, but it earns no Google rich result.

## Technical essentials
- **The main content must be in the server-rendered HTML:** product name, price, availability, key copy and structured data. Search and AI crawlers may not run JavaScript reliably.
- **Canonicals:** variant and parameter URLs point to the canonical PDP, unless a variant deliberately has its own page.
- **Out-of-stock and discontinued products:**
  - Temporarily out of stock: keep the page, mark availability correctly, and offer alternatives.
  - Discontinued: redirect to the closest replacement or category, or return 404/410. Never redirect everything to the homepage.
- **Hand-offs to the site and SEO team:** content work can't fix these, but you should flag them.
  - Core Web Vitals (LCP ≤ 2.5s, INP ≤ 200ms, CLS ≤ 0.1 at the 75th percentile).
  - A lazy-loaded hero image.
  - Index bloat from faceted navigation.
  - `hreflang` errors (e.g., `uk` instead of `en-gb`).

## Images
- The main image must accurately show the exact variant sold. Retailers have their own main-image rules (background, fill, no text), so check them.
- **Secondary images** should answer questions: scale (in hand or in use), details, materials, what's in the box, dimensions graphics using real values.
- **Filenames and alt text** should be descriptive and specific to the variant.
