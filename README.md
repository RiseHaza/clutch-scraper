[Clutch Scraper](https://apify.com/zadexinho/clutch-scraper?fpr=data)

## Clutch.co Scraper

Scrape company profiles, client reviews, and B2B lead data from Clutch.co — 280,000+ service providers.

**What you get:**

- Company profiles with 50+ fields: rating, hourly rate, min project size, employee count, year founded
- Service line percentages (e.g., Web Dev 60%, Mobile 30%)
- Technology stack with distribution (e.g., React 45%, Node.js 35%)
- Industry focus and client size breakdown (small / midmarket / enterprise)
- Client reviews with Q&A sections: background, challenge, solution, results
- Review rating breakdowns: quality, schedule, cost, willingness to refer
- Project details: type, budget range, timeline, location
- Contact data: website, social links (LinkedIn, Twitter, etc.), office locations

**How it works:**

- Pass category URLs, filtered search URLs, or direct profile URLs
- Quick scan mode (~15 fields) or full profile enrichment (50+ fields)
- Optional review extraction with project budgets and timelines
- Anti-detect browser for reliable Cloudflare bypass — 100% success rate

## What data can you extract?

### Company profiles

| Field | Type | Description |
| --- | --- | --- |
| `name` | string | Company name |
| `slug` | string | Clutch URL slug |
| `profileUrl` | string | Full Clutch profile URL |
| `website` | string | Company website |
| `logoUrl` | string | Company logo image URL |
| `tagline` | string | Short company description |
| `rating` | number | Overall rating (0-5) |
| `reviewCount` | integer | Total number of client reviews |
| `hourlyRate` | string | Hourly rate range (e.g., "$50 - $99 / hr") |
| `minProjectSize` | string | Minimum project budget (e.g., "$10,000+") |
| `employeeCount` | string | Employee count range (e.g., "50 - 249") |
| `yearFounded` | integer | Year the company was founded |
| `description` | string | Company overview text |
| `location.city` | string | Primary office city |
| `location.country` | string | Primary office country |
| `location.fullText` | string | Full location string |
| `additionalLocations` | array | Additional office locations |
| `serviceLines` | array | Service focus with percentages (e.g., Web Dev 60%, Mobile 30%) |
| `industryFocus` | array | Industry focus with percentages (e.g., IT 40%, Healthcare 25%) |
| `technologyStack` | array | Technologies/frameworks with percentages (e.g., React 45%) |
| `clientSizeDistribution` | object | Client size breakdown: small, midMarket, enterprise |
| `socialLinks` | object | LinkedIn, Facebook, Twitter, Instagram URLs |
| `isVerified` | boolean | Clutch verified badge |
| `clutchRanking` | string | Clutch ranking badge text |
| `scrapedAt` | string | Scrape timestamp (ISO 8601) |

### Client reviews (when enabled)

| Field | Type | Description |
| --- | --- | --- |
| `reviewId` | string | Unique review identifier |
| `companySlug` | string | Parent company slug |
| `companyName` | string | Parent company name |
| `rating` | number | Overall review rating (0-5) |
| `ratingBreakdown.quality` | number | Quality rating |
| `ratingBreakdown.schedule` | number | Schedule adherence rating |
| `ratingBreakdown.cost` | number | Cost rating |
| `ratingBreakdown.willingnessToRefer` | number | Willingness to refer rating |
| `title` | string | Review headline |
| `summary` | string | Short review summary |
| `fullText` | string | Full review text |
| `qaSections.background` | string | Project background/context |
| `qaSections.challenge` | string | Business challenge described |
| `qaSections.solution` | string | Solution provided |
| `qaSections.results` | string | Project results/outcomes |
| `reviewer.name` | string | Reviewer name |
| `reviewer.title` | string | Reviewer job title |
| `reviewer.company` | string | Reviewer company |
| `reviewer.companySize` | string | Reviewer company size |
| `reviewer.industry` | string | Reviewer industry |
| `project.type` | string | Project type/service |
| `project.budget` | string | Project budget range |
| `project.timeline` | string | Project duration |
| `project.location` | string | Project location |
| `isVerified` | boolean | Verified review badge |
| `date` | string | Review date |

## How to scrape Clutch.co

1. Enter one or more Clutch.co URLs in the **Start URLs** field:

- Category pages: `clutch.co/web-developers`
- Filtered search: `clutch.co/hr/staffing?client_budget=5000`
- Direct profiles: `clutch.co/profile/kumsal-agency`
2. Set **Max Results** to control how many companies to collect. Use `0` for unlimited.
3. Enable **Scrape Full Profiles** (default: on) for 50+ fields per company.
4. Enable **Extract Reviews** to collect client reviews with Q&A sections.
5. Click **Start** and download results from the **Dataset** tab as JSON, CSV, or Excel.

Disable **Scrape Full Profiles** for quick category scans — ~15 fields per company in a fraction of the time.

## How much does it cost?

Pay-per-event pricing — you are charged per company profile scraped. Reviews are free.

| Price per company | Price per 1,000 companies |
| --- | --- |
| $0.001 | $1.00 |

**Example:** Scraping 100 companies with full profiles costs approximately **$0.10**.

Client reviews with Q&A sections are included at no extra charge.

## Use cases

- **B2B lead generation** — Build agency lists by category with contacts, websites, and service offerings
- **Vendor landscape mapping** — Compare ratings, pricing, and service focus across categories
- **Competitive analysis** — Track how agencies rank, what services they emphasize, which technologies they use
- **Procurement intelligence** — Extract client reviews with project budgets, timelines, and outcomes
- **CRM enrichment** — Merge Clutch profiles with existing contact databases
- **Pricing benchmarks** — Analyze hourly rates and min project sizes across categories and locations
- **Technology tracking** — See which frameworks agencies use, with exact percentage breakdowns

## Input

| Field | Type | Default | Description |
| --- | --- | --- | --- |
| `startUrls` | string[] | — | Clutch.co URLs: category pages, search results, or profile pages (required) |
| `maxResults` | integer | `100` | Maximum companies to collect (0 = unlimited) |
| `scrapeProfiles` | boolean | `true` | Enrich listing data with full profile (50+ fields) |
| `getReviews` | boolean | `false` | Extract client reviews with Q&A sections |
| `maxReviewsPerCompany` | integer | `50` | Max reviews per company (1-5000) |
| `startPage` | integer | `1` | Listing page to start from |
| `requestDelay` | integer | `500` | Delay between requests in ms (100-10000) |
| `proxy` | object | residential | Proxy configuration (residential recommended) |

### Input examples

**Category listing (quick scan):**

```
{
    "startUrls": ["https://clutch.co/web-developers"],
    "maxResults": 50,
    "scrapeProfiles": false
}
```

**Category with full profiles:**

```
{
    "startUrls": ["https://clutch.co/agencies/digital-marketing"],
    "maxResults": 20,
    "scrapeProfiles": true
}
```

**Direct profile URL with reviews:**

```
{
    "startUrls": ["https://clutch.co/profile/kumsal-agency"],
    "scrapeProfiles": true,
    "getReviews": true,
    "maxReviewsPerCompany": 10
}
```

**Filtered search with budget:**

```
{
    "startUrls": ["https://clutch.co/hr/staffing?client_budget=5000&hourly_rate=300"],
    "maxResults": 100,
    "scrapeProfiles": true
}
```

**Multiple URLs in one run:**

```
{
    "startUrls": [
        "https://clutch.co/web-developers",
        "https://clutch.co/profile/kumsal-agency",
        "https://clutch.co/it-services/analytics/new-york-state"
    ],
    "maxResults": 30,
    "scrapeProfiles": true,
    "getReviews": true
}
```

## Output example

### Company record

```
{
    "type": "company",
    "name": "Kumsal Agency",
    "slug": "kumsal-agency",
    "profileUrl": "https://clutch.co/profile/kumsal-agency",
    "website": "https://kumsal.co",
    "tagline": "We Build Digital Products",
    "rating": 4.9,
    "reviewCount": 89,
    "hourlyRate": "$50 - $99 / hr",
    "minProjectSize": "$10,000+",
    "employeeCount": "50 - 249",
    "yearFounded": 2015,
    "description": "Kumsal Agency is a full-service digital agency...",
    "location": {
        "city": "Istanbul",
        "country": "Turkey",
        "fullText": "Istanbul, Turkey"
    },
    "serviceLines": [
        {"name": "Web Development", "percentage": 60.0},
        {"name": "Mobile App Development", "percentage": 30.0},
        {"name": "UX/UI Design", "percentage": 10.0}
    ],
    "industryFocus": [
        {"name": "Information Technology", "percentage": 40.0},
        {"name": "Business Services", "percentage": 25.0}
    ],
    "technologyStack": [
        {"name": "React", "percentage": 45.0},
        {"name": "Node.js", "percentage": 35.0}
    ],
    "clientSizeDistribution": {
        "small": "30%",
        "midMarket": "50%",
        "enterprise": "20%"
    },
    "socialLinks": {
        "linkedin": "https://linkedin.com/company/kumsal-agency"
    },
    "isVerified": true,
    "scrapedAt": "2026-02-18T10:30:00+00:00"
}
```

### Review record

```
{
    "type": "review",
    "reviewId": "review-a1b2c3d4e5f6",
    "companySlug": "kumsal-agency",
    "companyName": "Kumsal Agency",
    "rating": 5.0,
    "ratingBreakdown": {
        "quality": 5.0,
        "schedule": 5.0,
        "cost": 4.5,
        "willingnessToRefer": 5.0
    },
    "title": "Exceptional Web Development Partner",
    "summary": "They delivered a complex e-commerce platform on time and within budget...",
    "qaSections": {
        "background": "We needed to modernize our legacy e-commerce platform.",
        "challenge": "Migrating 50,000+ products while maintaining SEO rankings.",
        "solution": "Phased migration with React frontend and Node.js backend.",
        "results": "40% increase in conversion rate, 60% faster page loads."
    },
    "reviewer": {
        "name": "Jane Smith",
        "title": "CTO",
        "company": "GlobalRetail Inc.",
        "companySize": "1,000 - 9,999",
        "industry": "Retail"
    },
    "project": {
        "type": "Web Development",
        "budget": "$200,000 to $999,999",
        "timeline": "6-12 months",
        "location": "Remote"
    },
    "isVerified": true,
    "date": "2025-11-15"
}
```

## Tips

- Clutch.co requires **residential proxies** — the default config uses Apify's RESIDENTIAL group. Do not disable this.
- Use **listing mode** (`scrapeProfiles: false`) for quick scans — name, rating, location, hourly rate.
- Use **profile mode** for the richest data — service percentages, tech stacks, industry focus from embedded chart data.
- Mix listing URLs and profile URLs in a single run — the scraper classifies each URL automatically.
- The scraper deduplicates by slug. Same company in multiple categories = one record.
- Use the `type` field to filter output — `"company"` vs `"review"`.
- Increase `requestDelay` to `1000`+ for large runs.

## FAQ

### How many companies can I scrape?

No hard limit. Set `maxResults` to `0` for all companies in a category. Paginates automatically.

### Do I need residential proxies?

Yes. Clutch.co uses Cloudflare protection. The default RESIDENTIAL proxy group is included in all Apify plans.

### What makes this scraper different?

Three-tier extraction (JSON-LD + JavaScript chart data + DOM selectors) captures service line, tech stack, and industry focus percentages that other scrapers miss. Reviews include full Q&A sections with project budgets and timelines.

### What if a company profile returns 404?

The scraper logs a warning and moves on. A final summary shows how many succeeded and failed.

### Can I scrape reviews?

Yes. Enable `getReviews`. Reviews include Q&A sections (Background, Challenge, Solution, Results), rating breakdowns, project details, and reviewer info.

### What is listing mode vs profile mode?

**Listing mode** (`scrapeProfiles: false`): ~15 fields per company from category pages. Fast, one request per page.
**Profile mode**: visits each company page to extract 50+ fields including service breakdowns, tech stacks, and industry focus.

## Changelog

- **v0.4** — Pay-per-event pricing (companies only, reviews free). Spending limit support. README rewrite.
- **v0.3** — Three-tier extraction verified at 100% success. Competitor benchmarks.
- **v0.2** — Camoufox anti-detect browser. Three-tier profile extraction (JSON-LD, chart data, DOM). Review extraction rewrite.
- **v0.1** — Initial release. Listing extraction, profile enrichment, review Q&A sections, circuit breaker.