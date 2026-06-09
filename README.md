[Clutch Scraper](https://apify.com/jungle_synthesizer/clutch-scraper?fpr=data)

# Clutch.co Scraper — B2B Service Providers & Reviews

Scrape B2B service company profiles and client reviews from [Clutch.co](https://clutch.co). Pull ratings, hourly rates, project minimums, service lines, industry focus, contact info, and the top client review in a single pass.

---

## What It Does

Two-phase crawl against Clutch.co:

1. **Directory listing** — the crawler walks a category or service-line index (e.g. `web-developers`, `agencies/seo`) and collects every company card on the page.
2. **Company profile** — each card's profile page is opened, full firmographic and review data is extracted, and a flat record is emitted to the dataset.

Clutch sits behind a Cloudflare managed challenge. The scraper uses Playwright with residential proxies and fingerprint rotation to clear the challenge automatically — no CAPTCHA keys required.

---

## Input

| Field | Type | Description |
| --- | --- | --- |
| `mode` | string | `listings` (cards only, fast) or `both` (cards + full profile + top review). Default: `both`. |
| `serviceLine` | string | Service-line slug (e.g. `web-developers`, `agencies/seo`). Leave blank to hit the default directory. |
| `minRating` | number | Drop profiles under this Clutch rating (0-5). Default: `0`. |
| `searchUrls` | array | Specific Clutch.co directory, category, or `/profile/<slug>` URLs. Overrides `serviceLine` if set. |
| `maxItems` | integer | Cap on returned records. Default: `15`. `0` = unlimited. |
| `proxyConfiguration` | object | Proxy config. Defaults to Apify residential proxy in the US (required for Cloudflare bypass). |

### Sample input

```
{
  "mode": "both",
  "serviceLine": "web-developers",
  "minRating": 4.5,
  "maxItems": 100,
  "proxyConfiguration": {
    "useApifyProxy": true,
    "apifyProxyGroups": ["RESIDENTIAL"],
    "apifyProxyCountry": "US"
  }
}
```

Or with explicit URLs:

```
{
  "mode": "both",
  "searchUrls": [
    { "url": "https://clutch.co/profile/toptal" },
    { "url": "https://clutch.co/agencies/seo" }
  ],
  "maxItems": 50
}
```

---

## Output

One record per company. Listing fields come from the directory card; profile fields and the top review come from the `/profile/<slug>` page.

```
{
  "company_name": "Toptal",
  "company_url": "https://www.toptal.com",
  "clutch_url": "https://clutch.co/profile/toptal",
  "tagline": "Hire the Top 3% of Freelance Talent",
  "description": "Toptal is an exclusive network of the top freelance software developers, designers, finance experts...",
  "location": "New York, NY",
  "employee_count": "1,000 - 9,999",
  "founded_year": 2010,
  "hourly_rate": "$100 - $149 / hr",
  "min_project_size": "$25,000+",
  "clutch_rating": 4.8,
  "reviews_count": 425,
  "service_lines": ["Web Development", "Mobile App Development", "Custom Software Development"],
  "industry_focus": ["Financial Services", "Healthcare", "E-Commerce"],
  "client_focus": ["Midmarket", "Enterprise"],
  "phone": "+1 (888) 555-0123",
  "review_rating": 5.0,
  "review_title": "Reliable partner for rapid MVP delivery",
  "review_text": "Toptal delivered a working MVP in six weeks and has been embedded with our product team since.",
  "reviewer_name": "VP of Engineering",
  "reviewer_company": "Series B FinTech",
  "review_date": "2025-08-14"
}
```

Array fields (`service_lines`, `industry_focus`, `client_focus`) are plain arrays of strings. Every other field is a scalar or null.

---

## Pricing — Pay Per Result

- **$0.002 per company record** (+ a fixed start fee per run).
- No seats, no subscriptions. You only pay for records we actually deliver.
- 100 records ≈ $0.20. 1,000 records ≈ $2. 10,000 records ≈ $20.

If a run fails before any records are saved, you aren't charged for results.

---

## Typical Use Cases

- **B2B lead generation** — pull agencies ranked in your target service line, then route them into outreach with hourly rate and project-size context already attached.
- **Competitive intelligence** — see how your category ranks on Clutch, with review volume and reviewer testimonials.
- **Vendor shortlisting** — filter by `minRating` and service line, then pipe directly into a CRM.
- **Market sizing** — count the providers per service line and region, with employee and hourly-rate buckets as proxies for firm scale.

---

## Notes & Limits

- Clutch.co pagination varies by category. Listing mode walks up to a small number of follow-up pages; detail mode stops once `maxItems` profiles have been saved.
- `review_*` fields return the top review only. Full review lists are not in scope for this actor.
- Clutch is Cloudflare-protected. Use residential proxies. Datacenter IPs will be blocked before the first page loads.
- Run memory defaults to 2 GB. Lower it only if you're hitting a small URL list.

---

## Issues, feature requests, custom data

Open an issue on the actor's Apify page or email us through the console. Happy to add fields, tune selectors, or build a variant (reviews-only, JSON-LD-only, specific country) if your use case needs it.