# Awesome E-Commerce & Data APIs

A curated list of APIs for modern e-commerce, multi-store operations, growth analytics, and data workflows.

> **Focus:** cross-border e-commerce, multi-account operations, ads & analytics, pricing, logistics, data collection.  
> **Goal:** help operators pick the right APIs for real workflows, not just read docs.

---

## How to use this list

- Browse by **category** (E-commerce platforms, Ads & Analytics, Payments & FX, Logistics, Data & Intelligence).
- Each API entry highlights:
  - **Main use case** in real operations
  - **Auth / Access level**
  - Whether **proxy / region routing** is recommended
  - Notes on **limits, compliance, or typical pitfalls**

For each API, there will eventually be:
- A short entry in this README.
- (Optional) A longer guide article explaining typical workflows and routing patterns.

---

## Categories

- [E-commerce Platforms](#e-commerce-platforms)
- [Ads & Analytics](#ads--analytics)
- [Payments & FX](#payments--fx)
- [Logistics & Tracking](#logistics--tracking)
- [Data & Intelligence](#data--intelligence)

---

## E-commerce Platforms

APIs used to manage stores, listings, orders, inventory, and basic account operations.

| Name | Main Use Case | Auth | Docs | Proxy / Routing Notes |
| ---- | ------------- | ---- | ---- | ---------------------- |
| Amazon Selling Partner API (SP-API) | Manage multi-store Amazon operations: listings, orders, fees, reports | OAuth / AWS Sig | DOCS_URL | Keep IP region aligned with marketplace (e.g. IN, DE, US). Avoid noisy public pools during login flows. |
| Shopify Admin API | Store management, product & order sync, app integrations | API key / OAuth | DOCS_URL | Usually tolerant of global IPs for API calls; stricter for back-office logins. Keep operator logins and API calls separated. |
| WooCommerce REST API | Self-hosted store data: products, orders, customers | API key | DOCS_URL | Server-side use usually fine without proxies; scraping front-end still benefits from stable regional IPs. |
| Lazada Open Platform API | Cross-border listings and orders for Lazada markets | OAuth | DOCS_URL | For console logins and seller operations, stick to stable regional routes per country (ID, MY, PH, etc.). |
| Shopee Partner API | Shopee store data sync and order processing | Partner key / OAuth | DOCS_URL | Highly sensitive to abnormal access patterns; avoid mixing many stores through one unstable IP pool. |

---

## Ads & Analytics

APIs for ads management, pixel data, analytics, and attribution.

| Name | Main Use Case | Auth | Docs | Proxy / Routing Notes |
| ---- | ------------- | ---- | ---- | ---------------------- |
| Meta Marketing API | Campaign, ad set, and ad management across Facebook / Instagram | OAuth | DOCS_URL | Use region-consistent routes for business manager and ad account logins. Sudden IP jumps can trigger reviews. |
| Google Ads API | Search / Shopping / Display campaigns, reports, bidding | OAuth | DOCS_URL | Separate dev machines from production routes. Long-lived, stable IPs are safer than high-churn residential pools. |
| Google Analytics Data API | Pull GA4 reports and metrics | OAuth | DOCS_URL | Backend server-to-server usually fine; front-end scraping or unofficial workflows may need proxy isolation. |
| TikTok Marketing API | TikTok ads, audiences, and reporting | OAuth | DOCS_URL | Keep account logins, Business Center, and Pixel management on consistent regional routes (e.g. SEA vs EU). |

---

## Payments & FX

APIs related to payments, payout, and currency.

| Name | Main Use Case | Auth | Docs | Proxy / Routing Notes |
| ---- | ------------- | ---- | ---- | ---------------------- |
| Stripe API | Online payments, subscriptions, payouts | API key | DOCS_URL | Strong KYC and risk controls; keep dashboard logins from stable, verified device–IP pairs. |
| PayPal REST API | Payments and payouts | OAuth | DOCS_URL | High-risk for account flagging if IP / device jumps around; avoid testing from random public endpoints. |
| Wise API | Multi-currency accounts and FX | OAuth / API key | DOCS_URL | Treat as banking context: one operator, one region, long-term stable routing. |
| Open Exchange Rates API | FX rates for pricing and reporting | API key | DOCS_URL | Mostly read-only; proxies mainly useful for regional latency or rate-limit spreading. |

---

## Logistics & Tracking

APIs used for shipping, label creation, and parcel tracking.

| Name | Main Use Case | Auth | Docs | Proxy / Routing Notes |
| ---- | ------------- | ---- | ---- | ---------------------- |
| EasyPost API | Multi-carrier shipping, labels, tracking | API key | DOCS_URL | Backend usage usually fine without proxies; scraping carrier sites for extra data is where proxies help. |
| ShipStation API | Order import, shipping rules, labels | API key | DOCS_URL | Keep store connections and ShipStation console on stable, operator-bound routes. |
| AfterShip API | Unified tracking across carriers | API key | DOCS_URL | Often used as backend service; region routing is mostly for latency, not identity. |

---

## Data & Intelligence

APIs for search, SERP, product data, or general web intelligence.

| Name | Main Use Case | Auth | Docs | Proxy / Routing Notes |
| ---- | ------------- | ---- | ---- | ---------------------- |
| SERP API (e.g. search engine result APIs) | Programmatic search results for SEO & ads research | API key | DOCS_URL | Provider often handles IPs, but you may still route through your own proxies for extra control. |
| Product Data APIs | Product catalogs, reviews, and price intelligence | API key | DOCS_URL | High-volume workloads benefit from distributed, residential or ISP routes to avoid throttling. |
| News / Content APIs | News headlines and articles for monitoring or content feeds | API key | DOCS_URL | Mostly legal/terms-based limits; proxies help manage rate limiting and geo-restricted sources. |

---

## Roadmap

- [ ] Fill in `data/apis.json` as the single source of truth.
- [ ] Add official docs URLs and basic rate-limit notes.
- [ ] Publish deep-dive guides for key APIs (use cases + routing strategies).
- [ ] (Optional) Generate this README from `data/apis.json` via a small script.

---

## Contributing

This is an opinionated list. APIs are selected based on:

1. Clear value in real e-commerce / data workflows.
2. Reasonable documentation and stability.
3. Transparent terms and pricing.

Suggestions are welcome via issues or pull requests once the basic structure is stable.
