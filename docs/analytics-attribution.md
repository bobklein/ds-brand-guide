# Analytics & Attribution — Implementation Details

> **Companion to `web-implementation.md §17`.** That section explains *what* the system promises (closed-loop attribution from paid click to lead) and *who* the players are. This file explains *how* it's wired — field keys, conversion IDs, cron schedules, script paths, failure modes.
>
> **Download:** [raw markdown](https://raw.githubusercontent.com/bobklein/ds-brand-guide/main/docs/analytics-attribution.md)

---

## 1. Pipedrive Lead Custom Fields (the 8 attribution fields)

Every Pipedrive Lead created by the Formspree webhook carries 8 custom fields that store the attribution payload. The field keys are 40-character hex strings, fixed at creation time, and hardcoded into `formspree-webhook.mjs` in the website repo.

| Field name | Lead field key | Stores | Sample value |
|---|---|---|---|
| UTM Source | `2d987c86f8c2ba6d4a2ba671202fb101963cb7ae` | Platform | `google` |
| UTM Medium | `5bc2cf59b8f65bac7fee4f0049decda09e64eefb` | Channel type | `cpc` |
| UTM Campaign | `f6983c094a3678e33fa339a912595b1d8c1a0ed3` | Campaign name | `AI_BUILD_PARTNER` |
| UTM Content | `de10675163c2f6d75a0699052c21d3a36e71091e` | Specific creative / ad ID | `199449858129` |
| UTM Term | `d1d21e1d19f61f635c583d6adf873673f9e9ece6` | Keyword (paid search) | `ai+development+services` |
| GCLID | `14de079f53a25515915fc0adb05f642607a6b1a7` | Google Click ID | `Cj0KCQiA...` |
| Referrer | `ffd711d13883b5aedefd9a2e4981919390343776` | `document.referrer` | `https://www.google.com/` |
| Landing Page | `e4fc9205150ff331e8df34dd1ec6c5e0a29da086` | Hardcoded per-LP | `/lp/ai-build-partner/` |
| Source Page | `1fe5fef0101f8b10a757d9944b072e0c098da15a` | Current page on submit | `/lp/ai-build-partner/` |

**Adding a new field:** Pipedrive's API does not expose Lead-field creation. Create the field in the Pipedrive UI (Settings → Custom Fields → Leads), copy the new key from the URL, and add a constant to `formspree-webhook.mjs`.

**History:** These 9 custom fields were added 2026-05-13. Before that, the webhook conditionally created Pipedrive Deals (which always supported custom fields) versus Leads (which did not at the time). Now all submissions create Leads; Deals are only used by the Pipedrive Scheduler flow.

---

## 2. Formspree → Webhook → Pipedrive

### Formspree endpoint

Every form on the site submits to a single Formspree endpoint:

```
https://formspree.io/f/xvzbywbr
```

Formspree receives the submission and fires a server-side webhook to the Netlify Function below.

### Webhook function

**File:** `netlify/functions/formspree-webhook.mjs` in the digitalscientists.com repo.

**Triggered by:** Formspree on every form submission.

**Process:**
1. Parse the Formspree payload.
2. Look up or create a Pipedrive Person (deduplicated by email).
3. Look up or create a Pipedrive Organization (if `company` field is present).
4. Create a Pipedrive **Lead** with:
   - Title = `_subject` hidden field value
   - Person + Organization references
   - 8 custom fields populated from the hidden UTM/gclid/referrer fields
   - A note containing the full form submission text
5. Return 200 to Formspree.

The webhook always creates a Lead (never a Deal) regardless of whether UTMs are present. Organic-traffic leads simply have empty attribution fields.

---

## 3. Google Analytics 4

GA4 is loaded via `gtag.js` from `ds-includes-v2.js`.

### Events

| Event | When | Implementation note |
|---|---|---|
| `page_view` | Every page load | Default gtag behavior |
| `form_submit` | Form submission on the source page | Synchronous gtag call |
| `generate_lead` | Form submission on the source page | Fired via `navigator.sendBeacon` for delivery reliability |

**Why both events fire on the source page** (not on `/thank-you/`):

In April 2026, GA4 measurement showed a ~38% leak — `generate_lead` was fired on the `/thank-you/` redirect destination, but a significant fraction of users closed the tab before the redirect completed, never firing the event. The fix: fire both events on the source page on form submit, using `sendBeacon` for `generate_lead` so the event survives even if the user navigates away mid-request.

### Property + service account

- GA4 Property: `ds-analytics-303617` (BigQuery export enabled)
- Service account: `claude-analytics@ds-analytics-303617.iam.gserviceaccount.com` (Owner access for programmatic queries)
- gtag.js measurement ID: configured in `ds-includes-v2.js`

---

## 4. PostHog

### Keys

- **Project Key (public, safe to expose):** `phc_pYXg2QfxEt3GYAdBZdCEefpqUw85tbwLyR6D72uFpLpN` — hardcoded in `ds-includes-v2.js`
- **Personal API Key (server-only, secret):** stored in `analytics/tools/.env` as `POSTHOG_PERSONAL_API_KEY`. Never commit to client code, never paste in chat. (A `phx_` key grants full account access.)
- **Project ID:** `434546`

### Reverse proxy

Ad blockers detect and block direct calls to `posthog.com` and `*.posthog.com`. To survive this, PostHog is reverse-proxied through `digitalscientists.com` via Netlify redirects:

```toml
# netlify.toml
[[redirects]]
  from = "/ingest/static/*"
  to   = "https://us-assets.i.posthog.com/static/:splat"
  status = 200
  force  = true

[[redirects]]
  from = "/ingest/*"
  to   = "https://us.i.posthog.com/:splat"
  status = 200
  force  = true
```

PostHog is initialized in `ds-includes-v2.js` with `api_host: "https://digitalscientists.com/ingest"`. Browser network requests look first-party (digitalscientists.com) and aren't blocked by typical ad blockers.

### Server-side queries

For programmatic dashboards and analysis, use the Personal API Key + Project ID with the PostHog Python SDK. HogQL is the preferred query language.

---

## 5. StatCounter

Independent backup analytics. Loaded site-wide.

**Do not remove.** Role is to serve as a second source-of-truth when GA4 silently breaks (gtag.js loading failures, browser-side blocking, measurement-protocol changes). If StatCounter and GA4 disagree, investigate GA4 first.

---

## 6. Google Ads ↔ Pipedrive Closed Loop

This is what makes paid attribution closed-loop. Without it, Google Ads only sees clicks, not the leads they generated.

### Google Ads account

- Customer ID: `1651404286` (Digital Scientists)
- **Two conversion actions fire from the offline upload cron (post 2026-05-22):**
  - `Pipedrive Lead Created` — fires on every Lead with GCLID. Low signal ($50 default value). Gives Smart Bidding daily training data even when MQL volume is small.
  - `Pipedrive MQL` — fires only when a Lead has been converted to a Deal in Pipeline 1 (Inbound Project). High signal. Real optimization target.
- The cron script looks up conversion actions by NAME at runtime, not by hardcoded ID, so action IDs are not coupled to the script.
- 5 active Search campaigns (as of 2026-05-22):
  - AI Build Partner (camp ID 23854408286)
  - Healthcare AI Build (23849081403)
  - Mobile App Development (23873299372)
  - UX Design (23863598577)
  - Custom Software Development (23873300074)
- **Geo-targeting:** `positive_geo_target_type = PRESENCE` on all 5 campaigns (set 2026-05-21). Google's default is `PRESENCE_OR_INTEREST`, which served ads to anyone with English-language interest in US topics, including overseas. Always set `PRESENCE` explicitly on new campaigns.
- **Day-parting:** -30% bid modifier 12am-6am ET, default 6am-12am, all 5 campaigns. Set 2026-05-21.

### The 9am ET cron — closes the loop

- **Script:** `scratchpad/pd_leads_to_ads_offline_conv.py`
- **Wrapper:** `scratchpad/run_pd_to_ads_conv.sh`
- **Schedule:** `0 9 * * *` (9am ET daily)
- **What it does** (two passes, two conversion events):

  **Pass 1 — "Pipedrive Lead Created" (low-signal early data):**
  1. Queries Pipedrive `/leads` for any Lead created in the last 7 days with the GCLID custom field populated.
  2. For each, uploads a `ClickConversion` with $50 value to the "Pipedrive Lead Created" conversion action.

  **Pass 2 — "Pipedrive MQL" (high-signal qualification event):**
  1. Queries Pipedrive `/deals` for any Deal in **Pipeline 1 ("Inbound Project")** created in the last 7 days with GCLID populated.
  2. For each, uploads a `ClickConversion` with the Deal value (or $500 default if value not yet set) to the "Pipedrive MQL" conversion action.

- **Why two passes:** A Pipedrive Lead is raw inbound — not yet qualified. A Deal in Pipeline 1 is the result of Sales confirming service interest in a conversation. The two events represent funnel stages of meaningfully different value. Smart Bidding learns better with both signals than with either alone.
- **Lead → Deal conversion preserves all 9 attribution custom fields** — Pipedrive auto-maps by field key. No data is lost when Sales qualifies a Lead by converting to a Deal.
- **Idempotency:** Google Ads dedupes by gclid + conversion_action + conversion_date_time. Re-running the cron does not inflate counts.

### Manual CPC → Smart Bidding transition

All 5 campaigns currently use Manual CPC. Smart Bidding (Target CPA or Maximize Conversions) requires 15-30 conversions in the trailing 30 days. Transition is planned once the offline conversion uploads accumulate enough signal.

---

## 7. Daily Morning Brief

A unified daily report combining Google Ads spend + PostHog sessions + Pipedrive leads + Google search-term alerts.

### Where it runs

- **Script:** `scratchpad/daily_morning_brief.py`
- **Wrapper:** `scratchpad/run_daily_morning_brief.sh`
- **Schedule:** `30 7 * * *` (7:30am ET daily)
- **Output file:** `scratchpad/daily-briefs/morning-brief-YYYY-MM-DD.txt`

### Contents

1. PPC performance per campaign: impressions, clicks, CTR, CPC, spend, conversions
2. PostHog: total site sessions, paid-LP session breakdown, form submits per LP
3. New Pipedrive Leads with UTM campaign + GCLID
4. Search-term alerts: any term with $5+ spend and 0 conversions in the prior day

### Known issue

macOS cron only fires when the machine is awake. If the laptop is asleep at 7:30am, the brief silently skips. Migration to `launchd` (which can wake the Mac) is planned but not implemented. Manual run: `bash scratchpad/run_daily_morning_brief.sh`.

Email delivery via the macOS `mail` command requires postfix configured, which usually isn't. The brief currently lives only as a file on disk; email delivery is a known follow-up.

---

## 8. Webhook Architecture — Failure Modes & Recovery

### Failure mode 1 — Formspree delivers, webhook 500s

Formspree retries failed webhooks 3 times over 24 hours. If the Netlify Function throws an exception, the lead may still arrive in Pipedrive on retry. Monitor Netlify Function logs for the formspree-webhook function.

### Failure mode 2 — Pipedrive API rate limit

The webhook makes 3-4 Pipedrive API calls per submission (Person upsert, Org upsert, Lead create, Note attach). If the daily form volume exceeds the Pipedrive plan's rate limit, calls 4+ will fail. As of 2026-05, no rate limiting has been triggered.

### Failure mode 3 — Hidden field empty

If `ds-includes-v2.js` fails to load or runs before `DOMContentLoaded` completes, hidden UTM fields may be empty on submit. The Lead is still created, but with empty attribution fields. The form submission text is preserved as a fallback record.

### Failure mode 4 — Ad-blocker kills PostHog

PostHog is reverse-proxied through `/ingest/*` specifically to prevent this. If a particular ad-blocker version still blocks the proxy path, only client-side session recording is affected. GA4 and the Pipedrive webhook continue to work because they don't share the PostHog code path.

### Failure mode 5 — Google Ads offline conversion rejected

`ClickConversion` requires the GCLID to be at most 90 days old. If a lead converts more than 90 days after the original click, the upload fails. Monitor the 9am cron output for failed rows.

---

## 9. CSP Requirements (full domain list)

The Content Security Policy in `netlify.toml` must include the following domains for the full attribution stack to work. Always run `python3 site/tools/validate_csp.py` before push.

| CSP Directive | Required Domains | Purpose |
|---|---|---|
| `script-src` | `us-assets.i.posthog.com`, `www.googletagmanager.com`, `www.google-analytics.com`, `c.statcounter.com` | PostHog runtime, GA4, StatCounter |
| `img-src` | `us.i.posthog.com`, `www.google-analytics.com`, `c.statcounter.com`, `googleads.g.doubleclick.net` | Pixel tracking + Google Ads conversion pixels |
| `connect-src` | `us.i.posthog.com`, `*.google-analytics.com`, `formspree.io`, `*.pipedrive.com` | API endpoints |
| `frame-src` | `digitalscientists3.pipedrive.com` | Scheduler iframe |
| `worker-src` | `'self' blob:` | PostHog Web Worker for batching |
| `form-action` | `formspree.io` | Form submission endpoint |

Before any push that touches `netlify.toml` or adds external scripts, manually verify every new domain is in the CSP. Silent CSP blocks are a frequent source of analytics outages — fonts, pixels, third-party scripts, and conversion events all fail without a visible error in production.

See `pipedrive-scheduler-setup.md` for scheduler-specific webhook details and Google Calendar sync.

---

## 10. Operational Memory

The following rules were learned by breaking things in production. Each has a working-memory entry to prevent recurrence:

1. **Manually verify CSP before any push** that adds external scripts or modifies `netlify.toml`. CSP errors silently break analytics in production — fonts, pixels, third-party scripts, and conversion events all fail with no surface error.
2. **Never remove StatCounter.** It's the GA4 backup. (See `feedback_statcounter.md`.)
3. **Never expose PostHog `phx_` (Personal API) keys in client code or chat.** They grant full account access. `phc_` (Project) keys are public-safe by design.
4. **Do not try to create Pipedrive Lead custom fields via API.** Pipedrive doesn't expose this. Always use the Pipedrive UI; then add the new field key to `formspree-webhook.mjs`.
5. **For new Google Ads campaigns:** always set `positive_geo_target_type = PRESENCE` explicitly. Google's default wastes spend on overseas curiosity clicks.
6. **Post-push QA always.** Every push to `digitalscientists.com` requires a post-push QA pass on the live site.

---

## Revision History

- 2026-05-22: v1.0 — Created as companion to `web-implementation.md §17`. Documents the closed-loop attribution stack (Formspree → Netlify Function → Pipedrive Lead → GA4 + PostHog + StatCounter → Google Ads offline conversions → daily morning brief).
