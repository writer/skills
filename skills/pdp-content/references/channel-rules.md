# Channel Rules for Product Content

> **Retailer and marketplace rules change frequently, and many vary by category.** Always prefer the user's current style guide, template or the channel's live documentation over the defaults below. Where a limit isn't known for certain, say so and ask. Don't guess. In the output, note which rule source you used (for example "Amazon category style guide supplied by user, dated …" or "default; verify").

## Brand.com (owned DTC site)
The most freedom, and the most responsibility.
- Full anatomy: title, benefits, description, specs, FAQ, rich media, reviews.
- **Unique content per page.** Don't let retailer copy and brand.com copy be identical.
- **SEO elements:** unique meta title and description, descriptive URL slug, one H1 (normally the product name), internal links to the category and related products, breadcrumbs.
- **Structured data** consistent with the visible page. See `seo-and-feeds.md`.
- **Accessibility:** alt text, good contrast, readable structure, and tables that are real tables.

## Google Merchant Center / Shopping feeds
- **Always required:** `id`, `title`, `description`, `link`, `image_link`, `availability`, `price`.
- **Required in specific cases:**
  - `brand`: for new products (except movies, books and music).
  - `gtin`: whenever the manufacturer assigned one.
  - `mpn`: when there is no GTIN.
  - `condition`: for used or refurbished items.
  - `item_group_id`: for variants in several major markets, including the US, UK, DE, FR, JP and BR.
- **Never fabricate identifiers.** If none exists, use `identifier_exists` correctly.
- **Verify against the live product data specification**, since requirements vary by country and category.
- **Title:** maximum 150 characters. The first part shows most often, so front-load brand + product type + key attributes (size, color, material, count).
- **Description:** maximum 5,000 characters. Describe the product only; no promotional text, links or other products.
- **Not allowed** in titles or descriptions: promotional text such as "free shipping" or "sale", ALL CAPS for emphasis, gimmicky characters.
- **Data must match the landing page exactly:** price, availability, variant. Mismatches lead to disapprovals.
- **Variants:** one item per variant, linked with `item_group_id`, with variant attributes (color, size, material, pattern) set.
- **Categories:** use the most specific `google_product_category`, and a full `product_type` path from your own taxonomy.
- **Images:** an accurate representation of the product, with no promotional overlays or watermarks on the main image.
- **Freshness:** keep price and availability in sync. Use supplemental feeds for overrides rather than editing source data by hand.

## Amazon
Verify against the current category style guide and Seller Central or Vendor Central policy for the category.
- **Title:** category-specific length limits and formatting rules, which tightened in recent years. Restricted special characters, no promotional phrases, no subjective claims, and no excessive repetition of words. Typical pattern: brand + product line + product type + key attributes (size, color, count). **Check the current limit for the category.**
- **Bullets ("About this item"):** typically up to five. Lead with the benefit, back it with a fact, one topic per bullet. No pricing, shipping, promotional or company information. No unsubstantiated claims.
- **Description and A+ (enhanced brand content).** A+ follows its own guidelines. Typically it allows:
  - no pricing, promotions or time-sensitive language
  - no quotes or reviews from customers or private individuals (a small number of attributed quotes from well-known publications or public figures may be allowed)
  - no guarantee, warranty or off-Amazon return or refund language
  - no comparisons with competitors' products (comparison charts are limited to your own products)

  Verify against the current A+ guidelines.

  **Planning A+ modules:**
  - Map each module to one shopper question: what it is, why it's different, how to use it, which variant to choose, what's included.
  - Use a comparison chart across your own range to help shoppers pick a variant.
  - Image text must follow the same claims rules as the copy.
  - Keep the text in images short and readable on mobile.
- **Backend search terms:** limited by bytes (verify the current limit). No brand names that aren't yours, no competitor brands, no repetition of words already in the title.
- **Claims:** restricted categories (pesticides and "antimicrobial" claims, supplements, cosmetics, children's products, medical devices) have special rules. Claims in ads must match the PDP.
- **Reviews:** Amazon prohibits incentivized reviews outside its own programs. Never ask for reviews that are conditional on sentiment.

## Walmart, Target and other retailers
- Each has its own templates, attribute requirements, character limits and content-quality scoring. Ask the user for the current item setup spec or style guide.
- **Typical common rules:**
  - Titles follow a brand + product + key attributes formula with stated length guidance.
  - Key features / bullets are concise and benefit-led.
  - No promotional, pricing or shipping language.
  - No external links or contact details.
  - Required attributes per category.
- **Many retailers score content completeness** (attributes filled, number of images, rich media). Fill required and recommended attributes from real data. Never pad attributes to raise a score.

## Social commerce and AI shopping surfaces
- **Social storefronts and catalogs:** the opening sentence carries the benefit; then specs, sizing and care. Prices and descriptions must match the other channels.
- **AI shopping assistants and agentic-commerce feeds:** these reward complete, structured, unambiguous attributes and consistent facts across the brand site, feeds and retailers. Same principle: accurate, complete, machine-readable data.
  - If the user supplies a specific product-feed spec (for example an AI assistant's merchant feed), follow its required fields exactly.

## One master, many retailers
- **One master record is the source of truth.** A retailer variant never becomes the master. For each retailer, output a master-to-variant diff.
- **Map attributes to each retailer's names** (e.g., "Scent" vs. "Fragrance").
  - Retailer-required attributes missing from the master go to the gap report. Never guess them.
  - A wrong category or browse node means suppressed search and lost filters.
- **Effort:** hand-optimize hero SKUs and syndicate the long tail. If the user syndicates through a content platform (e.g., Salsify, Syndigo, 1WorldSync), deliver in its ingest format.
- **Retail events and programs** (e.g., Prime Day, loyalty offers) never go into listing copy.
- **Hero image:** brand, product type, variant and size must stay legible at search-thumbnail and mobile size.

## Grocery and quick commerce (e.g., Instacart, Kroger, delivery apps)
- **Titles:** short, as brand + type + variant + size.
- **Attributes:** ingredient and dietary attributes drive filters, so fill them, from data only.
- **Images:** pack shot on white.
- **Copy:** answer what shoppers check at the shelf: flavor, size, dietary fit.

## Cross-channel consistency checklist
- [ ] Same core facts (specs, materials, dimensions, compatibility) everywhere.
- [ ] Same approved claims, with the same qualifications.
- [ ] Titles adapted to each channel's format, while the product is clearly the same item.
- [ ] Prices and availability come from the commerce or feed systems, not hand-written copy.
- [ ] Images show the correct variant.
