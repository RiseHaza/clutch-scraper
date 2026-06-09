[Clutch Scraper](https://apify.com/pro100chok/clutch-scraper?fpr=data)

# Clutch.co Scraper — Companies, Reviews, Emails & Phones

Extract **company profiles, customer reviews, email addresses, and phone numbers** from [Clutch.co](https://clutch.co) — the leading B2B ratings and reviews platform with 300,000+ companies.

Build lead lists, competitive intelligence reports, and market research datasets with a single click.

## Two pricing options

This Actor is available in two versions — choose the one that fits your usage:

| Version | Price | Best for | Link |
| --- | --- | --- | --- |
| **Pay per result** | $2 per 1,000 results | One-time scrapes, small datasets, testing | [Clutch Scraper](https://apify.com/pro100chok/clutch-scraper) |
| **Monthly subscription** | $20/month (unlimited results) | Regular scraping, large datasets, ongoing projects | [Clutch Scraper Monthly](https://apify.com/pro100chok/clutch-scraper-monthly) |

Both versions have the same features and output format — the only difference is how you pay.

## Why this scraper?

| Feature | This Actor | Other scrapers |
| --- | --- | --- |
| Full company profiles | 40+ fields | 10-15 fields |
| Customer reviews with Q&A | Background, Challenge, Solution, Results | Title + rating only |
| Sub-ratings | Quality, Schedule, Cost, Willing to Refer | Overall rating only |
| Email extraction from websites | Scans homepage + /contact + /about | Not available |
| Phone extraction from websites | tel: links, Schema.org, context-based | Not available |
| All Clutch filters built-in | Location, budget, hourly rate, size, industry, verified | URL-only filtering |
| Quality scoring | Computed 0-100 score per company | Not available |
| Search by keywords | Live search API integration | Most require URLs |
| Social media links | LinkedIn, Twitter, Facebook, Instagram | Partial or none |
| Verification data | Premier Verified status, entity info | Basic badge only |
| No headless browser needed | Pure HTTP + HTML parsing (fast & cheap) | Many use Playwright |

## What data do you get?

### Company Profile (40+ fields)

- **Basic:** name, Clutch URL, website, logo, description, tagline
- **Metrics:** rating (0-5), review count, quality score (0-100)
- **Business:** hourly rate, min project size, employees, year founded
- **Location:** multiple office addresses with city, country, phone
- **Services:** full list with percentage breakdown
- **Social media:** LinkedIn, Twitter, Facebook, Instagram URLs
- **Verification:** Premier Verified / Verified status, legal entity data
- **Portfolio:** project images, descriptions, links
- **Contact enrichment:** emails and phone numbers from company website

### Customer Review (20+ fields)

- **Ratings:** overall + Quality, Schedule, Cost, Willing to Refer
- **Content:** title, quote, full feedback text
- **Q&A sections:** Background, Challenge, Solution, Results
- **Reviewer:** name, position, industry, location, company size
- **Project:** services provided, budget range, duration
- **Meta:** date, verified badge, featured badge

## How to use

### 1. Scrape a category (most common)

Get all software development companies:

```
{
    "mode": "catalog",
    "startUrls": [{ "url": "https://clutch.co/developers" }],
    "scrapeProfiles": true,
    "scrapeReviews": true,
    "maxReviewsPerCompany": 10,
    "maxItems": 100
}
```

### 2. Scrape specific companies

Get full profiles for known companies:

```
{
    "mode": "profile",
    "startUrls": [
        { "url": "https://clutch.co/profile/simform" },
        { "url": "https://clutch.co/profile/goji-labs" }
    ],
    "scrapeReviews": true,
    "extractContacts": true
}
```

### 3. Search by keywords

Find companies by keyword:

```
{
    "mode": "search",
    "keywords": ["mobile app development", "AI consulting"],
    "maxItems": 50,
    "scrapeProfiles": true
}
```

### 4. Use filters (location, budget, size)

Get verified US companies with $50K+ budgets:

```
{
    "mode": "catalog",
    "startUrls": [{ "url": "https://clutch.co/developers" }],
    "filterLocation": "United States",
    "filterBudget": "50000",
    "filterVerifiedOnly": true,
    "sortBy": "ClutchRank",
    "scrapeProfiles": true,
    "maxItems": 200
}
```

### 5. Extract emails and phones

Enrich company data with contact information from their websites:

```
{
    "mode": "catalog",
    "startUrls": [{ "url": "https://clutch.co/web-developers" }],
    "scrapeProfiles": true,
    "extractContacts": true,
    "maxItems": 50
}
```

## Example output

```
{
    "id": 17572,
    "name": "Simform",
    "slug": "simform",
    "url": "https://clutch.co/profile/simform",
    "website_url": "https://www.simform.com",
    "logo_url": "https://img.shgstatic.com/...",
    "rating": 4.8,
    "review_count": 83,
    "verification_status": "Premier Verified",
    "min_project_size": "$25,000+",
    "hourly_rate": "$25 - $49",
    "employees": "1,000 - 9,999",
    "founded": 2010,
    "description": "Simform is a leading software development company...",
    "tagline": "Your Trusted Digital Engineering Partner",
    "addresses": [
        {
            "city": "Orlando",
            "region": "FL",
            "country": "United States",
            "country_code": "US",
            "phone": "+1 (321) 237-2727"
        }
    ],
    "services": [
        { "name": "AI Development", "percentage": null },
        { "name": "Custom Software Development", "percentage": null },
        { "name": "Mobile App Development", "percentage": null },
        { "name": "Cloud Consulting & SI", "percentage": null }
    ],
    "social_media": {
        "linkedin": "https://www.linkedin.com/company/simform/",
        "twitter": "https://twitter.com/simform",
        "facebook": "https://www.facebook.com/simform",
        "instagram": "https://www.instagram.com/_simform/"
    },
    "emails": ["info@simform.com"],
    "phones": ["+13212372727"],
    "quality_score": 88.8,
    "is_sponsor": true,
    "reviews": [
        {
            "id": 442581,
            "title": "Custom Software Dev for Scientific Research Company",
            "date": "Nov 7, 2022",
            "overall_rating": 5.0,
            "quality_rating": 4.5,
            "schedule_rating": 4.5,
            "cost_rating": 5.0,
            "willing_to_refer": 4.5,
            "quote": "We really appreciate the level of expertise...",
            "reviewer": {
                "name": null,
                "position": "CTO, Estima Scientific",
                "industry": "IT Services",
                "company_size": "1-10 Employees"
            },
            "qa": {
                "background": "I am the CTO of Estima Scientific...",
                "challenge": "We are performing extensive R&D...",
                "solution": null,
                "results": "The team has been able to develop new mobile software..."
            },
            "is_verified": false,
            "is_featured": false
        }
    ],
    "scraped_at": "2026-03-15T02:21:02.612000"
}
```

## Supported Clutch.co categories

Works with **any** Clutch.co category URL, including:

- `/developers` — Software Development Companies
- `/web-developers` — Web Development Companies
- `/it-services` — IT Services Companies
- `/agencies/digital-marketing` — Digital Marketing Agencies
- `/agencies/seo` — SEO Companies
- `/agencies/ppc` — PPC Agencies
- `/web-designers` — Web Design Companies
- `/app-developers` — Mobile App Developers
- `/agencies/social-media-marketing` — Social Media Marketing
- `/agencies/content-marketing` — Content Marketing
- Any other category on clutch.co

## Input parameters

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `mode` | string | `catalog` | `catalog`, `profile`, `search`, or `url` (auto-detect) |
| `startUrls` | array | — | Clutch.co category or profile URLs |
| `keywords` | array | — | Search keywords (for `search` mode) |
| `maxPages` | integer | `0` | Max catalog pages (0 = all, ~50 companies per page) |
| `maxItems` | integer | `0` | Max companies to scrape (0 = unlimited) |
| `scrapeProfiles` | boolean | `true` | Visit each company page for full data |
| `scrapeReviews` | boolean | `false` | Extract customer reviews |
| `maxReviewsPerCompany` | integer | `10` | Max reviews per company (0 = all) |
| `extractContacts` | boolean | `false` | Extract emails & phones from company websites |
| `filterLocation` | string | — | Filter by location (e.g. `United States`) |
| `filterBudget` | string | — | Min budget: `5000`, `10000`, `25000`, `50000`, `100000` |
| `filterHourlyRate` | string | — | Hourly rate: `25`, `50`, `100`, `150`, `200`, `300` |
| `filterEmployees` | string | — | Company size: `10 - 49`, `50 - 249`, `250 - 999` |
| `filterVerifiedOnly` | boolean | `false` | Only verified companies |
| `sortBy` | string | `relevance_desc` | Sort: `ClutchRank`, `NumberOfReviews`, `ReviewRating` |
| `proxyConfiguration` | object | — | Apify Proxy settings (residential recommended) |
| `concurrency` | integer | `3` | Parallel requests (1-5) |
| `requestDelay` | number | `1.5` | Delay between requests in seconds |

## Tips for best results

- **Use residential proxies** for large runs (1000+ companies). Datacenter proxies may get blocked by Cloudflare.
- **Start small** — test with `maxItems: 10` before running large scrapes.
- **Enable `scrapeProfiles`** for full data. Without it, you only get basic catalog fields (name, rating, location).
- **Set `requestDelay: 2.0`** or higher to avoid rate limiting (Clutch allows ~50 requests per minute).
- **Use filters** to narrow results instead of scraping entire categories — faster and cheaper.

## Integrations

Connect Clutch.co data to your tools:

- **Google Sheets** — auto-export companies to spreadsheets
- **Zapier / Make** — trigger workflows when new data is scraped
- **Slack** — get notifications when scraping completes
- **CRM (HubSpot, Salesforce)** — import leads directly
- **API** — access results programmatically via [Apify API](https://docs.apify.com/api)

## Cost estimation

This Actor uses **no browser** — only fast HTTP requests. Approximate costs on Apify platform:

| Scenario | Companies | Time | Apify cost |
| --- | --- | --- | --- |
| Catalog only (no profiles) | 500 | ~2 min | ~$0.01 |
| With full profiles | 500 | ~30 min | ~$0.10 |
| With profiles + reviews | 500 | ~60 min | ~$0.20 |
| With profiles + reviews + contacts | 500 | ~90 min | ~$0.30 |

*Costs depend on proxy type and platform plan. Residential proxies add proxy traffic costs.*

## Having issues? Help me fix them faster

If you experience any problems, please share your run data with me so I can debug and improve the Actor:

1. Go to [Apify Security Settings](https://console.apify.com/settings/security)
2. Find **"Share run data with developers"**
3. In the **"Manage list of Actors"** section, check this Actor (or **All Actors**)
4. Save

This data is used **only for debugging** and helps me resolve issues much faster. Thank you!

## Support

Having issues or need a custom feature?

- Email: **[afrcanec@gmail.com](mailto:afrcanec@gmail.com)**
- Open an issue on this Actor's page
- Response time: typically within 24 hours

## 🏷️ Tags

Clutch.co Scraper, Clutch Scraper, B2B Lead Generation, Company Reviews Scraper, IT Services Database, Software Development Companies, Clutch.co Data Extractor, Business Profile Scraper, Client Reviews Extractor, Company Ratings Scraper, B2B Data Mining, Digital Agency Finder, Clutch.co API, Email Extractor B2B, Phone Number Extractor, Competitive Intelligence, Market Research B2B, Company Directory Scraper, How to Scrape Clutch.co, Extract Company Data, B2B Sales Intelligence, Agency Reviews Scraper, Service Provider Database, Lead Lists Builder, Company Contact Information, Social Media Links Extractor, Verified Companies Data, Web Development Companies, Quality Score Calculator, B2B Outreach Data