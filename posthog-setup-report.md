<wizard-report>
# PostHog post-wizard report

The wizard has completed a deep integration of PostHog analytics into the DevEvent Next.js App Router project. The following changes were made:

- **`instrumentation-client.ts`** (new) — Initialises PostHog on the client side using Next.js 15.3+ instrumentation. Configures the reverse proxy host (`/ingest`), enables automatic exception capture, and turns on debug mode in development.
- **`next.config.ts`** — Added reverse proxy rewrites (`/ingest/*` → PostHog US ingestion endpoints) and `skipTrailingSlashRedirect: true` so that PostHog trailing-slash requests are handled correctly.
- **`components/ExploreBnt.tsx`** — Added `posthog.capture('explore_events_clicked')` inside the existing button click handler.
- **`components/EventCard.tsx`** — Added `'use client'` directive and `posthog.capture('event_card_clicked', { title, slug, location, date })` on the Link's `onClick`, so that the event title, slug, location, and date are recorded with every click.
- **`.env.local`** — Populated `NEXT_PUBLIC_POSTHOG_KEY` and `NEXT_PUBLIC_POSTHOG_HOST` (never written directly into source files).

| Event | Description | File |
|---|---|---|
| `explore_events_clicked` | User clicks the "Explore Events" CTA button on the home page | `components/ExploreBnt.tsx` |
| `event_card_clicked` | User clicks an event card to navigate to its detail page | `components/EventCard.tsx` |

## Next steps

We've built some insights and a dashboard for you to keep an eye on user behavior, based on the events we just instrumented:

- **Dashboard — Analytics basics:** https://us.posthog.com/project/331109/dashboard/1329655
- **CTA & Event Card Clicks (Daily):** https://us.posthog.com/project/331109/insights/xzamnbB6
- **CTA → Event Card Conversion Funnel:** https://us.posthog.com/project/331109/insights/CiVRDhY9
- **Most Clicked Events (by Slug):** https://us.posthog.com/project/331109/insights/zWVQMLT8
- **Weekly Active Users Browsing Events:** https://us.posthog.com/project/331109/insights/9ajBMDk1

### Agent skill

We've left an agent skill folder in your project. You can use this context for further agent development when using Claude Code. This will help ensure the model provides the most up-to-date approaches for integrating PostHog.

</wizard-report>
