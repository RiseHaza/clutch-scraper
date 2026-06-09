[Clutch Scraper](https://apify.com/khadinakbar/clutch-scraper?fpr=data)

# 🔍 Clutch.co Scraper — Extract Agency Leads, Ratings & Pricing

**What does the Clutch.co Scraper do?** It extracts company profiles from Clutch.co — the world's largest B2B ratings and reviews platform — giving you verified agency leads with ratings, pricing, location, services, and contact information.

**Why use the Clutch.co Scraper?**

- Build targeted B2B prospect lists of IT agencies, software developers, and marketing firms
- Enrich your CRM with verified company data backed by real client reviews
- Monitor competitors or identify top-rated vendors in any service category

**What data can the Clutch.co Scraper extract?**

| Field | Type | Example |
| --- | --- | --- |
| company_name | string | "Saritasa" |
| profile_url | string | "[https://clutch.co/profile/saritasa](https://clutch.co/profile/saritasa)" |
| website | string | "[https://saritasa.com](https://saritasa.com)" |
| tagline | string | "Software Development & IT Services" |
| star_rating | number | 4.9 |
| review_count | integer | 142 |
| min_project_size | string | "$10,000+" |
| hourly_rate | string | "$25 - $49 / hr" |
| employees | string | "50 - 249" |
| location | string | "Newport Beach, CA" |
| services | array | ["Custom Software Dev", "Web Dev"] |
| is_verified | boolean | true |
| is_sponsored | boolean | false |
| scraped_at | ISO 8601 | "2026-04-13T12:00:00.000Z" |
| source_url | string | "[https://clutch.co/it-services?page=1](https://clutch.co/it-services?page=1)" |

---

## 🚀 How to Use the Clutch.co Scraper

### Step 1 — Pick your category

Go to [clutch.co](https://clutch.co) and browse to the service category you want. Copy the URL from your browser — for example:

- `https://clutch.co/it-services` — IT services companies
- `https://clutch.co/web-developers` — Web development agencies
- `https://clutch.co/agencies/digital-marketing` — Digital marketing agencies
- `https://clutch.co/app-developers` — Mobile app developers

### Step 2 — Paste the URL & run

Paste it into the **Clutch Category URL** field and set **Max Results** to control how many companies to scrape. Click **Run**.

### Step 3 — Export your leads

Download results as CSV, JSON, or XLSX — ready for your CRM, outreach tool, or spreadsheet.

### Example: Scrape top 100 UK web development agencies

```
{
    "categoryUrl": "https://clutch.co/uk/web-developers",
    "maxResults": 100
}
```

### Example: Scrape IT companies in New York

```
{
    "categoryUrl": "https://clutch.co/it-services",
    "location": "New York",
    "maxResults": 50
}
```

### Example: Run via API

```
curl -X POST "https://api.apify.com/v2/acts/USERNAME~clutch-scraper/runs?token=YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"categoryUrl": "https://clutch.co/web-developers", "maxResults": 200}'
```

---

## 💰 Pricing

This actor uses **Pay-Per-Event** pricing — you only pay for what you scrape.

| What | Price |
| --- | --- |
| Per company scraped | $0.05 |
| Free trial | First 10 companies free |

**Example:** 100 companies = $5.00. 1,000 companies = $50.00.

---

## 📊 Output Example

```
{
    "company_name": "Saritasa",
    "profile_url": "https://clutch.co/profile/saritasa",
    "website": "https://saritasa.com",
    "tagline": "We Build Software That Powers Growth",
    "star_rating": 4.9,
    "review_count": 142,
    "min_project_size": "$10,000+",
    "hourly_rate": "$50 - $99 / hr",
    "employees": "250 - 999",
    "location": "Newport Beach, CA",
    "services": ["Custom Software Development", "Web Development", "Mobile App Development"],
    "is_verified": true,
    "is_sponsored": false,
    "scraped_at": "2026-04-13T12:00:00.000Z",
    "source_url": "https://clutch.co/it-services"
}
```

---

## ⚙️ Input Parameters

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| categoryUrl | string | `https://clutch.co/it-services` | Clutch.co category or search URL |
| startUrls | array | `[]` | Alternative: list of Clutch URLs to scrape |
| location | string | `` | Filter by city/country (e.g., "London") |
| maxResults | integer | `50` | Max companies to scrape (1–5000) |
| maxConcurrency | integer | `2` | Browser tabs in parallel (keep low to avoid blocks) |

---

## 🔗 Integrate with Other Tools

Export scraped data, run the scraper via API, schedule and monitor runs, or integrate with other tools. Connect directly to:

- **Google Sheets** — real-time lead tracking
- **Zapier / Make** — automated CRM pushes
- **Airtable** — enriched agency database
- **HubSpot / Salesforce** — direct CRM import via API

---

## 🌐 Available Clutch Categories

Some popular category URLs you can use:

- `/it-services` — IT Services
- `/web-developers` — Web Developers
- `/app-developers` — App Developers
- `/agencies/digital-marketing` — Digital Marketing
- `/seo-firms` — SEO Companies
- `/agencies/social-media-marketing` — Social Media Marketing
- `/firms/artificial-intelligence` — AI Companies
- `/cloud-consulting` — Cloud Consulting
- `/cybersecurity` — Cybersecurity
- `/agencies/content-marketing` — Content Marketing
- `/agencies/pr` — PR Agencies
- `/agencies/advertising` — Advertising Agencies

---

## ❓ FAQ

**Does it require login?**
No. The Clutch.co Scraper works without any account or cookies.

**Will it trigger bot detection?**
The scraper uses Playwright with stealth settings and keeps concurrency low to minimize detection risk. We recommend running with `maxConcurrency: 2` (the default).

**Can I scrape individual company profiles?**
The current version scrapes listing pages. Company profile deep-scraping (portfolio, individual reviews, social links) is available in the Pro tier — contact us or check our other actors.

**How fresh is the data?**
Every run fetches live data directly from Clutch.co in real time.

**Can I schedule runs?**
Yes. Use Apify's built-in scheduler to refresh your lead database weekly or monthly.

---

## ⚖️ Legal Disclaimer

*This actor is intended for lawful data collection from publicly available sources. Users are responsible for compliance with applicable laws, Clutch.co's Terms of Service, and data protection regulations (GDPR, CCPA, etc.). Do not use this actor to collect personal data without a lawful basis. Apify and the actor developer are not liable for any misuse.*