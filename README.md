# Superprof Tutor Scraper [💰$0.81]

Extract structured data from [superprof.co.uk](https://superprof.co.uk) — Search Superprof tutors by subject and city on 18 country sites. Every row gives the tutor name, hourly price, rating and profile link in one clean table. Schedule repeat runs to spot tutors that have joined since last time.

**[Superprof Tutor Scraper [💰$0.81] on Apify →](https://apify.com/blackfalcondata/superprof-co-uk-scraper?fpr=1h3gvi)**

---

## 🚀 How to use this actor

> ### 💚 $5 free Apify credits — every month
> No credit card required. No commitment. Cancel anytime.

### 👉 [Sign up free on Apify →](https://console.apify.com/sign-up?fpr=1h3gvi)

1. **Click sign up** — pick GitHub, Google, or email; takes ~30 seconds
2. **Open this actor** — input is pre-filled with a working example
3. **Click Start** — export results as JSON, CSV, or Excel

Your **$5 monthly platform credit** is enough to run this actor right away — and again every month — scraping typically several hundred to several thousand results per run, depending on your input.

## Key features

**Search with filters** — Search by keyword and location. Filter by 🌍 superprof country site, 📝 description format, ↕️ sort results by, and more.

**Incremental mode** — Only get new or changed records since your last run. Content hash per record — no duplicates, no re-processing.

**Change classification** — Track unchanged, expired, cross-run duplicate detection across runs. Build audit trails of how records evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Result cap** — Stop after N records (up to 1.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every record returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured records from superprof.co.uk on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor records, track trends, and analyze market dynamics with structured, deduplicated data from superprof.co.uk.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired ${NOUNS}. Perfect for price-tracking, churn analysis, and alerting pipelines.

**AI / LLM training data**
Structured JSON per record is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "maths",
  "location": "London",
  "country": "uk",
  "maxResults": 100,
  "compact": false,
  "excludeEmptyFields": false,
  "incrementalMode": false,
  "skipReposts": false,
  "notifyOnlyChanges": false,
  "notificationLimit": 5,
  "descriptionFormat": "all"
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Subject to search, e.g. "maths", "english", "guitar", "yoga". Use a JSON array for several subjects in one run (e.g. ["maths","physics"]). Leave the subject empty and give a city to list every tutor near that city. Required if no start URL, city or coordinates are provided. |
| `location` | string | — | City or address Superprof geocodes the search around, e.g. "London". Use a JSON array for several locations in one run. Leave the subject empty and give a city (or coordinates) to list every tutor there. Give a subject without a city to search the whole country site. A run needs at least a subject, a city, coordinates or a start URL. |
| `country` | enum | `"uk"` | Which Superprof country site to search (18 country sites). Prices and currency follow the site. |
| `maxResults` | integer | `100` | Maximum total tutors (0 = unlimited). |
| `maxPages` | integer | `30` | Maximum result pages to read per search (18 tutors per page). If both maxResults and maxPages are set, the lower cap wins. |
| `startUrls` | array | `[]` | Paste raw Superprof search URLs. Each URL becomes its own search task; results are merged and deduped by tutor ID across all URLs. When provided, startUrls REPLACE the subject/city fields (unsupported URLs are skipped, and if none is supported the run stops with an input error). |
| `compact` | boolean | `false` | Core fields only (for AI-agent/MCP workflows). |
| `excludeEmptyFields` | boolean | `false` | Drop null, empty-string, and empty-array fields from each record before push. Smaller payloads for AI agents and dashboards. |
| `incrementalMode` | boolean | `false` | Compare against previous run state. stateKey is optional — defaults to a value derived from search inputs (subjects, cities, startUrls, country site) so different filter sets never share state. |
| `stateKey` | string | — | Optional. Stable identifier for the tracked search universe. Leave empty to auto-generate from search inputs. |
| `emitUnchanged` | boolean | `false` | When incremental, also emit records that haven't changed. |
| `emitExpired` | boolean | `false` | When incremental, also emit records no longer found. |
| `skipReposts` | boolean | `false` | When incremental, skip tutors whose content matches a listing that expired in a prior run (cross-run duplicate detection). |
| `notifyOnlyChanges` | boolean | `false` | When Incremental Mode is on, only send notifications for NEW and UPDATED tutors. Has no effect outside incremental mode. |
| `notificationLimit` | integer | `5` | Maximum number of tutors included in each notification message (1–20). |
| `telegramToken` | string | — | Telegram bot token (from @BotFather). Required for Telegram notifications. |
| `telegramChatId` | string | — | Telegram chat or channel ID (e.g. "-100123456789"). Required when telegramToken is set. |
| `discordWebhookUrl` | string | — | Discord incoming webhook URL. Server Settings → Integrations → Webhooks → New Webhook. |
| `slackWebhookUrl` | string | — | Slack incoming webhook URL. api.slack.com/messaging/webhooks. |
| `whatsappPhoneNumberId` | string | — | Your WhatsApp Business phone-number ID (numeric, from Meta dashboard). Required when whatsappAccessToken is set. |
| `whatsappAccessToken` | string | — | WhatsApp Cloud API permanent access token (System User token from Meta Business). Recipient must have messaged the business number within the last 24h (service-conversation window — free since Nov 2024). |
| `whatsappTo` | string | — | Recipient phone in E.164 format without + (e.g. "436641234567"). Recipient must have messaged your business number within last 24h. |
| `webhookUrl` | string | — | Receives a JSON POST with {metadata, items} after each run. Universal escape hatch for n8n / Make / Zapier / custom backends. |
| `webhookHeaders` | object | — | Optional JSON object of custom headers (e.g. {"Authorization":"Bearer ..."}). |
| `appConnector` | string | — | Optional. Pick a connected app under Settings → API & Integrations to receive your results (including any contact details). Best-effort across MCP connectors as Apify expands its catalog. |
| `mcpIssueTeam` | string | — | Only when the connected app is an issue tracker: the team (name or ID) the summary issue is created under, if that app requires one. |
| `descriptionFormat` | enum | `"all"` | Choose which representation of the listing description to include. `all` keeps every variant; the others keep only the selected one. |
| `radiusKm` | integer | `0` | Only keep tutors whose listed distance from the searched place is at most this many kilometres. 0 = no limit. |
| `minPrice` | integer | — | Lowest hourly price to keep, in the site's own currency. Sent to Superprof's own price filter and re-checked on every result. Empty = no minimum. |
| `maxPrice` | integer | — | Highest hourly price to keep, in the site's own currency. Sent to Superprof's own price filter and re-checked on every result. Empty = no maximum. |
| `webcamOnly` | boolean | `false` | Search Superprof's online (webcam) lessons instead of lessons near a place, and keep only tutors who teach by webcam. |
| `orderBy` | enum | `"pertinence_DESC"` | Relevance and distance are applied by Superprof. Price and rating orders are applied by this actor over the tutors it reads for each search: every page up to Max pages is read first, sorted, then delivered. |
| `latitude` | string | — | Search around these coordinates instead of a city (give both latitude and longitude), e.g. "55.9533". When set, the coordinates decide the place, not the city field. |
| `longitude` | string | — | Longitude for a coordinate search, e.g. "-3.1883". Used only together with latitude. |
| `distance` | integer | `200` | How far around the coordinates Superprof searches, in kilometres. Used only with latitude and longitude. |

---

## Output fields

Every record returns the same 60-field schema. Missing values are `null` — never omitted.

- `listingId`
- `searchQuery`
- `contentQuality`
- `detailFetched`
- `scrapedAt`
- `source`
- `contentHash`
- `changeType`
- `id_annonce`
- `title`
- `url`
- `url_mer`
- `teacherName`
- `teacherCity`
- `teacherPhoto`
- `price`
- `price_ci`
- `rating_score`
- `rating_count`
- `rating_label`
- `type`
- `badge`
- `senior`
- `verified`
- `faceToFace`
- `webcam`
- `firstHourFree`
- `firstFreeDuration`
- `is_credit_impot`
- `is_feminin`
- `responseTime`
- `responseTimeDesc`
- `gallery`
- `tutorId`
- `name`
- `profileUrl`
- `portalUrl`
- `hourlyPrice`
- `price_html`
- `currency`
- `rating`
- `reviewCount`
- `ratingLabel`
- `city`
- `country`
- `countrySite`
- `distanceKm`
- `photo`
- `profilePhoto`
- `lessonType`
- `lessonInPerson`
- `lessonOnline`
- `freeFirstLesson`
- `taxCreditEligible`
- `responseTimeHours`
- `memberStatusId`
- `subject`
- `searchLocation`
- `searchUrl`
- `sourceDomain`

---

## Sample output

One object per record. Here is a real example from a production run:

```json
{
  "listingId": "19b80b5a688ab470375303a467fe4cf60480cf8feb27e72147a6bc8094673cb3",
  "searchQuery": "maths",
  "contentQuality": "full",
  "detailFetched": false,
  "scrapedAt": "2026-10-25T23:44:48.601Z",
  "source": "superprof.co.uk",
  "contentHash": "c0f8881358be6a09bb5fdbe7cb57c0116f4b96cbbb99add5cb9b3e60d6e162f8",
  "changeType": null,
  "id_annonce": "10990942",
  "title": "GCSE/IGCSE AND A LEVEL EXAMINER with UK Boards,11+, 13+ and 16+ ENTRANCES, 100%...",
  "url": "https://www.superprof.co.uk/gcse-igcse-and-level-examiner-with-boards-and-entrances-100-grade-excellent-results-20yrs-experience.html",
  "url_mer": "https://www.superprof.co.uk/connections-your-request-10990942.html"
}
```

*Truncated — full records contain 60 fields. See Output fields for the complete schema.*

**[Try Superprof Tutor Scraper [💰$0.81] now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/superprof-co-uk-scraper?fpr=1h3gvi)**

---

## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.0045 |
| Result | $0.00081 |

See the [actor on Apify](https://apify.com/blackfalcondata/superprof-co-uk-scraper?fpr=1h3gvi) for current pricing.

---

## FAQ

**How do I scrape superprof.co.uk?**
Use this actor on Apify to extract structured data from superprof.co.uk. Configure your search query and filters in the input, then click Start — no coding required.

**How do I get superprof.co.uk data as JSON, CSV, or Excel?**
The actor writes each record to Apify's dataset. Download as JSON, CSV, or Excel from the Console, stream via the API, or push to Make, Zapier, Airbyte, or Keboola.

**Is it legal to scrape superprof.co.uk?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check superprof.co.uk's terms of service for your specific use case.

**How much does it cost?**
Pay-per-event pricing — you only pay for ${NOUNS} extracted. Apify's free $5 credit is enough to run thousands of results before you pay anything.

**How does incremental mode work?**
Each record gets a content hash. On subsequent runs, only new or changed records are emitted — saving time, compute, and storage. Expired records can be tracked separately.

**Do I need an API key or credentials?**
No. Just sign up for Apify, paste your input, and click Start. No credit card required.

---

## Related products by Black Falcon Data

[Browse all Black Falcon Data actors →](https://apify.com/blackfalcondata?fpr=1h3gvi)

---

## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. Sign up — $5 platform credit included
2. Open [Superprof Tutor Scraper [💰$0.81]](https://apify.com/blackfalcondata/superprof-co-uk-scraper?fpr=1h3gvi) and configure your input
3. Click **Start** — export results as JSON, CSV, or Excel

Need more later? [See Apify pricing](https://apify.com/pricing?fpr=1h3gvi).

---

## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---

*Last updated: 2026 10*
