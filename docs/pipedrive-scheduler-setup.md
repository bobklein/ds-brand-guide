# Digital Scientists — Website-to-CRM Integration

## Overview

The digitalscientists.com website connects to Pipedrive CRM through three integrated systems:

1. **Formspree** — Handles all web form submissions (contact forms, newsletter signups)
2. **Pipedrive Scheduler** — Handles meeting bookings (replaced Calendly)
3. **Google Calendar** — Synced two-way with Pipedrive for meeting scheduling

Both Formspree and the Scheduler route into Pipedrive with consistent campaign attribution. UTM parameters from marketing campaigns are captured on the website and written as native custom fields on Pipedrive Deals, enabling campaign-level reporting directly in the CRM.

---

## System Architecture

```
                         digitalscientists.com
                         (Netlify static site)
                                  │
              ┌───────────────────┼───────────────────┐
              │                   │                    │
         Formspree Forms    Pipedrive Scheduler    Analytics
         (20+ pages)        (6 pages)              (GA4, GTM,
              │                   │                 StatCounter,
              │                   │                 LinkedIn, RB2B)
              ▼                   ▼
    Formspree Service      Pipedrive Scheduler
    (formspree.io)         (pipedrive.com)
              │                   │
              │ webhook           │ creates Activity
              ▼                   ▼
    ┌──────────────────────────────────────┐
    │      Netlify Functions (serverless)   │
    │                                      │
    │  formspree-webhook.mjs               │
    │    → Creates Deal or Lead            │
    │                                      │
    │  schedule-lead.mjs                   │
    │    → Pre-booking Deal w/ UTMs        │
    │                                      │
    │  scheduler-webhook.mjs               │
    │    → Post-booking enrichment         │
    └──────────────────┬───────────────────┘
                       │ Pipedrive API
                       ▼
              ┌─────────────────┐
              │    Pipedrive    │
              │      CRM       │
              │                │
              │  Persons       │
              │  Organizations │
              │  Leads         │
              │  Deals         │
              │  Activities    │
              │  Notes         │
              └───────┬────────┘
                      │ two-way sync
                      ▼
              ┌─────────────────┐
              │  Google Calendar │
              │  (Gmail/GSuite) │
              └─────────────────┘
```

---

## 1. Formspree Forms

### What Formspree Does

Formspree (formspree.io) is a form backend service. The website's HTML forms submit directly to Formspree, which:
- Stores the submission
- Sends email notifications
- Fires a webhook to our Netlify Function for Pipedrive integration

All forms use a single Formspree endpoint: `https://formspree.io/f/xvzbywbr`

### Where Forms Appear (Complete Inventory)

Every form on the site has a hidden `source` field (identifies the page) and a hidden `_subject` field (becomes the Lead/Deal title in Pipedrive). UTM hidden fields are injected automatically by `ds-includes-v2.js`.

| Page | Source ID | Pipedrive Title | Also Has Scheduler? |
|---|---|---|---|
| **Core conversion pages** | | | |
| `/` (homepage) | `homepage` | Homepage -- New Lead | No |
| `/start/` | `start-page` | Get Started — New Lead | **Yes** (button) |
| `/proof/` | `proof-landing-page` | Proof in 5 Days — New Lead | No |
| `/method/` | `method-page` | Method Page — New Lead | No |
| `/reasons-to-believe/` | `reasons-to-believe` | Reasons to Believe Page Inquiry | No |
| **Healthcare hub** | | | |
| `/healthcare/` | `healthcare-hub` | Healthcare Hub -- New Lead | No |
| **Healthcare solutions** | | | |
| `/healthcare/solutions/patient-portal-digital-front-door/` | `patient-portal` | Patient Portal Inquiry | No |
| `/healthcare/solutions/electronic-health-record-practice-management/` | `ehr-practice-management` | EHR/Practice Management Inquiry | No |
| `/healthcare/solutions/telemedicine-app-development/` | `telemedicine-app-development` | Telemedicine Solutions Inquiry | No |
| `/healthcare/solutions/healthcare-interoperability-solutions/` | `healthcare-interoperability` | Healthcare Interoperability Inquiry | No |
| `/healthcare/solutions/predictive-analytics-healthcare/` | `predictive-analytics` | Predictive Analytics Inquiry | No |
| `/healthcare/solutions/population-health-management/` | `population-health-management` | Population Health Management Inquiry | No |
| `/healthcare/solutions/remote-patient-monitoring-solutions/` | `remote-patient-monitoring` | Remote Patient Monitoring Inquiry | No |
| `/healthcare/solutions/cdss-clinical-decision-support-system/` | `cdss` | Clinical Decision Support Inquiry | No |
| **Healthcare capabilities** | | | |
| `/healthcare/capabilities/healthcare-ai-development/` | `healthcare-ai-development` | Healthcare AI Development Inquiry | No |
| `/healthcare/capabilities/healthcare-saas-development/` | `healthcare-saas` | Healthcare SaaS Development Inquiry | No |
| `/healthcare/capabilities/healthcare-data-analytics-engineering/` | `healthcare-data-analytics` | Healthcare Data Analytics Inquiry | No |
| `/healthcare/capabilities/healthcare-ux-design-research/` | `healthcare-ux-design` | Healthcare UX Design Inquiry | No |
| `/healthcare/capabilities/software-as-medical-device-samd/` | `software-as-medical-device` | Software as Medical Device (SaMD) Inquiry | No |
| **Healthcare assessment** | | | |
| `/healthcare/assessment/partnership/` | `healthcare-assessment-partnership` | Partnership Assessment Inquiry | No |
| `/healthcare/assessment/platform/` | `healthcare-assessment-platform` | Platform Assessment Inquiry | No |
| **Newsletter popup** (all pages) | `newsletter-popup` | Insights Newsletter — New Subscriber | N/A |

**Pages with Scheduler only (no form):**

| Page | Scheduler Type |
|---|---|
| `/thank-you/` | Button (post-form CTA) |
| `/healthcare/assessment/` | **Embedded iframe** (in-page booking widget) |
| `/event/paltc26-annual-conference/` | 4 buttons (hero + pills + footer) |
| `/event/beckers-health-it-rcm-2026/` | 4 buttons (hero + pills + footer) |
| `/event/2026-nchcfa-annual-convention-expo/` | 1 button (footer) |

**Note:** `/start/` is the only page that has **both** a Formspree form and a Pipedrive Scheduler link.

### Form Fields

**Standard fields** (most forms):
- First name, last name (combined into `name` on submit)
- Email (required — used for Person deduplication in Pipedrive)
- Company (used for Organization lookup in Pipedrive)
- Message / problem description

**Hidden fields** (auto-populated):
- `source` — identifies the form/page (see table above)
- `_subject` — becomes the Lead/Deal title in Pipedrive
- `utm_source`, `utm_medium`, `utm_campaign`, `utm_content`, `utm_term` — injected by JS from sessionStorage

**Additional fields** on some forms: `starting_phase`, `primary_interest`, `platform_type`, `partnership_interest`, `segment`.

### Form → Pipedrive Flow

```
Visitor fills out form on digitalscientists.com
        ↓
Form submits to Formspree (formspree.io/f/xvzbywbr)
        ↓
Formspree stores submission + sends email notification
        ↓
Formspree fires webhook → POST to /.netlify/functions/formspree-webhook
        ↓
formspree-webhook.mjs processes the submission:
        ↓
  1. Find or create Person (deduplicated by email)
  2. Find or create Organization (from company field)
  3. Check for UTM parameters in the submission data
        ↓
  ┌─────────────────────────────────────────────┐
  │  Has UTM params?                            │
  │                                             │
  │  YES → Create Deal                          │
  │    • Pipeline: Inbound Project              │
  │    • Stage: Marketing Qualified             │
  │    • UTM Source/Medium/Campaign/Content      │
  │      as native custom fields                │
  │    • Pinned note with form details          │
  │      + Campaign Attribution section         │
  │                                             │
  │  NO → Create Lead                           │
  │    • Title from form subject                │
  │    • Pinned note with form details          │
  └─────────────────────────────────────────────┘
```

### Formspree Configuration

- **Endpoint:** `https://formspree.io/f/xvzbywbr`
- **Webhook URL:** `https://digitalscientists.com/.netlify/functions/formspree-webhook`
- **Webhook handshake:** Formspree sends an `x-hook-secret` header on first setup; the function echoes it back
- **Error handling:** Function always returns HTTP 200 to prevent Formspree from retrying endlessly. Errors are logged server-side.

---

## 2. Pipedrive Scheduler

### What Changed

We replaced Calendly with Pipedrive's native Scheduler in March 2026. This eliminates a third-party dependency and creates meetings natively in Pipedrive.

### Where the Scheduler Appears

| Page | Type | Link/Embed |
|------|------|------------|
| `/start/` | Button | "Schedule a 30-Minute Call" |
| `/thank-you/` | Button | "Schedule a 30-Minute Call" (post-form CTA) |
| `/healthcare/assessment/` | **Embedded iframe** | In-page booking widget |
| `/event/paltc26-annual-conference/` | Buttons (4) | Hero CTA + "Book time" pills + footer CTA |
| `/event/beckers-health-it-rcm-2026/` | Buttons (4) | Hero CTA + "Book time" pills + footer CTA |
| `/event/2026-nchcfa-annual-convention-expo/` | Button | Footer CTA |

All point to: `https://digitalscientists3.pipedrive.com/scheduler/kOOeAEu2/meeting-with-bob-klein`

The assessment page uses an iframe embed; all others are outbound links that open in a new tab.

### Scheduler Booking Fields

When a prospect books, the Pipedrive Scheduler collects:
- Name
- Email
- Phone
- Company
- Agenda for Call (free text)

These are written to the Activity's note field in Pipedrive.

### Scheduler → Pipedrive Flow (Two Phases)

The scheduler integration is more complex than forms because the booking happens on Pipedrive's domain (not ours), so we can't capture UTM data and contact details in the same request. This is solved with a two-phase approach:

#### Phase 1: Pre-Booking (happens on our site, before redirect)

```
Visitor clicks "Schedule a Call" on digitalscientists.com
        ↓
ds-includes-v2.js intercepts the click
        ↓
Reads UTM data from sessionStorage
        ↓
POST to /.netlify/functions/schedule-lead
        ↓
  ┌─────────────────────────────────────────────┐
  │  Has UTM params?                            │
  │                                             │
  │  YES → Create Deal (no person yet)          │
  │    • Pipeline: Inbound Project              │
  │    • Stage: Marketing Qualified             │
  │    • Title: "Scheduler from {page} ({campaign})" │
  │    • UTM fields populated natively          │
  │    • Person: none (we don't know who yet)   │
  │                                             │
  │  NO → Passthrough (no Pipedrive action)     │
  └─────────────────────────────────────────────┘
        ↓
Browser redirects to Pipedrive Scheduler
(2-second timeout fallback — booking is never blocked)
```

#### Phase 2: Post-Booking (happens after prospect completes the booking)

```
Prospect enters details + picks a time on Pipedrive Scheduler
        ↓
Pipedrive creates:
  • Person (or finds existing, deduplicated by email)
  • Organization (from company field)
  • Activity (type: meeting) with note containing form text
        ↓
Pipedrive Webhook #3102756 fires (event: activity.create)
        ↓
POST to /.netlify/functions/scheduler-webhook
        ↓
Webhook handler:
  1. Verifies this is a Scheduler activity (subject contains "Meeting with Bob Klein")
  2. Fetches full Activity details via API (note text is omitted from webhook payload)
  3. Searches for a recent unlinked Deal (title "Scheduler...", no person, last 10 min)
        ↓
  ┌─────────────────────────────────────────────┐
  │  Found a matching Deal?                     │
  │                                             │
  │  YES → Enrich the Deal                      │
  │    • Link Person to the Deal                │
  │    • Link Organization to the Deal          │
  │    • Link Activity to the Deal              │
  │    • Add form text as pinned note           │
  │    (UTM fields already on the Deal from     │
  │     Phase 1 — now it has everything)        │
  │                                             │
  │  NO → Create Lead                           │
  │    • Title: "Scheduler — {Person Name}"     │
  │    • Link Person + Organization             │
  │    • Add form text as pinned note           │
  └─────────────────────────────────────────────┘
        ↓
Activity syncs to Google Calendar
```

---

## 3. Google Calendar Integration

### How It Works

Pipedrive's native calendar sync connects Pipedrive Activities to Google Calendar (Gmail/GSuite):

- **Direction:** Two-way sync
- **What syncs:** Pipedrive Activities ↔ Google Calendar events
- **Activity types:** "Meeting" must be enabled for sync in Pipedrive settings

### Setup Location

Pipedrive → Settings → Calendar Sync → Google Calendar

### The Sync Chain for Scheduler Bookings

```
Prospect books on Pipedrive Scheduler
        ↓
Pipedrive creates Activity (type: meeting)
  • Due date + time from the booking
  • Person linked (prospect)
  • Subject: "{Prospect Name} / Bob Klein - Meeting with Bob Klein"
  • Note: name, phone, company, agenda
        ↓
Pipedrive calendar sync pushes to Google Calendar
        ↓
Meeting appears on Bob's Gmail calendar
  • With time, prospect name, and details
  • Bob gets a calendar notification
```

### Why Not Calendly?

| | Calendly | Pipedrive Scheduler |
|---|---|---|
| CRM integration | Required third-party integration (none natively available) | Native — creates Person + Activity directly |
| Calendar sync | Writes directly to Google Calendar (could duplicate) | Syncs via Pipedrive's calendar integration (single source of truth) |
| Lead/Deal creation | Not supported | Via our webhook function |
| Cost | Separate subscription | Included in Pipedrive Professional |
| Form flexibility | More customizable | Basic fields only |

The tradeoff: Pipedrive Scheduler's booking form is less flexible than Calendly's (or Formspree's), but the native CRM integration eliminates an entire middleware layer.

---

## UTM Attribution System

### How UTMs Are Captured

1. Visitor arrives with UTM parameters in the URL (e.g., from a LinkedIn ad, email campaign, or Google Ads)
2. `ds-includes-v2.js` extracts `utm_source`, `utm_medium`, `utm_campaign`, `utm_content`, and `utm_term` from the URL
3. Values are stored in `sessionStorage` (key: `ds_utm`)
4. UTMs persist across page navigations within the same browser tab/session
5. When the visitor converts (form or scheduler), UTMs are passed to the Netlify Function

### UTM Parameters

| Parameter | Purpose | Example Values |
|---|---|---|
| `utm_source` | Traffic source | `linkedin`, `google`, `email`, `twitter` |
| `utm_medium` | Marketing medium | `cpc`, `social`, `email`, `organic` |
| `utm_campaign` | Campaign name | `paltc26`, `beckers2026`, `spring-nurture` |
| `utm_content` | Ad/CTA variant | `hero-cta`, `sidebar-ad`, `email-button` |
| `utm_term` | Search keyword | (used for paid search) |

### Pipedrive Deal Custom Fields

These fields are created on the Deal object in Pipedrive and populated natively (not as text notes):

| Field Name | Pipedrive API Key | Type |
|---|---|---|
| UTM Source | `2d987c86f8c2ba6d4a2ba671202fb101963cb7ae` | Text |
| UTM Medium | `5bc2cf59b8f65bac7fee4f0049decda09e64eefb` | Text |
| UTM Campaign | `f6983c094a3678e33fa339a912595b1d8c1a0ed3` | Text |
| UTM Content | `de10675163c2f6d75a0699052c21d3a36e71091e` | Text |
| Source Page | `1fe5fef0101f8b10a757d9944b072e0c098da15a` | Text |

These are filterable, sortable, and reportable in Pipedrive's built-in reporting.

### Why Deals and Not Leads?

Pipedrive Leads **do not support custom fields**. This is a Pipedrive platform limitation. UTM data can only be stored natively on Deals (or as plain text in notes, which is not filterable or reportable).

Our routing rule:

| Visitor has UTMs? | Record type | Rationale |
|---|---|---|
| **Yes** | **Deal** in Inbound Project → Marketing Qualified | Campaign attribution stored as native fields |
| **No** | **Lead** in inbox | No attribution data to store — qualify manually |

UTM data is also written into the pinned note (under "Campaign Attribution") for quick reference regardless of record type.

---

## End-to-End Examples

### Example 1: LinkedIn Ad → Form Submission

1. Marketing runs a LinkedIn campaign for PALTC26 with link: `https://digitalscientists.com/start/?utm_source=linkedin&utm_medium=cpc&utm_campaign=paltc26`
2. Dr. Martinez clicks the ad, lands on `/start/`
3. JS captures UTMs into sessionStorage
4. Dr. Martinez fills out the contact form (name, email, company, message)
5. Form submits to Formspree → webhook fires → `formspree-webhook.mjs` runs
6. **Result in Pipedrive:**
   - Person: Dr. Martinez (linked by email)
   - Organization: Midwest Health Partners
   - Deal: "Website Inquiry" in Inbound Project → Marketing Qualified
   - UTM Source: `linkedin` / UTM Medium: `cpc` / UTM Campaign: `paltc26`
   - Pinned note: form details + Campaign Attribution section

### Example 2: Email Campaign → Scheduler Booking

1. Marketing sends an email with link: `https://digitalscientists.com/event/paltc26-annual-conference/?utm_source=email&utm_medium=email&utm_campaign=paltc26-invite`
2. Sarah Johnson clicks the link, lands on the event page
3. JS captures UTMs into sessionStorage
4. Sarah clicks "Schedule a Meeting"
5. **Phase 1:** `schedule-lead.mjs` creates Deal with UTMs (no person yet)
6. Browser redirects to Pipedrive Scheduler
7. Sarah enters her details and picks a time
8. **Phase 2:** Pipedrive creates Activity → webhook fires → `scheduler-webhook.mjs` enriches the Deal
9. **Result in Pipedrive:**
   - Person: Sarah Johnson (linked by webhook)
   - Organization: HealthTech Solutions (linked by webhook)
   - Deal: "Scheduler from event/paltc26-annual-conference (paltc26-invite)"
   - UTM Source: `email` / UTM Medium: `email` / UTM Campaign: `paltc26-invite`
   - Source Page: `event/paltc26-annual-conference`
   - Pinned note: "Name: Sarah Johnson, Phone: ..., Company: HealthTech Solutions, Agenda: ..."
   - Activity: Meeting linked to the Deal
   - Google Calendar: Meeting on Bob's calendar with time + details

### Example 3: Organic Search → Form Submission (No UTMs)

1. A prospect finds digitalscientists.com via Google organic search
2. Browses to `/proof/` and fills out the contact form
3. No UTMs in sessionStorage
4. **Result in Pipedrive:**
   - Person: created/found
   - Lead: "Proof in 5 Days — New Lead" (in Lead inbox, not pipeline)
   - Pinned note: form details (no Campaign Attribution section)

### Example 4: Direct Visit → Scheduler Booking (No UTMs)

1. A prospect types `digitalscientists.com/healthcare/assessment/` directly
2. Uses the embedded scheduler iframe to book a meeting
3. No UTMs, no pre-booking Deal created
4. **Phase 2 webhook only:** Creates Lead directly
5. **Result in Pipedrive:**
   - Person: linked from booking details
   - Organization: linked from booking details
   - Lead: "Scheduler — {Person Name}"
   - Pinned note: booking form text (name, phone, company, agenda)
   - Activity: Meeting on Google Calendar

---

## Technical Reference

### Netlify Functions

| Function | Trigger | Purpose |
|---|---|---|
| `formspree-webhook.mjs` | Formspree webhook (POST) | Processes form submissions → Deal or Lead |
| `schedule-lead.mjs` | Frontend JS (POST) | Pre-booking: creates Deal with UTMs for campaign traffic |
| `scheduler-webhook.mjs` | Pipedrive webhook (POST) | Post-booking: enriches Deal with contact info, or creates Lead |

### External Service Connections

| From | To | Connection Type | Credential |
|---|---|---|---|
| Website forms | Formspree | HTML form action (`formspree.io/f/xvzbywbr`) | None (public endpoint) |
| Formspree | Netlify Function | REST webhook (`x-hook-secret` handshake) | Configured in Formspree dashboard |
| Netlify Functions | Pipedrive API | REST API (v1) | `PIPEDRIVE_API_TOKEN` env var in Netlify |
| Pipedrive | Netlify Function | Webhook v2.0 (#3102756, `activity.create`) | Registered via Pipedrive API |
| Pipedrive | Google Calendar | Native two-way calendar sync | OAuth (configured in Pipedrive Settings) |
| Website | Pipedrive Scheduler | iframe embed + outbound links | Public scheduler URL |

### Content Security Policy

The `netlify.toml` CSP headers whitelist the following for Pipedrive:
- `frame-src`: `digitalscientists3.pipedrive.com` (scheduler iframe)
- `connect-src`: `*.pipedrive.com` (API calls, LeadBooster)
- `script-src`: `webforms.pipedrive.com`, `leadbooster-chat.pipedrive.com`

### Environment Variables (Netlify)

| Variable | Purpose |
|---|---|
| `PIPEDRIVE_API_TOKEN` | Authenticates all Pipedrive API calls from Netlify Functions |

### Pipedrive Configuration

| Setting | Location | Value |
|---|---|---|
| Webhook #3102756 | Settings → Webhooks | `activity.create` → `scheduler-webhook.mjs` |
| Calendar sync | Settings → Calendar Sync | Google Calendar, two-way, Meetings enabled |
| UTM custom fields | Settings → Data Fields → Deal | 5 fields (see table above) |
| Scheduler | Settings → Scheduler | `kOOeAEu2/meeting-with-bob-klein` |

---

## Resilience & Failure Modes

| Failure | Impact | Mitigation |
|---|---|---|
| Pre-booking function fails | Visitor still reaches Scheduler (2s timeout fallback) | Webhook creates Lead without UTMs |
| Webhook doesn't fire | Scheduler still creates Activity + Person | Lead/Deal must be created manually |
| Formspree webhook fails | Formspree still stores submission + sends email | Function returns 200 to prevent retries; check Netlify logs |
| Pipedrive API down | Functions log errors, return gracefully | Formspree retains submissions; Scheduler retains bookings |
| UTM sessionStorage cleared | No campaign data captured | Visitor used private browsing or cleared storage — rare |
| Concurrent campaign bookings | Webhook could mismatch Deals (10-min window) | Extremely rare in B2B; review deal titles if suspicious |

---

## Pipedrive Reporting

With UTM fields on Deals, you can build reports to answer:

- **Which campaigns generate the most deals?** → Group by UTM Campaign
- **Which channels perform best?** → Group by UTM Source
- **Which pages convert best?** → Group by Source Page
- **What's the pipeline value by campaign?** → Filter by UTM Campaign, sum Deal values
- **Campaign → close rate?** → Filter by UTM Campaign, compare won vs total
- **Form vs Scheduler conversion mix?** → Filter by title prefix ("Website Inquiry" vs "Scheduler from")

---

## Webhook Payload Reference (Pipedrive v2.0)

```json
{
  "data": {
    "id": 12345,
    "type": "meeting",
    "subject": "Jane Smith / Bob Klein - Meeting with Bob Klein",
    "person_id": 20348,
    "org_id": 13528,
    "due_date": "2026-03-25",
    "due_time": { "value": "10:00:00" }
  },
  "previous": null,
  "meta": {
    "action": "create",
    "entity": "activity",
    "version": "2.0"
  }
}
```

**Important:** The `note` field (booking form text) is not included in the webhook payload. The webhook handler fetches it via a separate API call to `GET /activities/{id}`.
