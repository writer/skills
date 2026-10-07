# Commercial Math (CPG ↔ Retailer)

Show every formula with its inputs, and label each input as customer data, syndicated data, retailer data or an assumption.

## Promotions
- **Effective discount per unit:**

  | Mechanic | Effective discount |
  |---|---|
  | TPR of X% | X% |
  | BOGO | 50% |
  | Buy 2 get 1 free | 33% |
  | "2 for $Y" | 1 − (Y ÷ 2) ÷ regular price |

- **Breakeven lift** for the party funding the promotion:
  - L* = d ÷ (m − d)
  - d = discount as a % of regular price
  - m = that party's regular margin as a % of regular price
  - Example: m = 40% and d = 20% gives L* = 20 ÷ 20 = 100%. Volume must double just to break even.
  - If d ≥ m, every unit sells at a loss and no lift breaks even.
  - With a fixed event fee F: L* = (d + f) ÷ (m − d), where f = F ÷ (baseline units × regular price). Use the same price base for d and m; for the manufacturer, that is its own net price.
- **Promo profit impact.** Use one of two equivalent methods, never a mix of both:
  - **Method 1:** cost = total trade funding (per-unit discount × all promo units) + fixed event fees. Value incremental units at the **regular** margin.
  - **Method 2:** cost = fixed event fees + (regular margin − promo margin) × baseline units. Value incremental units at the **promo** margin.
  - **Check:** incremental contribution − cost = profit with the promo − profit without it.
  - **Subsidized baseline** = discount × baseline units, the funding spent on volume that would have sold anyway. Report it as a share of total funding.
- **True incremental units** = (actual − baseline) − cannibalization − pull-forward. Measure pull-forward once, either as the post-period dip against baseline (preferred) or as estimated pantry loading. Never both.
  - For the retailer, brand switching within the category isn't incremental.
- **ROI:**
  - Gross = incremental revenue ÷ spend. State whose revenue: for the manufacturer it's net revenue at net price, not retail sales.
  - Net = incremental contribution ÷ spend. A ratio below 1.0 means the event lost money. If you report (contribution − spend) ÷ spend instead, say so.
  - True = net, after cannibalization, the dip and execution cost.

## Pricing
- **Breakeven volume loss** for a price increase of p%, with contribution margin m%:
  - V* = p ÷ (m + p)
  - Example: p = 5% and m = 30% gives V* = 5 ÷ 35 = 14.3%. Volume can fall up to 14.3% before profit drops.
- **Elasticity (log-log):**
  - %ΔQ ≈ ε × %ΔP for small changes. For larger moves, use Q₁ = Q₀ × (P₁ / P₀)^ε.
  - Report a range, and stay within observed price points.
- **Retailer margin %** = (shelf price − cost to retailer) ÷ shelf price. Model it before proposing any list-price change.

## Gross-to-net (manufacturer)
- **Waterfall:**
  1. List price
  2. − off-invoice = net invoice
  3. − scan / performance allowances, bill-backs and other variable trade = net-net
  4. − fixed trade (slotting, lump sums) = net revenue, depending on the accounting policy
- **Trade rate** = (list − net-net) ÷ list, or total trade ÷ gross sales. State which definition you used.
- **Accounting:** under US GAAP (ASC 606), most consideration paid to customers, including most trade promotion, reduces revenue rather than appearing as an expense. Confirm the company's own policy.
- **Contribution margin layers:**
  - CM I = net revenue − variable COGS (and variable freight and logistics)
  - CM II = CM I − remaining variable trade
  - CM III = CM II − A&P
  - Name the layer you report.

## Shelf and distribution
- **Share of shelf** = brand facings or linear space ÷ category facings or space.
- **Share-to-space ratio** = share of category sales ÷ share of shelf. A ratio above 1 argues for more space.
- **Growth contribution index** = share of category growth ÷ share of category sales.
- **%ACV distribution**: the share of the market's all-commodity volume sold through stores that carry the item.
- **TDP (total distribution points)**: the sum of %ACV across items.
- **Velocity**: sales per point of distribution (sales ÷ TDP), or units per store per week per item.
- **Fair share index** = our share of the category (or segment) at this retailer ÷ our share of the same category in the total market, × 100. Below 100 means we under-index at this retailer.

## Supply scorecards
- **OTIF**: the share of orders that are both on time AND complete. Each retailer measures it at order level, by its own definitions and windows; use the current supplier guide.
- **Fill rate**: units shipped ÷ units ordered. State whether it is by case, line or order.
- **Deductions %** = total deductions ÷ net sales. Classify deductions by type and by validity.
