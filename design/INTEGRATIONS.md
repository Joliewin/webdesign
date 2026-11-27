# Integrations — Yunnan Tasty Garden

## Backend API (Primary Integration)

**Selected backend provider:** Supabase is selected for persistent menu and order data. The production project/account, enabled Supabase products, and whether the browser accesses any public interface directly or all operations pass through a trusted server remain undecided. No separate backend API specification or request/response schema is available.

| Template field | Confirmed information or status |
|---|---|
| Base URL/discovery | Unknown; Supabase project and frontend/backend deployment arrangement are not established. |
| Protocol | Not selected. |
| Endpoints/operations | No endpoint paths or contracts confirmed. Conceptual needs: read active menu/options; submit a pickup order; staff authenticate/read orders/update statuses; admins create/update menu records/options. |
| Authentication | Private staff/admin login is required. Provider, session/token method, and authorization policy are undecided. |
| Errors | No status/error schema or field-error contract defined. Customer experience must distinguish validation/rejection/failure; no false order-success confirmation. |
| Pagination | Unknown; no order-list behavior/contract defined. |
| Filtering/sorting | Unknown whether performed by backend or client; no query syntax defined. |
| Versioning | Unknown/not selected. |
| Rate limits | Provider/application request limits and abuse thresholds are unknown. Order-submission abuse protection is required and must not be a blanket one-order-per-IP-per-15-minutes rule. |
| Limitations/gaps | Exact APIs, data model, authorization, and trusted execution path are unknown. The confirmed capabilities require full active menu/options, order persistence, staff order/status operations, and admin menu editing. No client-side workaround or missing endpoint is assumed. |

Order submission must use a trusted server-side path to validate active menu items/options and authoritative prices, enforce operating hours/minimum notice/scheduled-slot capacity, and apply duplicate/abuse controls. Scheduled pickup uses 15-minute slots, a maximum of 8 orders per slot, at least 30 minutes’ notice, and daily 11:00 a.m.–9:30 p.m. hours. Final cutoff, ASAP capacity, timezone handling, and the exact backend contracts remain unknown.

## Data Flows and Persistence

- Customers need to read active menu items, prices, and item-specific options.
- A pickup submission includes required customer name and phone; optional email/notes; selected items/options; and ASAP or scheduled pickup information.
- Orders are accepted on successful submission, persisted in Supabase, and receive an on-site confirmation number only after successful storage.
- Staff use a private interface to view orders and update their status. Admins use a separate private interface to maintain menu items, prices, availability, spice choices, and add-ons.
- Menu data is the current source for customer browsing. Order persistence needs customer/order details, selected items/options, pickup choice/time, confirmation identifier, submission time, and status. Whether historical orders keep item/price/option snapshots is undecided.
- Public access must not expose private order records or customer contact information. Exact access policies are not defined.
- No website order is sent to Square at launch. Payment, delivery, customer notifications, and customer status lookup are deferred.
- Data-retention period and production backup/recovery procedure are undecided.

## External Dependencies

The following are assessed as references or conditional candidates; only Supabase is selected as a provider. Direct production use of the preview’s remote assets/links is not confirmed.

| System | Type / protocol | Data flow and authentication | Privacy and fallback |
|---|---|---|---|
| Supabase | Managed database/backend provider; exact connection/API protocol and direct-vs-server path unknown | Menu reads and order/menu/staff operations are required conceptually. Credentials/auth method are undecided; privileged secrets must not be exposed in browser code. | Customer/order data is involved. Provider-side handling/retention depends on selected plan/configuration and needs review. Failure must not produce false order success; exact outage fallback is undecided. |
| Google Fonts | External font service in existing preview; browser font request if retained | Browser requests font files; no application order data is intentionally required. No API key confirmed. | Provider request metadata/privacy terms require review if retained. Use a local/system fallback if font loading fails; production choice undecided. |
| Unsplash | Remote stock-image host in existing preview; browser image requests if retained | Browser requests stock images; no application order data is intentionally required. No API key confirmed. | Provider request metadata/privacy and licensing/content suitability require review. Image fallback behavior is undecided. Images are not verified restaurant/dish photos. |
| Google Maps | Existing outbound directions link, not a confirmed Maps API/SDK integration | A click navigates to a Google directions URL containing the restaurant destination. No application API key or customer order data is confirmed as sent. | The destination/business details require restaurant confirmation. If the external page is unavailable, customers can use the displayed verified address if supplied; production fallback is undecided. |
| Instagram | Existing preview placeholder (`#home`) | No external request or account integration is confirmed by the placeholder. A production social link/account is unverified. | No confirmed data flow. Do not represent placeholder as an active official account. |
| Square POS | In-store POS, not a website dependency at launch | No website order flow to Square; integration deferred. | No website data flow confirmed. |

No other direct third-party service, payment provider, analytics, notification, or AI provider is selected.

## Browser APIs

| Area | Status |
|---|---|
| Storage (local/session storage, IndexedDB) | No persistent browser storage is confirmed. Cart/client persistence and any auth-token storage strategy are undecided; sensitive order/customer data must not be persisted client-side without approval. |
| Network | Network access is needed for backend operations and any retained remote assets. Specific request API/protocol, WebSocket, and server-sent events are not selected/confirmed. |
| Media | File upload, drag/drop, clipboard, and image preview are not applicable to confirmed v1 capabilities. |
| Navigation | The existing preview uses hash navigation. Production routing/history/query/hash behavior is undecided. |
| Notifications | Browser notifications/badges are not part of confirmed scope; customer email/text notifications are deferred. |
| Other | Geolocation, Web Workers, Canvas, and WebGL are not confirmed or required. |

## State Management Strategy

- **Server state:** Menu, order, status, and admin data need to reflect backend state. Cache technology, TTL, invalidation, optimistic updates/refetch behavior, and stale-while-revalidate are undecided. Order submission must not be acknowledged until persistence succeeds.
- **Client state:** Temporary cart and form/interface state are needed conceptually; mechanism and lifetime are undecided.
- **URL state:** The preview uses hashes, but production route, search/filter, pagination, and dialog URL behavior are not selected.
- **Persistent client state:** Preferences/drafts are unconfirmed. Auth/session storage is undecided; no privileged secrets or unnecessary customer/order details should be stored in browser persistence.
- **Concurrency:** Simultaneous scheduled-order submissions must not exceed the 8-order slot cap. Atomic enforcement belongs on the trusted backend path; exact mechanism is undecided. Concurrent admin edits/conflict behavior is unknown.

## NPM Dependencies

No framework or package choice is confirmed. Each category remains **undecided/not selected**: framework, routing, data fetching, forms, styling, UI components, validation, date/time handling, testing, and build tool. Do not infer a Node version or package manager from the existing static preview.

## Environment & Build

- Runtime/Node version, package manager, build tool/configuration, output format (SPA/MPA/SSR/SSG), bundle-size target, dev-server port/proxy, and hot-reload expectations: **unknown/not selected**.
- Environment variables for backend URL, auth/client identifiers, feature flags, or analytics: **not defined**. Analytics keys are not a confirmed dependency.
- Never commit or expose privileged credentials. Exact secret-management and public configuration boundaries remain for architecture/implementation decisions.

## Deployment & Runtime

- **Hosting:** Not selected. Vercel was discussed but is not assumed. Its Hobby plan is restricted to personal/non-commercial use and should not be assumed suitable for restaurant production.
- **Supabase plan/account:** Not selected. Information reviewed November 27, 2026 indicated Free may pause after one week of inactivity and has no automatic backups; Pro was listed at $25/month with daily backups for 7 days. Recheck current terms/pricing before production.
- **Same origin/CORS:** Frontend/backend domain arrangement and CORS requirements are unknown.
- **Asset loading:** Existing preview loads Google Fonts and Unsplash remotely; production use is undecided. Fallbacks and network-failure presentation need confirmation.
- **Browsers:** The visual reference mentions current Chrome, Edge, Firefox, and Safari on desktop/mobile. The approved Vision leaves production browser support undecided; confirm target versions before release.
- **Polyfills and performance budget:** Unknown/not selected.
- **Operations:** Deployment region, environment separation, monitoring, production data retention, backup/restore ownership, and recovery test remain open.

## Constraints Summary

1. Supabase is selected for persistent menu/order data, but its project, plan, products, APIs, auth, and data policies remain undecided.
2. Trusted server-side processing must validate orders/prices/options and enforce pickup timing, slot capacity, duplicate prevention, and abuse protection; a shared IP alone must not block a customer.
3. Initial scope is pickup-only with no online payment, delivery, Square integration, customer notifications/status lookup, or AI provider.
4. Staff and admins require private access; public users must not access orders/customer data or privileged menu operations.
5. Scheduled pickup is 15-minute slots, 30-minute minimum notice, at most 8 orders per slot, and daily 11:00 a.m.–9:30 p.m.; final cutoff, ASAP capacity, and timezone are unresolved.
6. Production hosting, runtime, environment, Supabase plan, and verified backup/recovery remain undecided; Vercel is not selected.
7. Existing remote assets and third-party business listings are references only; production use/details require confirmation.

## Gaps for Architecture

No endpoint contracts, schemas, base URL, protocol, auth strategy, error format, pagination/filtering/versioning/rate-limit policy, or backend capability inventory is available. Architecture must retain these as explicit decisions rather than fabricate interfaces. It must also resolve trusted server-side execution, public/private access boundaries, browser-vs-server Supabase access, runtime/hosting, state strategy, environment/secrets, and operational recovery. The approved Capabilities’ visual/accessibility outcomes are requirements for the frontend, not selected APIs or packages.

## Sources

- Approved `design/VISION.md` and revised, approved `design/CAPABILITIES.md`.
- Existing preview references: `design/deisgn-md/DESIGN-yunnan.md`, `design/preview/preview-yunnan.html`.
- Business details/provenance: `docs/yunnan/yunnan_info.md`; confirm details before publication.
- [Supabase pricing](https://supabase.com/pricing), reviewed November 27, 2026; recheck before production.
- [Vercel Hobby terms](https://vercel.com/legal/terms#hobby-plan).
