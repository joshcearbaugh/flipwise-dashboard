# FlipWise Dashboard

A live eBay + Vinted seller dashboard showing active listings, revenue, and daily sales.

## Structure

```
index.html          # Main dashboard (Cowork sidebar artifact)
data/
  dashboard_data.json  # Sales & listing data (update this to refresh the dashboard)
```

## Data

The dashboard reads its data from Google Drive (file ID stored in `index.html` as `DOC_ID`). To update the data:

1. Scrape new figures from eBay Seller Hub and Vinted API
2. Update `data/dashboard_data.json`
3. Re-encode and upload to Google Drive, or update the listing overrides in `index.html`

## Listing overrides

eBay and Vinted listing counts/values are hardcoded as overrides in `index.html` under `const LISTINGS = {...}` since the Drive file may have stale data. Update these when listing counts change.

## Key data sources

- **eBay revenue**: Scraped from eBay Seller Hub `/sh/performance/sales`
- **eBay listings**: Scraped from `/sh/lst/active`
- **Vinted revenue**: `GET /api/v2/my_orders` (requires browser login)
- **Vinted listings**: `GET /api/v2/catalog/items?search_text=&user_ids[]=3149671155`
  - ⚠️ Do NOT use `owner_id=` — it's broken and returns random items
