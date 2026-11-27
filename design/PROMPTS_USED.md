# Saved Prompts

## Table of Contents
- [Prompt 1: Project context and vision](#prompt-1-project-context-and-vision)
  - [Prompt 1 Original](#prompt-1-original)
- [Prompt 2: Capabilities and acceptance criteria](#prompt-2-capabilities-and-acceptance-criteria)
  - [Prompt 2 Original](#prompt-2-original)
  - [Prompt 2 Revision 1](#prompt-2-revision-1)
- [Prompt 3: Integrations and external constraints](#prompt-3-integrations-and-external-constraints)
  - [Prompt 3 Original](#prompt-3-original)
  - [Prompt 3 Revision 1](#prompt-3-revision-1)
- [Prompt 4: Threat Model](#prompt-4-threat-model)
  - [Prompt 4 Original](#prompt-4-original)
  - [Prompt 4 Revision 1](#prompt-4-revision-1)
- [Prompt 5: Architecture](#prompt-5-architecture)
  - [Prompt 5 Original](#prompt-5-original)
  - [Prompt 5 Revision 1](#prompt-5-revision-1)
  - [Prompt 5 Revision 2](#prompt-5-revision-2)
  - [Prompt 5 Revision 3](#prompt-5-revision-3)
- [Prompt 6: Ordered stories](#prompt-6-ordered-stories)
  - [Prompt 6 Original](#prompt-6-original)
  - [Prompt 6 Revision 1](#prompt-6-revision-1)
  - [Prompt 6 Revision 2](#prompt-6-revision-2)
- [Prompt 7: Critical path and waves](#prompt-7-critical-path-and-waves)
  - [Prompt 7 Original](#prompt-7-original)
  - [Prompt 7 Revision 1](#prompt-7-revision-1)
  - [Prompt 7 Revision 2](#prompt-7-revision-2)
- [Prompt 8: Project progress tracker](#prompt-8-project-progress-tracker)
  - [Prompt 8 Original](#prompt-8-original)
  - [Prompt 8 Revision 1](#prompt-8-revision-1)
- [Prompt 9: AI productivity metrics](#prompt-9-ai-productivity-metrics)
  - [Prompt 9 Original](#prompt-9-original)
  - [Prompt 9 Revision 1](#prompt-9-revision-1)
- [Prompt 10: Consistency audit](#prompt-10-consistency-audit)
  - [Prompt 10 Original](#prompt-10-original)
  - [Prompt 10 Revision 1](#prompt-10-revision-1)
  - [Prompt 10 Revision 2](#prompt-10-revision-2)
- [Prompt 11: Land the walking skeleton](#prompt-11-land-the-walking-skeleton)
  - [Prompt 11 Original](#prompt-11-original)
  - [Prompt 11 Revision 1](#prompt-11-revision-1)
- [Prompt 12: Implement one story](#prompt-12-implement-one-story)
  - [Prompt 12 Original](#prompt-12-original)
- [Prompt 13: Review a planned checkpoint](#prompt-13-review-a-planned-checkpoint)
  - [Prompt 13 Original](#prompt-13-original)

## Prompt 1: Project context and vision

### Prompt 1 Original
- Approval: approved
- Current: no

```

Create or refine `design/VISION.md` for the **Yunnan Tasty Garden** website.

Use these confirmed project details:
- The goal is to build a full-stack website, not only reproduce the existing static preview. Existing references are `design/deisgn-md/DESIGN-yunnan.md` and `design/preview/preview-yunnan.html`.
- The initial release supports pickup ordering from the full menu. Delivery and online payment are deferred.
- Customers can choose ASAP pickup or a scheduled time. Scheduled pickups use 15-minute slots and require at least 30 minutes’ notice. Intended ordering hours are daily 11:00 a.m.–9:30 p.m.; exact slot capacity and cutoff rules are undecided.
- On submission, an order is automatically accepted, stored in a backend database, and the customer sees an on-site confirmation number. Customer email/text notifications and later order-status lookup are deferred.
- Checkout requires the customer’s name and phone number; email and order notes are optional.
- Restaurant staff need a private dashboard with basic login to view orders and update their status. More detailed staff roles are deferred.
- An admin interface must let authorized admins create and edit menu items, prices, dish-specific spice levels, and add-ons. Menu and option details should be maintained in the database, not hard-coded.
- Square is currently used in-store only. Square POS integration is deferred for later investigation; do not imply orders reach Square in the initial scope.
- The success target is **20 online pickup orders per week**.
- Starbucks’ ordering experience may be reviewed for high-level UX inspiration, but do not copy its branding or content.
- Existing project references are `design/deisgn-md/DESIGN-yunnan.md` and `design/preview/preview-yunnan.html`. `docs/yunnan/yunnan_info.md` contains business details sourced from third-party listings; confirm them with the restaurant before publication. Sample dishes/prices and placeholder AI/order controls in the preview are not verified or operational.

Produce a concise Vision with **Problem**, **Users**, **Success**, **Non-Goals**, and **Constraints** sections. Cover customers placing pickup orders, staff managing orders, and admins maintaining the menu. Keep initial scope distinct from deferred features.

Use supplied project context and existing files; do not invent facts, technology choices, payment arrangements, or operational rules. Ask one focused question at a time for information needed to complete the Vision. Keep unresolved details explicit, including menu options, pickup-slot capacity/cutoffs, verified business details, hosting, technology, and accessibility/browser requirements. Do not write the Vision until necessary context is clear.
```

## Prompt 2: Capabilities and acceptance criteria

### Prompt 2 Original
- Approval: approved
- Current: no

```
Based on the approved `design/VISION.md`, create `design/CAPABILITIES.md` for the Yunnan Tasty Garden full-stack website.

Define the smallest useful end-to-end walking skeleton, core capabilities, and intentionally deferred capabilities. Describe what customers, restaurant staff, and admins can do and observe. Do not choose frameworks, database products, payment providers, or implementation architecture.

**Confirmed initial-release scope**
- Customers order from the full menu for pickup. Delivery and online payment are deferred.
- Customers can configure only the spice levels and add-ons that apply to each dish, choose ASAP or scheduled pickup, submit the order, and receive an on-site confirmation number.
- Orders are accepted on submission and stored in a backend database. Checkout requires name and phone; email and order notes are optional.
- Scheduled pickup uses 15-minute slots, at least 30 minutes’ notice, and a maximum of 8 orders per slot. Ordering hours are daily 11:00 a.m.–9:30 p.m. The final-slot and cutoff behavior is undecided.
- Staff need a basic-login private dashboard to view orders and update status. Admins need a separate interface to maintain menu items, prices, and dish-specific spice levels and add-ons in the database.
- Protect order submission from accidental duplicates and abuse using server-side controls. Do not impose a blanket one-order-per-IP-per-15-minutes rule. Exact signals and thresholds are undecided.
- Square POS integration, delivery, online payments, staff roles, customer notifications, and order-status lookup are deferred.
- Success target: 20 online pickup orders per week.

**Confirmed deferred AI capability**
- A later release may deploy a small AI model for customer-facing menu recommendations. It should use the existing menu and consider taste/spice preferences, dietary needs, budget, and group size.
- The AI recommends existing dishes; it does not create menu items. Customers may choose one or more suggested dishes individually—or none—to add to their order.
- The model and deployment approach are undecided. Keep this capability separate from the initial release.

For each capability, provide its name, user-facing purpose, priority, dependencies, and concrete acceptance criteria, including relevant interactions and success/error states. Identify a thin end-to-end walking skeleton that demonstrates an order being submitted, stored, acknowledged, and visible to staff. Include the admin menu-maintenance capability in the plan. Include the deferred AI capability with criteria consistent with its deferred status.

Use the approved Vision as authoritative. Existing preview materials may inform the visual experience, but do not treat sample dishes/prices or placeholder controls as verified operational behavior. The project requested Starbucks ordering UX as inspiration, not copied branding or content; the available text fetch returned no readable content, so do not claim specific Starbucks behaviors as observed.

Preserve unknowns explicitly. Do not invent menu/options data, ASAP-order capacity, final pickup cutoff behavior, technical choices, or AI model details. Ask one focused question at a time where clarification is needed; leave unresolved decisions visible rather than guessing. Present the generated document for separate review; prompt approval does not approve the document.
```

### Prompt 2 Revision 1
- Approval: approved
- Current: yes

```
Based on the approved `design/VISION.md`, revise `design/CAPABILITIES.md` for the Yunnan Tasty Garden website.

**Before writing, review these sources if applicable:**
- The approved `design/VISION.md`.
- The existing `design/CAPABILITIES.md`, preserving decisions that remain consistent with the approved Vision.
- Any separate backend capabilities document or backend API documentation, if present. None was found during preparation; do not invent backend endpoints or contracts.
- `design/deisgn-md/DESIGN-yunnan.md` and `design/preview/preview-yunnan.html` as visual/interaction references only, not as sources of verified operational data or behavior.

Describe what users can do and observe, not implementation architecture. Preserve confirmed decisions and make unknowns explicit. If requirements conflict, use the approved Vision and surface the conflict. Do not invent operational facts, endpoints, or technical choices.

## Walking Skeleton (MVP)
Identify the smallest end-to-end slice that exercises the customer-facing experience and staff outcome.

Include:
- **Name**
- **User Story** in standard “As a…, I want…, so that…” form
- **Acceptance Criteria** with specific, testable user-visible conditions for rendering, interaction, data/API integration behavior where a backend operation is confirmed, and displayed results

The slice must demonstrate that a customer can browse available menu items, configure applicable options, submit a pickup order, have it stored, receive an on-site confirmation only after successful storage, and have staff see and manage it in the private dashboard. Include admin menu maintenance in the v1 capability plan, even if it is outside the smallest walking-skeleton slice.

## Core Capabilities
For each capability required in v1.0, include:
- **Name**
- **User Story**
- **Acceptance Criteria**: concrete UI/UX outcomes covering relevant loading, success, empty, and error states; validation and error messages; data display/formatting; user interactions; keyboard and screen-reader accessibility
- **Priority**: Must / Should / Could
- **Dependencies**: other capabilities it builds on

Preserve these confirmed initial-release requirements:
- Customers can browse the full active menu and prices, and configure only item-specific spice choices or add-ons that apply to each dish.
- Customers can add, review, change, or remove items/options in a cart.
- Checkout requires customer name and phone; email and order notes are optional.
- Customers choose ASAP or scheduled pickup. Scheduled pickup uses 15-minute slots, at least 30 minutes’ notice, a maximum of 8 orders per slot, and daily 11:00 a.m.–9:30 p.m. hours. Final-slot/cutoff behavior and ASAP capacity remain unresolved.
- Successful submission stores the order and shows an on-site confirmation number; failed submission must not look successful.
- Server-side order-abuse protections must reduce accidental duplicates and abuse without a blanket one-order-per-IP-per-15-minutes rule. Exact signals and thresholds remain undecided.
- Staff sign in to a private dashboard, view submitted orders and necessary details, and update status. Statuses currently confirmed are new, preparing, ready, completed, and cancelled.
- Admins use a separate private interface to maintain menu items, prices, spice-level choices, add-ons, and availability without editing code.
- Success target: 20 online pickup orders per week.
- The verified full menu and exact dish-specific options are still needed; sample preview content is not verified.

## Frontend Design System
Define the visual language and interaction patterns for the user-facing experience. Carry forward the existing warm, contemporary restaurant-editorial direction from the visual reference; do not copy placeholder AI/order behavior as operational functionality.

### Color Palette
State background/surface, text, action/link, semantic feedback, and border/divider colors. Preserve the existing reference palette where applicable: burgundy `#6b1f2a`, deep burgundy `#48151d`, hover burgundy `#842d38`, orange/copper `#d96b32`, cream `#fff4e5`, deep cream `#f5e8d6`, espresso `#2b211d`, muted brown `#665750`, and border `#e6d8c7`. Identify any semantic colors not established by the reference as undecided rather than guessing.

### Typography
Record font families, weights, sizing hierarchy, line-height, and letter-spacing. The reference uses Bitter for headings/brand, Inter for body/prices/controls, and Montserrat for uppercase eyebrow text. Include sensible fallbacks; do not assume remote font availability.

### Spacing System
Describe the reference’s spacing philosophy and known values: adaptive section gutters `clamp(36px, 7.5vw, 144px)` on desktop and 27px on mobile; narrower gutters for header/footer/home hero; 4/8-based exact scale and component padding remain unspecified unless supported by the reference.

### Texture & Atmosphere
Describe supported surface treatments, shadows, borders/radii, and transparency from the existing design reference. Preserve its restrained editorial treatment; mark details without evidence as undecided.

### Interactions
Describe transition/reduced-motion behavior, hover, visible keyboard focus, loading, disabled, validation/error, and confirmation states. Preserve the reference’s visible focus and reduced-motion expectations; do not invent behavior for deferred features.

## Future Capabilities
List intentionally deferred capabilities and why they are deferred:
- A later customer-facing small AI model may recommend only existing menu items using taste/spice preferences, dietary needs, budget, and group size. Customers may add one or more suggestions individually, or none; suggestions are not added automatically. Model, deployment, data handling, allergy safeguards, and ownership remain undecided.
- Delivery, online payment, Square POS integration, customer email/text notifications, customer order-status lookup, and multiple staff roles/permissions are not in the initial release.

Include responsive design and accessibility in v1 rather than listing them as deferred. Keep the acceptance criteria user-visible and avoid prescribing React components, state management, APIs, libraries, or backend architecture.

Preserve the existing order-abuse, pickup, menu, staff, admin, and deferred-AI decisions. Do not treat placeholder controls or sample dishes/prices as operational facts. If a necessary detail remains unknown, record it explicitly rather than filling it in.

Save the revised draft to `design/CAPABILITIES.md` and present it for separate review. Approval of this prompt does not approve the generated document. After generating the new Capabilities document, pause; the developer will decide whether to update downstream documents.
```

## Prompt 3: Integrations and external constraints

### Prompt 3 Original
- Approval: approved
- Current: no

```
Based on the approved `design/VISION.md` and `design/CAPABILITIES.md`, create `design/INTEGRATIONS.md` for the Yunnan Tasty Garden website.

Record confirmed external systems and constraints, information flows, and persistent state that the architecture must respect. Describe only confirmed interfaces and services; mark unknowns clearly. Do not invent API endpoints, credentials, service guarantees, or implementation details.

**Confirmed context**
- **Supabase is the selected backend/database provider** for persistent menu and order data. The Supabase plan tier, account status, exact APIs, and whether Supabase Auth will handle staff login are not yet decided.
- Customers submit pickup orders to the backend; order details include customer name and phone, optional email/notes, selected menu items/options, and pickup time. Menu items, prices, spice levels, and add-ons are maintained in the database through a separate admin interface.
- Scheduled pickup uses 15-minute slots, at least 30 minutes’ notice, and a maximum of 8 orders per slot. Order submission must enforce these rules server-side. Final cutoff behavior and ASAP capacity remain unknown.
- Basic staff/admin login is required. Staff can view and update orders; admins can manage menu data. Authentication implementation and data-access boundaries remain to be decided.
- Online payment, delivery, Square POS integration, customer email/text, and customer status lookup are deferred. A small customer-facing AI model for menu recommendations is also deferred; do not include an initial-release AI provider or data integration.
- Vercel was discussed as possible hosting but has **not** been selected. Its Hobby plan is restricted to personal or non-commercial use; don’t assume it is suitable for this restaurant’s production site.
- Existing preview assets use Google Fonts and remote Unsplash images. The visit section links to Google Maps; Instagram currently points to a placeholder. Treat these as existing references, not automatic requirements for the new production site.
- Business details in `docs/yunnan/yunnan_info.md` come from third-party listings and require confirmation before publication.

Include concise sections for:
- Confirmed systems and their role (including Supabase)
- Data flows and stored data, especially customer/order/menu information
- Authentication and access boundaries, distinguishing confirmed requirements from undecided implementation
- Browser/client and external asset dependencies that remain relevant
- Hosting, environment, and operational constraints that are known or still unresolved
- Deferred integrations and explicit gaps

For any missing decision needed to complete the document, ask one focused question at a time. Distinguish confirmed “none” from “not yet known.” Do not turn a hosting discussion into a selection, assume Supabase Auth, or choose the Supabase plan. Save the draft to `design/INTEGRATIONS.md` and present it for separate review; approval of this prompt does not approve the generated document.
```

### Prompt 3 Revision 1
- Approval: approved
- Current: yes

```
Based on the approved `design/VISION.md` and revised, approved `design/CAPABILITIES.md`, revise `design/INTEGRATIONS.md` for the Yunnan Tasty Garden website.

Before writing, reread this approved prompt and review:
- `design/VISION.md` and `design/CAPABILITIES.md`.
- The existing `design/INTEGRATIONS.md`, preserving confirmed decisions that remain consistent with the approved upstream documents.
- Backend API endpoint documentation, request/response schemas, and backend `design/INTEGRATIONS.md`, if present. No separate backend API specification was found during preparation; do not invent endpoints or contracts.
- Existing visual/reference files only as evidence of current preview dependencies, not as automatic production requirements.

Map every confirmed external system, API, database, browser capability, and runtime/build constraint that the application may touch. Distinguish confirmed interfaces from those controlled by the project; distinguish confirmed “none” from “not known/not selected.” Preserve existing decisions unless revised approved upstream documents conflict. Do not select products, frameworks, APIs, protocols, hosting, or credentials that remain undecided.

## Backend API (Primary Integration)
Document the interface the frontend will consume. For each template field, state the confirmed value or explicitly mark it unknown/not yet selected:
- Base URL and how the frontend discovers it.
- Protocol.
- Endpoints/operations by resource, with method/path/purpose/request/response only when documented; otherwise identify the needed conceptual operation and state that the contract is not defined.
- Authentication.
- Error format and field-level validation behavior.
- Pagination.
- Filtering and sorting.
- Versioning.
- Rate limits/throttling.
- Backend limitations and capability gaps; note client-side workarounds or missing backend operations only when supported by confirmed facts.

Supabase is selected as the managed backend/database provider, but direct browser-versus-server access, Supabase products/APIs, endpoint contracts, auth, and data policies are undecided. The trusted server-side path must enforce order validation, prices, pickup rules, capacity, and abuse protection. Do not imply browser-only enforcement or expose privileged credentials.

## External Dependencies
For every external system the frontend calls directly, record:
- System and type.
- Protocol/connection method.
- Data sent and received.
- Authentication/keys, or confirmed none; otherwise unknown.
- Privacy implications of data sent to the provider.
- Fallback behavior or explicit unknown.

Assess conditionally, without assuming continued production use: Supabase; Google Fonts; Unsplash images; the Google Maps directions link; and the Instagram placeholder. Square is in-store POS only and website integration is deferred. Payment, delivery, notifications, status lookup, and AI providers are deferred; do not create launch integrations for them. Distinguish a simple outbound link from an API/SDK integration.

## Browser APIs
Record what the production frontend uses or needs, marking each confirmed, not selected, unknown, or not applicable:
- Storage: local/session storage, IndexedDB, and what data if any.
- Network: request transport, WebSocket, or server-sent events.
- Media: uploads, drag/drop, clipboard, image preview.
- Navigation: History API, URL/query/hash state.
- Notifications: browser notifications/badges.
- Other browser APIs such as geolocation, workers, canvas, or WebGL.
The existing preview uses hash navigation and remote assets, but the production behavior remains to be confirmed.

## State Management Strategy
Describe confirmed needs and mark the chosen mechanism/strategy unknown when undecided:
- Server state: caching/synchronization, freshness/TTL, invalidation, optimistic updates/refetch behavior, stale-while-revalidate.
- Client state: ephemeral interface state.
- URL state: filters, pagination, dialog/navigation state.
- Persistent client state: preferences, draft forms, or authentication tokens; do not propose storing sensitive data without approval.
- Concurrency: handling simultaneous edits/order submissions.

## NPM Dependencies
List the template categories and confirmed choices, or mark them undecided/not selected:
- Framework.
- Routing.
- Data fetching.
- Forms.
- Styling.
- UI components.
- Validation.
- Date/time.
- Testing.
- Build tool.
Do not introduce package names or dependency recommendations as decisions.

## Environment & Build
Record known values or mark unknown:
- Runtime/Node version.
- Package manager.
- Build tool/configuration.
- Required environment variables (backend URL, auth/client IDs, feature flags, analytics keys); distinguish required, not applicable, and unknown. Never include secrets.
- Output type (SPA/MPA/SSR/SSG) and bundle-size target.
- Development server port/proxy arrangement.
- Hot-reload expectations/limitations.

## Deployment & Runtime
Record known values or explicit unknowns for:
- Hosting provider and how frontend assets are served.
- Frontend/backend same-origin relationship and whether CORS is needed.
- Font/image/icon loading and fallback.
- Supported browsers and versions.
- Polyfills.
- Performance budgets/load-time targets.
Vercel was discussed but not selected; its Hobby plan must not be assumed appropriate for restaurant production. The existing visual specification mentions current Chrome/Edge/Firefox/Safari, but production browser support is not confirmed by the Vision.

## Constraints Summary
List the 5–7 most important constraints the architecture must respect, including:
- Supabase selected, while plan/account/products/APIs/policies remain undecided.
- Trusted server-side enforcement for order integrity, pickup timing/capacity, and abuse prevention.
- Pickup-only initial scope, no payment/Square/delivery/notifications/status lookup/AI.
- Private staff/admin access and separation from public menu access.
- Vercel not selected; production hosting, runtime, environment, and recovery remain open.
- Existing third-party assets and business listing details are references requiring production confirmation.
Add other evidence-grounded constraints from the approved Vision and Capabilities.

## Gaps and Unknowns
Summarize integration gaps between approved capabilities and confirmed backend/system reality. Do not invent APIs or workaround designs; identify missing decisions for the architecture phase.

Preserve the existing Integrations document’s valid decisions, including Supabase selection, deferred services, data flows, authentication uncertainty, hosting uncertainty, and operational gaps. Save the revised draft to `design/INTEGRATIONS.md` and present it for separate review. Approval of this prompt does not approve the generated document.
```

## Prompt 4: Threat Model

### Prompt 4 Original
- Approval: approved
- Current: no

```
Based on the approved `design/VISION.md`, `design/CAPABILITIES.md`, and `design/INTEGRATIONS.md`, create `design/THREAT_MODEL.md` for the Yunnan Tasty Garden website.

Keep it concise. Identify confirmed assets, actors, trust boundaries, plausible in-scope abuse cases, and architecture-relevant controls. Include only evidence-grounded risks; keep unknowns explicit. Do not choose a framework, security product, or implementation design.

**Confirmed context and threat surfaces**
- Customers submit pickup orders containing their name and phone, optional email/notes, order items/options, and pickup time. Orders are stored in Supabase and visible to authenticated staff.
- The menu, prices, spice choices, and add-ons are stored in Supabase and edited through a private admin interface.
- Customers access the public site; staff and admins need basic private login. The authentication mechanism and detailed authorization policies are undecided.
- The server must enforce scheduled-slot limits, pickup timing, and order-submission abuse controls. Do not impose a blanket one-order-per-IP-per-15-minutes rule.
- Vercel hosting is not selected. Supabase is selected, but its plan, account, and production backup policy are undecided. Supabase Free may pause after inactivity and does not include automatic backups, per the current pricing information; production recovery planning is still open.
- Google Fonts and Unsplash assets, a Google Maps directions link, and an Instagram placeholder appear in the existing preview. Their production use is unconfirmed.
- Online payments, delivery, Square POS, customer notifications/status lookup, and customer-facing AI are deferred.

Include:

**Assets:** customer contact/order data, menu/pricing/options integrity, order availability and pickup capacity, staff/admin credentials and privileges, and any confirmed external-service configuration. Name owner and impact if disclosed, altered, or unavailable; mark uncertain impact rather than inventing sensitivity.

**Actors and trust assumptions:** anonymous customers, authenticated staff/admins, automated abusive clients or other attackers, the trusted application/backend boundary, Supabase, and third-party asset providers only where applicable.

**Trust boundaries:** browser-to-backend/database, customer input to stored/rendered data, staff/admin authentication and authorization, and third-party assets to the browser if retained.

**In-scope abuse cases:** unauthorized order/customer-data access; forged or altered orders/prices/options; duplicate or abusive submissions; oversubscribing the 8-order scheduled slot limit; unauthorized menu edits or privilege escalation; injection through customer/admin-controlled content; credential or secret exposure; and service interruption or data loss affecting orders.

**Required controls:** map each in-scope case to a testable, architecture-level control. Consider least-privilege access, server-side validation and price verification, safe output rendering, protected secrets, duplicate prevention, abuse controls that don’t block users solely for sharing an IP, atomic enforcement of slot capacity, privacy-safe logs, and a verified backup/recovery plan before production. Do not claim any control is already implemented or select a particular product/API.

Add **Story and Tool Implications** with negative-test expectations, plus **Residual Risk** with rationale and owner where confirmed. Explicitly state that payment, delivery, Square, and the AI recommendation feature are deferred rather than implying their threat surfaces are assessed for launch.

If a missing fact is necessary, ask one focused question at a time. If details remain unknown, record the uncertainty and rationale; do not declare risk absent just because information is missing. Save the draft to `design/THREAT_MODEL.md` and present it for separate review; prompt approval does not approve the generated document.
```

### Prompt 4 Revision 1
- Approval: approved
- Current: yes

```
Based on the approved `design/VISION.md`, revised/approved `design/CAPABILITIES.md`, and revised/approved `design/INTEGRATIONS.md`, revise `design/THREAT_MODEL.md` for the Yunnan Tasty Garden website.

Before writing, reread this approved prompt and review:
- `design/VISION.md`, `design/CAPABILITIES.md`, and `design/INTEGRATIONS.md`.
- The existing `design/THREAT_MODEL.md`, preserving confirmed threat decisions unless an approved upstream document changes them.
- Do not invent identities, sensitivity, deployed controls, protocols, or service guarantees. Mark conditional risks (for example, cookie-based auth or remote third-party assets) as conditional.

Keep the model concise and use tables where helpful. Identify evidence-grounded assets, actors, trust boundaries, plausible abuse cases, architecture-required controls, story/test implications, and accepted residual risks. If a threat surface is uncertain, record the uncertainty rather than claiming risk is absent.

## Assets
List frontend-specific data, privileged functions, and critical properties. For each, name its owner and rate impact **low / medium / high** if disclosed, altered, or unavailable. Consider customer/session data, order/contact details, menu/pricing/options integrity, pre-submit form/cart input, credentials/tokens if any, client configuration, and third-party scripts/assets only where applicable. Preserve the existing asset assessments where still supported.

## Actors and Trust Assumptions
Address anonymous customers, authenticated staff/admins, abusive automated clients/attackers, third-party scripts/assets if retained, browser extensions, network attackers (including interception), and attackers with stolen tokens. Distinguish confirmed actors from plausible/conditional actors; do not imply a token, third-party script, or authentication method has already been selected.

## Trust Boundaries
For each relevant crossing, state what authenticates it and what remains untrusted on the receiving side:
- Browser → backend/Supabase (auth and server path are undecided; browser inputs/requests are untrusted).
- User input → application and stored/rendered data.
- Staff/admin identity/session → order and menu operations.
- Third-party scripts/assets → application data, only if used.
- Browser extensions → page/application state.
Do not assume an authentication mechanism or third-party script is present.

## In-Scope Abuse Cases
Tie attacker goals to confirmed capabilities/assets. Assess:
- Unauthorized customer/order-data access and privilege escalation.
- Forged/tampered order items, options, or prices; duplicate/abusive submission; scheduled-slot oversubscription.
- Unauthorized menu edits or staff-to-admin escalation.
- XSS through stored or submitted content; client-side injection/unsafe DOM handling.
- CSRF on state-changing operations if cookie/session authentication is selected.
- API token/secret exposure in browser storage, URLs, logs, developer console, or error messages.
- Sensitive customer/order data exposure through browser tools, console output, or errors.
- Third-party script/asset compromise if a direct dependency is retained.
- Service interruption, Supabase plan pause, or data loss affecting orders.
Mark applicability and unknowns; do not claim conditional mechanisms exist.

## Out-of-Scope Attacks
Explicitly list out-of-scope attack classes and a reason grounded in the project boundary. Do not treat lack of information as proof of no risk. Keep attacks affecting order availability, privacy, or integrity in scope unless there is a defensible exclusion.

## Required Controls
Map every in-scope case to a testable control that `design/ARCHITECTURE.md` must place in a component/boundary. Name the control type, not a preferred library/product. Include applicable controls for:
- Input validation and output encoding/safe rendering.
- Least-privilege access and staff/admin authorization.
- Server-side price/item validation and atomic scheduled-slot capacity.
- Duplicate/abuse protection without blocking customers solely for shared IP.
- Secret/token handling and avoiding sensitive data in logs, URLs, console, or errors.
- CSRF protection if cookie-based stateful authentication is selected.
- Restricting third-party script sources if any are retained.
- Privacy-safe observability and verified backup/recovery before production.
Do not claim these controls are implemented.

## Story and Tool Implications
Identify negative tests and security checks. The test infrastructure in Story 1 must be capable of supporting applicable XSS injection tests and token/secret leakage verification. The first story enabling each abuse case must include its negative test expectation. Include order tampering, duplicate attempts, shared-IP legitimate use, capacity races, unauthorized reads/writes, and safe rendering where applicable. Do not name a test framework/tool.

## Residual Risk
List each accepted or unresolved risk, its rationale, and owner where confirmed. Preserve the existing risks around basic staff/admin access, production recovery, and conditional third-party assets. Do not mark unresolved risks accepted or assign an unconfirmed owner.

## Cross-Check
Verify every high-impact asset has at least one control; every confirmed integration appears as an actor or trust boundary; and every control is specific enough to have a component home in Architecture. Do not include secrets or a generic STRIDE essay.

State explicitly that online payment, delivery, Square POS, customer notifications/status lookup, multiple staff roles, and customer-facing AI recommendations are deferred; their future threat surfaces require review before enablement.

Save the revised draft to `design/THREAT_MODEL.md` and present it for separate review. Approval of this prompt does not approve the generated document.
```

## Prompt 5: Architecture

### Prompt 5 Original
- Approval: approved
- Current: no

```
Based on the approved `design/VISION.md`, `design/CAPABILITIES.md`, `design/INTEGRATIONS.md`, and `design/THREAT_MODEL.md`, create `design/ARCHITECTURE.md` for the Yunnan Tasty Garden website.

Describe the simplest architecture that satisfies the approved capabilities, integration constraints, and threat controls. Keep it concise. Do not invent a framework, language, hosting provider, API contract, or Supabase service choice.

**Confirmed decisions and requirements**
- Supabase is the selected managed database/backend provider; the account, plan, authentication product, and specific Supabase APIs are undecided.
- The site supports a public customer menu/cart/checkout, a private staff order dashboard, and a separate private admin menu-management interface.
- Menu items, prices, dish-specific spice levels, and add-ons are stored in Supabase and maintained by admins.
- Customers submit pickup orders without online payment. A confirmation number is shown only after the order is successfully stored.
- Order submission must use a trusted server-side path to validate active menu items/options and trusted prices; enforce operating hours, minimum notice, scheduled-slot capacity (maximum 8), duplicate protection, and abuse controls. Do not rely on browser-only checks or block solely based on a shared IP.
- Staff need private login to view orders and update status; admins need authenticated menu-edit access. Authentication mechanism and exact authorization policies remain undecided.
- Square, payment, delivery, customer notifications/status lookup, and AI recommendations are deferred.
- Vercel was discussed but not selected. Production hosting, deployment region, Supabase plan, and backup/recovery plan remain open.

Include:

**Architecture decision:** conceptual application/backend structure and how Supabase fits, without prescribing an unconfirmed technology stack.

**Responsibilities and data flow:** customer menu read, cart/checkout, trusted order submission and persistence, confirmation-number response, staff order viewing/status updates, and admin menu editing.

**Security/control placement:** private data access and authorization, trusted price/item validation, atomic slot-capacity enforcement, duplicate/abuse protection, safe rendering of stored content, secrets protection, and backup/recovery ownership. Map each required threat-model control to a component or boundary.

**Interfaces and dependencies:** state what is confirmed, and mark specific endpoints, Supabase Auth/RLS details, server-side execution mechanism, hosting, and environment configuration as undecided where not approved.

**Key decisions and gaps:** explicitly surface choices needed before implementation, including authentication, trusted server-side mechanism, exact Supabase plan and backups, hosting, pickup cutoff/ASAP capacity, and operational menu data.

Keep the deferred AI model and other deferred integrations out of the initial architecture except for noting their deferred status. Use the approved threat model; do not claim any control is already implemented. Save the draft to `design/ARCHITECTURE.md` and present it for separate review; prompt approval does not approve the generated document.
```

### Prompt 5 Revision 1
- Approval: approved
- Current: no

```
Based on the approved `design/CAPABILITIES.md`, `design/INTEGRATIONS.md`, and `design/THREAT_MODEL.md`, revise `design/ARCHITECTURE.md` for the Yunnan Tasty Garden website.

Keep the architecture to approximately one page by being concise, but retain every section and cross-check listed below. Describe the simplest architecture that meets the approved requirements. Do not invent or select an unapproved framework, language, hosting provider, API contract, authentication product, or Supabase service.

**Confirmed context**
- Supabase is the selected managed database/backend provider. The account, plan, authentication product, exact APIs, and data-access policies are undecided.
- The site has a public customer ordering experience, a private staff order dashboard, and a separate private admin menu-management interface.
- Customers order pickup without online payment. A confirmation number is shown only after successful persistence.
- A trusted server-side path must validate active items/options and authoritative prices; enforce operating hours, minimum notice, scheduled-slot capacity (8 orders maximum), duplicate prevention, and abuse controls. Browser-only enforcement is insufficient; users must not be blocked solely for sharing an IP.
- Staff require private login to view orders and update status; admins require authorized menu-edit access.
- Vercel was discussed but not selected. Production hosting, deployment region, Supabase plan, backup/recovery plan, and authentication approach remain undecided.
- Payment, delivery, Square POS, customer notifications/status lookup, detailed staff roles, and customer-facing AI recommendations are deferred.

Include these sections and retain their intended substance from the frontend architecture template:

**1. Architecture decision and technology constraints**
- State the conceptual application/backend structure and Supabase’s role.
- List technology categories only where useful (framework/runtime, routing, state, styling, forms/validation, testing/build); mark each as undecided unless confirmed.
- Give concise rationale for confirmed non-obvious choices. Do not invent considered-and-rejected technologies.

**2. Application structure**
- Identify the customer, staff, and admin pages/areas, their responsibilities, and data needs.
- Describe shared component groups (layout, data display, input, feedback, navigation) and note controlled/uncontrolled input choices only if established; otherwise mark undecided.
- Describe the API-client boundary and the required conceptual operations, without inventing endpoint names or contracts.
- Describe data-fetching/query and mutation responsibilities, cache behavior, and freshness choices; mark specific hooks, keys, and timing policies undecided.
- Identify domain, request/response, form, and component types needed conceptually; leave exact schemas/contracts for implementation design.

**3. Dependency flow**
- Show the conceptual direction between pages, shared components, data-fetching/state responsibilities, API/backend boundary, Supabase, and styling.
- Keep privileged order processing and authorization on a trusted server-side path; do not imply the browser talks directly to privileged interfaces.

**4. Key design decisions**
Address component composition; form state and validation timing; filtering/sorting responsibility; error/failure handling and boundary placement; authentication token/session storage and injection; dialog/modal state; and file upload only as “not applicable/none confirmed” unless evidence says otherwise.
- Preserve undecided choices rather than silently selecting them.

**5. Security/control placement**
Map each approved threat-model control to its conceptual component or trust boundary: least-privilege private data access; staff/admin authorization; server-side item/option/price validation; atomic slot capacity; duplicate and abuse controls; safe rendering of untrusted content; protected secrets; privacy-safe logging; and backup/recovery responsibility.
- Include testable negative-case expectations, without claiming controls are implemented or prescribing a product/API.

**6. File-structure view**
- Provide a concise conceptual structure for pages, shared components, data/API boundary, state/data-fetching, types, and general utilities.
- Do not present speculative filenames or a framework-specific directory structure as a decision.

**7. Data flow and open decisions**
- Cover menu reads, cart/checkout, trusted order validation and persistence, confirmation after persistence, staff order viewing/status changes, and admin menu editing.
- Keep the order-time menu snapshot recommendation visibly unresolved.
- Explicitly list open decisions: Supabase account/plan/auth/APIs/policies, trusted server-side execution mechanism, hosting/region/environment configuration, backups and recovery ownership, final scheduled cutoff, ASAP capacity, timezone, verified menu data, and order snapshot behavior.

**8. Cross-check**
- Map every approved capability to a page or component responsibility.
- Map every confirmed backend operation to a conceptual API-client/data-access responsibility without fabricating endpoint contracts.
- Confirm integration constraints and threat controls have an architecture home; list gaps explicitly.

Keep deferred features out of the initial architecture except for noting their deferred status. Save the revised draft to `design/ARCHITECTURE.md` and present it for separate review. Approval of this prompt does not approve the revised document.
```

### Prompt 5 Revision 2
- Approval: approved
- Current: no

```
Based on the approved `design/CAPABILITIES.md`, `design/INTEGRATIONS.md`, and revised/approved `design/THREAT_MODEL.md`, revise `design/ARCHITECTURE.md` for the Yunnan Tasty Garden website.

Before writing, reread this approved prompt first, then read the existing `design/ARCHITECTURE.md`. The existing Architecture is a revised draft pending review, not an approved authority; preserve its useful decisions only where they remain consistent with the approved upstream documents. Also review the approved Capabilities, Integrations, and Threat Model. Do not omit applicable template steps; mark unconfirmed choices as undecided rather than inventing them.

Describe the simplest module structure and interfaces satisfying the approved capabilities and integration constraints. Keep the result concise and approximately one page, while retaining all sections and cross-checks below. Do not select an unapproved framework, language, hosting provider, API contract, authentication product, package, or Supabase service.

## Tech Stack (from INTEGRATIONS.md constraints)
- Address framework/version; routing; server state; styling; forms; validation; testing; and build tool.
- Give a one-line rationale for each confirmed non-obvious choice.
- State what alternatives were considered/rejected only if actually established; otherwise say none were confirmed.
- Supabase is selected as managed backend/database provider. Account, plan, products/APIs, auth, runtime, and hosting are undecided.

## Application Structure

### Pages (one per route/area)
For customer ordering, staff order management, and admin menu management, state conceptual route/area, responsibility, and data needs. Do not invent route paths; mark them undecided.

### Shared Components
Group responsibilities under Layout, Data Display, Input, Feedback, and Navigation. Keep the proposed structure flat. State controlled/uncontrolled decisions only if established; otherwise mark undecided.

### API Client Layer
Describe one conceptual client/data-access operation per confirmed backend endpoint. No endpoint paths or request/response contracts are confirmed; list conceptual operations and clearly identify missing contracts without fabricating method/path/schema.

### Data Fetching Hooks / Responsibilities
Identify conceptual queries and mutations for menu reads, order submission, staff order/status operations, and admin menu operations. Mark hook names, cache keys, and stale-time/freshness policy undecided unless confirmed.

### TypeScript / Domain Types
Identify conceptual domain models, request/response, component props, and form types. Exact schemas and whether TypeScript is used remain undecided.

## Dependency Flow
Show the conceptual direction `Pages → Components → Data Fetching/State → API Client → Backend`, with styling supporting components. Include the trusted server-side order-processing/authorization boundary between browser-originated requests and privileged persistence. Do not imply direct browser access to privileged Supabase operations.

## Key Design Decisions
Address each template topic, preserving uncertainty where not approved:
- Component composition strategy.
- Form-state management (controlled/uncontrolled) and validation timing.
- File upload handling, if needed; otherwise state none is required/confirmed.
- Client-side filtering/sorting only where backend does not provide it; current backend behavior is unknown.
- Error-boundary placement and failure behavior.
- Token/auth storage and injection; auth method and session storage are undecided, and privileged secrets must not be exposed to the browser.
- Modal/dialog management (URL-based vs state-based); undecided unless confirmed.

## File Structure
Provide a concise conceptual structure corresponding to pages, components, API client, data-fetching/state, types, and utilities. Do not present speculative filenames or a framework-specific source tree as a decision.

## Security and Control Placement
Give every approved Threat Model control a component or boundary home, including least-privilege private reads/writes; staff/admin authorization; server-side item/option/price validation; atomic scheduled-slot capacity; duplicate/abuse controls that do not block solely by shared IP; safe rendering; protected secrets and privacy-safe logs/errors; conditional CSRF defenses if cookie sessions are selected; third-party script boundaries if introduced; secure production transport; and backup/recovery ownership.
For each, include concise negative-test expectations. Do not claim controls are already implemented or select a product/library.

## Data Flow and Key Gaps
Cover active menu reads, cart/checkout, trusted validation and persistence, confirmation only after success, staff viewing/status updates, and admin menu editing. Preserve scheduled pickup rules (15-minute slots, 30 minutes’ notice, maximum 8 per slot, daily 11:00 a.m.–9:30 p.m.) and unresolved final cutoff, ASAP capacity, and timezone.
List gaps: Supabase account/plan/products/APIs/policies/auth; trusted server-side mechanism; hosting/region/environment; backup and recovery; order-time item/price/options snapshots; verified menu data; browser support/accessibility details; and any missing API contracts.

## Cross-Check
- Map every approved capability to a page or component responsibility.
- Map every confirmed endpoint to an API client function; where none are documented, map conceptual operations and flag the absent contracts.
- Confirm every integration constraint is honored.
- Confirm every threat control has a component/boundary home.
- Flag gaps and contradictions rather than silently resolving them.

Keep deferred online payment, delivery, Square POS, customer notifications/status lookup, multiple staff roles, and AI recommendations out of the initial architecture except to note their deferred status. Save the revised draft to `design/ARCHITECTURE.md` and present it for separate review; prompt approval does not approve the generated document.
```

### Prompt 5 Revision 3
- Approval: approved
- Current: yes

```text
Revise `design/ARCHITECTURE.md` using the approved vision, capabilities, integrations, and threat model. Preserve the existing architecture and unresolved technology choices. Explicitly map the approved frontend design system to shared UI responsibilities, and identify the operational boundary responsible for monitoring production service state. Keep the monitoring owner, method, provider, and configuration undecided unless already approved. Do not claim monitoring is implemented. Preserve all other approved scope and controls. Present the revised document for separate review.
```

## Prompt 6: Ordered stories

### Prompt 6 Original
- Approval: approved
- Current: no

```
Based on the approved `design/VISION.md`, `design/CAPABILITIES.md`, `design/INTEGRATIONS.md`, `design/THREAT_MODEL.md`, and `design/ARCHITECTURE.md`, create `design/STORIES.md` for the Yunnan Tasty Garden website.

Decompose the approved initial-release architecture into ordered, independently verifiable stories. Keep dependencies forward-consistent and explicit. Do not add scope or choose unapproved tools, frameworks, hosting, APIs, authentication products, database schema, or test infrastructure.

**Requirements to cover**
- Establish an appropriate, tool-neutral test/verification foundation early; do not name a test framework or CI tool.
- Use Supabase as the selected backend/database provider while leaving its plan, auth product, exact APIs, and trusted server-side execution mechanism undecided unless the owner confirms them.
- Implement the customer pickup flow: full active menu, applicable item-specific options, cart, required name/phone, optional email/notes, ASAP or scheduled pickup, order persistence, and confirmation number only after successful persistence.
- Enforce scheduled pickup hours, 15-minute slots, 30-minute minimum notice, maximum 8 orders per slot, duplicate prevention, and server-side abuse protection. Do not rely on browser-only checks or block users solely because they share an IP.
- Implement private staff login/order viewing/status updates and a separate admin interface for menu items, prices, spice levels, and add-ons.
- Include security controls and negative-test expectations from the approved threat model in the first story that enables each relevant behavior.
- Online payment, delivery, Square POS, customer notifications/status lookup, detailed staff roles, and customer-facing AI recommendations are deferred. Do not create implementation stories for deferred features in this initial plan.

Identify a **walking-skeleton checkpoint** that proves a customer order is submitted, stored, acknowledged, and visible to staff. Include the admin menu-management capability in the initial plan; if the skeleton depends on seed data or another temporary arrangement, make that dependency explicit and do not treat sample preview content as verified menu data.

For each story include:
- **Title**
- **Depends on** (or `none`)
- **Enables**
- **Builds**
- **Acceptance Criteria**: concrete, user/project-verifiable outcomes and relevant negative cases
- **Complexity**: relative S/M/L only, with no time estimate

Add a checkpoint immediately after the walking skeleton, with manual verification scenarios, architecture/security review questions, and unresolved decisions to review. Keep checkpoints out of the story dependency graph. Every dependency must have a matching `Enables` relationship; every initial-scope capability and architecture component must map to at least one story.

Preserve open decisions instead of resolving them in the story plan: verified menu/options data, ASAP capacity and final pickup cutoff, Supabase plan/auth/policies, hosting, backup/recovery, and whether to persist order-time menu snapshots. Do not impose branches, merges, specific test tools, CI, or release tags.

Save the draft to `design/STORIES.md` and present it for separate review; approval of this prompt does not approve the generated story plan.
```

### Prompt 6 Revision 1
- Approval: approved
- Current: no

```
Based on the approved `design/VISION.md`, `design/CAPABILITIES.md`, `design/INTEGRATIONS.md`, `design/THREAT_MODEL.md`, and newly approved `design/ARCHITECTURE.md`, revise `design/STORIES.md` for Yunnan Tasty Garden.

Before writing, reread this approved prompt first, then read the existing `design/STORIES.md`. The current Stories document is a revised draft pending review, not an approved authority; preserve useful decisions only where consistent with approved upstream documents. Also review all approved inputs listed above. Do not invent tools, frameworks, hosting, endpoints, authentication products, schemas, test infrastructure products, CI, branches, merges, or release tags.

Decompose the approved architecture into ordered, independently verifiable stories. The first stories must compose into a thin end-to-end walking skeleton. Every story must build one coherent increment, identify what it depends on, what it enables, what it builds, concrete acceptance criteria, and relative complexity.

## Story Format
For every story, include:
- **Title**
- **Depends on**: earlier stories that must be complete, or `none`
- **Enables**: stories unblocked by this story
- **Builds**: relevant pages/areas, shared UI, data/API responsibilities, or test foundation from the approved Architecture
- **Acceptance Criteria**: specific, verifiable user/project outcomes and applicable unit/integration/security negative-test expectations
- **Complexity**: relative S/M/L only; no time estimate

## Sequencing Rules
- No story may depend on a later-numbered story; every `Depends on` relationship must be reciprocated by the prerequisite’s `Enables`.
- **Story 1 must be Test Infrastructure.** Establish a tool-neutral foundation that lets every subsequent story add unit and integration tests alongside its implementation. It must support tests around backend boundaries, mocked/test-double responses for confirmed conceptual operations (without inventing endpoints), negative XSS/rendering cases, and token/secret leakage checks. Include global test setup, a clear test organization, and coverage capability as concepts, but do not select a framework, libraries, file paths, or CI.
- The next early stories should form the walking skeleton: a runnable basic application shell, followed by customer-visible backend data display, then order submission/persistence/confirmation and staff visibility/status management as needed to exercise all required layers. Adapt the generic template’s sample sequence to this project's full pickup-order skeleton; do not force unconfirmed tools or a shorter slice that fails to reach staff.
- Add later capabilities one at a time. Include admin menu management in this initial plan.
- The first story enabling each Threat Model abuse case must include its negative-test expectation; do not defer these to cleanup.
- Preserve existing approved ordering decisions where consistent, especially Story 1 testing infrastructure and the customer→staff walking skeleton.

## Project Requirements to Cover
- Supabase is selected for persistent menu/order data; its account/plan/products/APIs/auth/policies and trusted server-side execution mechanism remain undecided.
- Implement active full-menu browsing and item-specific options, cart editing, required name/phone, optional email/notes, ASAP/scheduled pickup, order persistence, and confirmation only after successful storage.
- Enforce scheduled 15-minute slots, at least 30 minutes’ notice, maximum 8 orders per slot, daily 11:00 a.m.–9:30 p.m. hours, duplicate/abuse protections, and trusted server-side validation. Do not rely on browser-only enforcement or block solely because customers share an IP. Keep final cutoff and ASAP capacity unresolved.
- Include private staff login/order viewing/status changes and separate private admin menu editing for items, prices, availability, spice choices, and add-ons.
- Include threat controls and negative tests at the first story enabling each behavior: authorization/privacy; item/option/price tampering; duplicate and abuse behavior; shared-IP legitimate customer; concurrent slot-capacity races; XSS/safe rendering; secret/token/log/error exposure; conditional CSRF if cookie sessions are chosen; conditional third-party scripts; secure transport; and backup/recovery readiness.
- Deferred: online payment, delivery, Square POS, customer notifications/status lookup, multiple staff roles, and customer-facing AI recommendations. Do not add implementation stories for deferred items.
- Use verified test menu data or explicitly identify a temporary test-data prerequisite; never treat preview sample dishes/prices as verified.

## Walking-Skeleton Checkpoint
Insert the first checkpoint immediately after the story sequence that proves customer order submission, storage, confirmation, and staff visibility/status management. Keep the checkpoint outside the story dependency graph.

Include:
- Manual browser verification scenarios for customer menu, cart, checkout, order persistence/confirmation, and staff view/status update.
- Architecture review of component boundaries, dependency flow, and conceptual API/data contracts.
- Security review questions and negative scenarios from the Threat Model.
- A decision point for learnings and unresolved items (menu data, pickup cutoff/ASAP capacity, auth/policies, hosting, backup/recovery, and order snapshots).
- A full test-suite check and running the application using whatever project-established procedure exists; do not invent commands or tools.
- Stop for developer review before later stories.

Add later human checkpoints after every 3–5 stories where useful; keep checkpoints out of story dependencies.

## Cross-Check
- Every page/area and capability in approved `CAPABILITIES.md` is covered by one or more stories.
- Every conceptual component/data/API responsibility in approved `ARCHITECTURE.md` is built by one or more stories.
- Every integration constraint and Threat Model control is reflected in a story/checkpoint.
- Flag gaps; do not alter approved scope to hide them.

Start with a table of contents linking every story and checkpoint. Preserve unresolved decisions: verified menu/options, final cutoff, ASAP capacity, Supabase plan/auth/policies, hosting, backup/recovery, and order-time menu snapshots. Save the revised draft to `design/STORIES.md` and present it for separate review; prompt approval does not approve the generated story plan.
```

### Prompt 6 Revision 2
- Approval: approved
- Current: yes

```text
Revise `design/STORIES.md` using the approved capabilities, threat model, and revised architecture. Make Story 7 depend on Stories 3 and 4, and update Story 4’s `Enables` accordingly. Add verifiable acceptance coverage for the approved frontend design system to Story 2, preserving unspecified values and asset choices as undecided. Add service-state monitoring readiness to the Story 6 checkpoint without choosing a monitoring owner, method, provider, or configuration. Update the coverage cross-check as needed. Preserve the existing stories, checkpoint timing, scope, and other dependencies. Present the revised document for separate review.
```

## Prompt 7: Critical path and waves

### Prompt 7 Original
- Approval: approved
- Current: no

```
Read the approved `design/STORIES.md` and produce `design/CRITICAL_PATH.md` for Yunnan Tasty Garden. Use STORIES.md as the sole source for story scope and dependency edges. Do not propose new stories, change scope, or modify STORIES.md.

Extract the graph from each story’s `Depends on` and `Enables` fields. Treat checkpoints as review gates, not stories or graph nodes. Surface any dependency not reciprocated by the matching `Enables` relationship as a graph issue; do not silently repair it.

## Dependency Graph
Provide a compact text diagram with one `Story → Story` edge per dependency. List graph inconsistencies if present.

## Critical Path
Identify the longest dependency chain, not the fastest or easiest chain. List it end-to-end in order, with each story’s approved S/M/L complexity and a cumulative complexity expression. Do not invent hours or a complexity-to-time conversion. If multiple paths tie or S/M/L values do not support an unambiguous weighted comparison, report the tie/uncertainty and the structural longest path(s).

Use a table:

| Order | Story | Complexity | Cumulative |
|---|---|---|---|
| 1 | Story N — title | S/M/L | symbolic sum |

## Parallel Waves
Group every story into ordered waves. Stories in one wave must have all prerequisites satisfied by earlier waves and must be sufficiently independent to proceed without conflicting shared-write work. Every story must appear in exactly one wave.

- Keep the walking-skeleton checkpoint and any other checkpoints out of the waves.
- Respect any stop-for-review gate in STORIES.md when describing when a later wave may begin.
- Include a wave-entry rule based on prerequisites and prior-wave completion, without imposing unconfirmed tracker status tokens or project tooling.

## Notes on Shape
Identify likely shared-write areas from story `Builds` descriptions that should be serialized, pure additions safer to parallelize, work that depends on/refactors earlier outputs, and unclear boundaries that prevent asserting safe parallelism. Do not claim parallel safety where the plan does not establish it.

## Rules and Cross-Check
- Every story in STORIES.md appears exactly once in the waves.
- Each wave’s prerequisites are satisfied by earlier waves.
- The critical path is a longest chain from the declared dependency graph; explain checkpoint gates without adding them to the graph.
- Surface graph mismatches, ties, and plan limitations as findings.
- Do not propose or make changes to STORIES.md.

Save the draft to `design/CRITICAL_PATH.md` and present it for separate review. Approval of this prompt does not approve the generated critical-path document.
```

### Prompt 7 Revision 1
- Approval: approved
- Current: no

```
Based on the approved `design/STORIES.md`, revise `design/CRITICAL_PATH.md` for Yunnan Tasty Garden.

Before writing, reread this approved prompt first, then read the existing `design/CRITICAL_PATH.md`. Also review the approved `design/STORIES.md` as the sole source of story scope and declared dependency edges. Treat the existing Critical Path as an approved document whose decisions remain in force unless they conflict with the story plan or this prompt. Do not change `design/STORIES.md` or add, remove, or rescope stories.

Treat each story's `Depends on` field as the source of incoming edges and validate it against the matching prerequisite `Enables` field. Show each edge once. Report any nonreciprocal or malformed dependency as a graph issue; do not silently repair it. Checkpoints are review gates, not stories or graph nodes.

## Dependency Graph
Provide a compact text diagram with one `Story → Story` line per dependency and concise notes on any graph inconsistencies.

## Critical Path
Identify the longest dependency chain in the declared graph—not the fastest/easiest path. List it end-to-end in a table with order, exact story number/title, approved S/M/L complexity, and cumulative symbolic complexity. Do not convert S/M/L to hours or assign numerical weights. If the ordinal labels do not establish a unique weighted longest path, state that limitation and give the structurally longest path(s). Explain any checkpoint that gates execution without turning it into a graph edge.

| Order | Story | Complexity | Cumulative |
|---|---|---|---|
| 1 | Story N — exact title | S/M/L | symbolic sum |

## Parallel Waves
Group every story into ordered waves. A story may enter a wave only after all its declared prerequisites are complete in earlier waves. Stories grouped in the same wave must be independent enough to run concurrently without conflicting shared writes; where the approved plan lacks file/module boundaries, say that parallel safety cannot be established rather than asserting it.

- Place every story in exactly one wave.
- Keep all checkpoints outside the graph and waves.
- Respect review gates stated in `design/STORIES.md`; specifically, the walking-skeleton checkpoint after Story 6 must be passed before Story 7 begins, even though its graph prerequisite is earlier.
- State the wave-entry rule: all prerequisite stories in earlier waves must be complete, and do not start a later wave until the prior wave is complete. Do not impose unconfirmed tools or status tokens.

## Notes on Shape
Identify, from each story's `Builds` description, likely shared-write areas to serialize, pure additions that may be safer to parallelize, work that depends on or refactors earlier outputs, and unclear boundaries that limit safe-parallelism claims.

## Cross-Check and Findings
- Every story appears in exactly one wave.
- Every wave's prerequisites are satisfied by earlier waves.
- The structurally longest critical path includes at least one story in every wave; if the graph or review gate makes this impossible, explain why.
- Dependency and `Enables` declarations agree, or mismatches are surfaced.
- Checkpoint rows are excluded from the graph and waves, and review gates are honored.
- Report bad paths, ties/weighting ambiguity, graph mismatches, and plan limitations as evidence-based findings at the end.
- Do not modify or propose edits to `design/STORIES.md`.

Save the revised draft to `design/CRITICAL_PATH.md` and present it for separate review. Approval of this prompt does not approve the regenerated Critical Path.
```

### Prompt 7 Revision 2
- Approval: approved
- Current: yes

```text
Revise `design/CRITICAL_PATH.md` using the approved `design/STORIES.md` as the sole source of story dependencies. Recalculate the graph, reciprocal `Enables` relationships, structurally longest path, and waves, including the new Story 4 → Story 7 dependency. Preserve the checkpoint after Story 6 as a review gate, not a graph edge. Do not infer durations from complexity labels or change story scope. Present the revised document for separate review.
```

## Prompt 8: Project progress tracker

### Prompt 8 Original
- Approval: approved
- Current: no

```
Create `design/PROGRESS.md` from the approved `design/STORIES.md` for the Yunnan Tasty Garden project. This is a progress tracker, separate from the stable story plan. Do not change `design/STORIES.md`.

Use a Markdown pipe table with columns `#`, `Title`, and `Status`. Include every story exactly once, using its exact story number and title from STORIES.md. Initialize every story’s status to `todo`. The only allowed status values are `todo`, `in_progress`, `in_review`, `done`, and `blocked`; keep each Status cell to exactly one value.

Include the walking-skeleton checkpoint after Story 6 as a clearly labeled non-story row, without assigning it a story number or status. Do not include deferred scope as stories.

Add a concise rolling-status section reflecting the initial state: 0 of 7 stories complete; current phase is Test Infrastructure; next is Story 1; no stories are blocked; no checkpoint approval has occurred.

Save the tracker to `design/PROGRESS.md`. Report the created file and present it for separate review. Prompt approval does not approve the generated tracker.
```

### Prompt 8 Revision 1
- Approval: approved
- Current: yes

```
Based on approved `design/STORIES.md`, revise `design/PROGRESS.md` for Yunnan Tasty Garden. The tracker is separate from the authoritative story plan; do not modify Stories.

Before writing, reread this approved saved prompt first, then read the existing `design/PROGRESS.md`, followed by approved `design/STORIES.md`. Preserve all recorded story statuses, branch/merge information if present, notes, checkpoint decisions, and other actual progress; never reset existing work or invent status. Flag discrepancies between the tracker and Stories rather than silently altering scope or discarding recorded work.

## Tracker format
- Keep the developer-confirmed location `design/PROGRESS.md`.
- Use Markdown pipe tables with `#`, `Title`, and `Status` columns, grouped by appropriate project phases using level-3 headings. Include each approved story exactly once with its exact number and title. Include branch/merge columns only if already present or separately approved; preserve any recorded branch/merge data.
- Each story's Status cell contains exactly one approved token: `todo`, `in_progress`, `in_review`, `done`, or `blocked`. Put details in a separate Notes column or notes section, never in the Status cell.
- Initialize only genuinely new, unstarted story rows to `todo` when supported by recorded state; if actual status is unclear, flag it instead of guessing.
- Include the approved walking-skeleton checkpoint after Story 6 as a clearly labeled non-story row, with `—` in number and status columns; do not include deferred features as story rows.
- Avoid checkbox-list story tracking and ambiguous numbered story-like bullets in prose. This is a clear Markdown convention, not a claim that a particular parser or tool is configured.

## Rolling Status
Derive completed count, current phase, next eligible story, blocked stories, and last checkpoint approval from recorded tracker state and the approved story plan; identify unknowns or conflicts rather than inventing them. Preserve the Story 6 review gate before Story 7.

## Notes on Plan Revisions
Include a section for future story-plan changes with a concise rationale and actual date when known; preserve existing notes and never invent a date or revision.

Cross-check exact story coverage, valid status tokens, checkpoint placement, and rolling-status consistency. Report any unresolved discrepancies. Save the revised tracker to `design/PROGRESS.md` and present it for separate review; approving this prompt does not approve the generated tracker.
```

## Prompt 9: AI productivity metrics

### Prompt 9 Original
- Approval: approved
- Current: no

```
Create `design/AI_METRICS.md` for the Yunnan Tasty Garden project, derived from approved `design/STORIES.md`. This metrics record is separate from the story plan. Do not change `design/STORIES.md`, the progress tracker, or other project files.

Use these per-story measures:
- `est_human_hours`: an independent, framework-neutral estimate for a mid-to-senior engineer to implement the approved story, add its tests, and perform local verification. Exclude design, meetings, and review. Base estimates on approved story scope; do not impose fixed hour anchors. Record estimates before work starts and never revise them retroactively; explain variance in notes.
- `ai_wall_hours`: actual active elapsed work time for the story, excluding intervals paused while waiting on the user or an external decision.
- `leverage`: `est_human_hours / ai_wall_hours`; do not compute when either value is unavailable or the denominator is zero.
- Record notes, model identity, and provider-reported token usage when available. Never infer or fabricate usage; mark unavailable counts explicitly.

Define per-story timestamp events for start, pause, resume, and completion in committed JSONL logs under the existing `.ai-metrics/` directory. Record timestamps consistently and preserve provider-specific token categories. Do not create raw story logs or invent story execution data now.

The record must include a table ready for the seven approved stories, an initial rolling summary with zero completed stories and no invented usage, and a concise explanation of fields and timekeeping. Do not select a test framework, runtime, implementation quality gate, branch convention, or provider-specific API. Do not modify `.gitignore`; raw logs are intended to be committed.

Save the metrics record to `design/AI_METRICS.md`. Report the created file and present it for separate review; approval of this prompt does not approve the generated metrics record.
```

### Prompt 9 Revision 1
- Approval: approved
- Current: yes

```
Based on approved `design/STORIES.md`, revise `design/AI_METRICS.md` for Yunnan Tasty Garden. Keep the metrics record separate from the authoritative story plan; do not modify Stories, the progress tracker, raw logs, `.gitignore`, or other project files.

Before writing, reread this approved saved prompt first, then read the existing `design/AI_METRICS.md`, and review approved `design/STORIES.md` and any existing per-story raw logs under `.ai-metrics/`. Preserve the approved metrics contract, all recorded estimates, actuals, timestamps, usage, notes, and prior decisions; never reset or retroactively revise them. If recorded information is missing or conflicts with the story plan, flag it without inventing data.

## Measures and estimate methodology
- Explain `est_human_hours`: an independent framework-neutral estimate, made before story work, for a mid-to-senior engineer implementing the approved scope, tests, and local verification; exclude design, meetings, and review. Assess scope, component/data integration complexity, novelty, and debugging as applicable without selecting a stack or imposing fixed hour anchors. Do not change a recorded estimate; explain variance in notes.
- Explain `ai_wall_hours` as actual active elapsed story work time including retries and revisions, excluding documented pauses while waiting for the user or an external decision. Explain `leverage = est_human_hours / ai_wall_hours`, its interpretation, and that it is unavailable if an input is missing or the denominator is zero.
- Describe model identity, provider-reported input/output/cache/other/total token categories and notes. Use actual reported data only; mark unavailable counts `null`, preserve provider-specific categories, and never infer usage.

## Timekeeping and quality gates
- Preserve the existing story start, pause, resume, completion, UTC timestamp, and decimal-hours conventions. Completion requires the approved acceptance criteria and project-confirmed applicable checks; do not impose unapproved branch conventions, frameworks, commands, or quality gates. Where a check or time record is missing, mark it unknown rather than claiming it passed or inventing a timestamp.
- Preserve the committed `.ai-metrics/story-{n}.jsonl` per-story log convention and example event shapes for start, pause, resume, completion, and provider-reported usage. Keep separate usage records per model response when available; retain provider/model identity and provider-specific categories. Explain how active intervals exclude documented pauses. Do not create logs or fabricate events.

## Per-story record and rolling summary
- Retain one row per approved story with exact number/title, model(s), token categories, human estimate, AI active hours, leverage, and notes. Preserve existing values and flag discrepancies; do not infer status or execution data.
- Describe updating the rolling summary after completed stories: count, total human estimates, total AI active hours, overall leverage, token totals by type and usage by model, and highest/lowest leverage where valid data exists. Preserve recorded data and distinguish unavailable/partial data from zero.

Cross-check the existing story rows and logs against approved Stories and the confirmed contract. Report gaps and inconsistencies without modifying other files. Save the revised `design/AI_METRICS.md` and present it for separate review; approving this prompt does not approve the regenerated document.
```

## Prompt 10: Consistency audit

### Prompt 10 Original
- Approval: approved
- Current: no

```
Read these approved Yunnan Tasty Garden design and tracking documents:
- `design/VISION.md`
- `design/CAPABILITIES.md`
- `design/INTEGRATIONS.md`
- `design/THREAT_MODEL.md`
- `design/ARCHITECTURE.md`
- `design/STORIES.md`
- `design/CRITICAL_PATH.md`
- `design/PROGRESS.md`
- `design/AI_METRICS.md`
- `.ai-metrics/FILE_DEPENDENCIES.md`
- `.ai-metrics/workflow-checkpoint.md` for recorded approval/output states and confirmed project decisions

Perform a findings-only consistency audit and save a concise report to `design/CONSISTENCY_AUDIT.md`. Do not edit the audited documents or act on findings. Do not present findings for substantive review yet; that review is deferred until the separately prepared Prompts 11–13 have been executed and their applicable output reviews are complete.

Record the exact input paths and their approval/state reviewed. Treat unknowns and deferred decisions as intentional when the approved documents say so; do not convert them into implementation decisions or report them as defects merely because they remain undecided.

Check:
1. **Vision → Capabilities:** capabilities serve named users and success outcomes; no scope contradicts Vision’s non-goals.
2. **Capabilities → Integrations:** confirmed integrations support capabilities; unresolved API/provider details remain explicit.
3. **Capabilities/Integrations → Threat Model:** relevant assets, actors, boundaries, abuse cases, and controls reflect the approved product and data flows.
4. **Capabilities/Integrations/Threat controls → Architecture:** every capability has a page/component responsibility; confirmed integration constraints are honored; each required threat control has a component or boundary home.
5. **Architecture/Threat Model → Stories:** architecture responsibilities are built by stories; dependencies are forward-consistent; Story 1 is test infrastructure; the customer-to-staff pickup flow and checkpoint after Story 6 match the approved project plan; security negative tests appear with the stories that first enable the relevant behavior.
6. **Capabilities → Stories:** each capability is covered; checkpoint placement matches the approved story plan.
7. **Stories → Critical Path:** every story appears in exactly one wave; each wave’s prerequisites are in earlier waves; graph edges and reciprocal `Depends on`/`Enables` declarations agree; the critical path is structurally longest; checkpoints are excluded from the graph and waves, with the Story 6 review gate respected.
8. **Stories → Progress:** `design/PROGRESS.md` (the developer-confirmed location) lists each story exactly once with its exact title; each starts at one approved status token; the checkpoint is a non-story row; rolling status agrees with the initial plan.
9. **Stories → AI Metrics:** `design/AI_METRICS.md` (the developer-confirmed location) covers all seven stories and agrees with the approved measurement contract. Do not require unapproved tools, runtime-specific quality gates, or unavailable provider-usage data.
10. **Non-goals:** no approved capability, threat model, architecture, story, critical-path item, progress row, or metric requirement silently adds deferred payment, delivery, Square POS, customer notifications/status lookup, multiple staff roles, or customer-facing AI recommendations.

An unmapped high-impact asset, a required threat control with no architecture home, or an orphan approved capability is a failure finding. Report only evidence-based findings, with source path/section and a concise explanation. If a check passes, state that briefly; do not propose fixes or edit any file.
```

### Prompt 10 Revision 1
- Approval: approved
- Current: no

```
Perform a findings-only consistency audit for Yunnan Tasty Garden and save it to `design/CONSISTENCY_AUDIT.md`.

Before writing, reread this approved saved prompt first, then the existing `design/CONSISTENCY_AUDIT.md`. Preserve prior finding identifiers, evidence, and recorded decisions; do not treat unreviewed findings as approved or resolved. Reread the actual current inputs listed below and record their exact paths and approval states. Record verifiable input revisions or content identifiers for later comparison; if unavailable, record sufficient reviewed state for manual comparison or mark it unverifiable.

Inputs: `design/VISION.md`, `design/CAPABILITIES.md`, `design/INTEGRATIONS.md`, `design/THREAT_MODEL.md`, `design/ARCHITECTURE.md`, `design/STORIES.md`, `design/CRITICAL_PATH.md`, `design/PROGRESS.md`, `design/AI_METRICS.md`, `.ai-metrics/FILE_DEPENDENCIES.md`, and relevant approval/output state in `.ai-metrics/workflow-checkpoint.md`. Identify missing or unapproved inputs as findings, not approved facts.

## Consistency checks
1. Vision → Capabilities: capabilities serve named users/success outcomes and respect non-goals.
2. Capabilities → Integrations: each confirmed external system supports a capability; identify unmapped systems and keep unresolved interfaces explicit.
3. Capabilities/Integrations → Threat Model: relevant assets, actors, boundaries and abuse cases are assessed; each high-impact asset has a corresponding control.
4. Capabilities/Integrations/Threat Model → Architecture: map each capability to a responsibility, integration constraints to the architecture, and every required threat control to a component or boundary.
5. Threat Model/Architecture → Stories: map relevant architecture responsibilities to stories; verify forward dependencies, Story 1 test infrastructure, and negative tests in the first story enabling each in-scope abuse. Evaluate the project's approved full customer-to-staff walking skeleton and checkpoint after Story 6, not the template's illustrative Stories 2–3.
6. Capabilities → Stories: verify capability coverage and checkpoint placement against the approved project plan; identify any applicable 3–5-story checkpoint interval concern without replacing the explicitly approved first checkpoint.
7. Stories → Critical Path: check every story appears exactly once in waves, prerequisites occur in earlier waves, graph/Enables relations match, checkpoints are excluded, and the approved review gate is respected. Check whether the structural critical path visits every wave; explain any gate/branch exception rather than changing the graph.
8. Stories → Progress: inspect confirmed `design/PROGRESS.md`, Markdown table, story row/title coverage, canonical single status tokens, checkpoint row, and rolling status. Preserve actual progress; do not demand resetting existing statuses to `todo`.
9. Stories → AI Metrics: inspect confirmed `design/AI_METRICS.md` for story coverage, model/token fields, estimate methodology, timekeeping, and project-confirmed quality-check treatment. Do not require unapproved tools, root-level locations, branches, or invented usage.
10. Non-goals: check capabilities, threat model, architecture, stories, path and tracker against Vision's deferred scope.

An unmapped high-impact asset, required control without an architecture home, or orphan approved capability is a failure finding. Report evidence-based findings with stable identifiers, source paths/sections, and concise explanations; distinguish reproduced, new, and not-reproduced findings without implying a fix. State passing checks briefly. Treat documented unknowns and deferred choices as intentional unless they create an actual inconsistency.

Do not edit audited inputs, propose or perform fixes, or decide findings. Save the audit only; substantive findings review and decisions remain deferred until Prompts 11–13 have been separately authorized and executed, with applicable reviews complete. Approval of this prompt does not approve the findings or authorize implementation.
```

### Prompt 10 Revision 2
- Approval: approved
- Current: yes

```text
Perform a findings-only consistency audit for Yunnan Tasty Garden and save it to `design/CONSISTENCY_AUDIT.md`. Reread the existing audit and the current approved `design/VISION.md`, `design/CAPABILITIES.md`, `design/INTEGRATIONS.md`, `design/THREAT_MODEL.md`, `design/ARCHITECTURE.md`, `design/STORIES.md`, `design/CRITICAL_PATH.md`, `design/PROGRESS.md`, `design/AI_METRICS.md`, `.ai-metrics/FILE_DEPENDENCIES.md`, and relevant approval/output states in `.ai-metrics/workflow-checkpoint.md`. Record the exact input paths, reviewed states, and verifiable fingerprints.

Check consistency from vision and capabilities through integrations, threat controls, architecture, stories, dependencies, waves, progress, and metrics. Preserve the approved Story 6 checkpoint as a review gate. Report evidence-based findings, keeping existing identifiers and decisions; mark findings not reproduced without claiming they are fixed solely on that basis. Assign new identifiers only to new findings. Do not edit audited inputs or decide findings during the audit. After saving the report, present it for separate review.
```

## Prompt 11: Land the walking skeleton

### Prompt 11 Original
- Approval: approved
- Current: no

````
# Land the Walking Skeleton

Build the Yunnan Tasty Garden walking skeleton defined in `design/STORIES.md`: **Stories 1–6**, ending at the **Walking-Skeleton Checkpoint After Story 6**. The goal is to prove the approved customer pickup flow through persistence, confirmation, and staff order management. Do not implement Story 7 or deferred scope.

## Read first

Read `AGENTS.md` if present; `.ai-metrics/workflow-checkpoint.md`; `.ai-metrics/FILE_DEPENDENCIES.md`; `design/VISION.md`; `design/CAPABILITIES.md`; `design/INTEGRATIONS.md`; `design/THREAT_MODEL.md`; `design/ARCHITECTURE.md`; `design/STORIES.md`; `design/CRITICAL_PATH.md`; `design/PROGRESS.md`; and `design/AI_METRICS.md`.

Verify that the current approved plan still identifies Stories 1–6 and the checkpoint after Story 6. If the plan, tracker, prerequisites, wave rules, or checkpoint boundary conflict or are unclear, stop and ask rather than improvising.

## Before starting or resuming implementation

- Obtain a **separate explicit request to execute this prompt**. Approval of the prompt itself authorizes saving it only.
- Verify the design-to-implementation commit/push readiness gate. Recheck it before each story and whenever implementation resumes; stop if it is absent, stale, or unconfirmed.
- Use **`dev` as the base branch and merge target**. Verify that it exists and confirm the story-branch procedure before Git changes. Do not invent a branch name or treat this prompt as authorization to merge.
- Identify the applicable project-confirmed testing, build, lint, type-checking, manual-verification, and other quality checks. If a required runtime, tool, interface, procedure, or decision is missing, stop and ask; do not choose one silently.

## Work through Stories 1–6

For each story in dependency order, one at a time:

1. Check that the story exists, is not already complete, its prerequisites are complete, and its wave may start. Follow the confirmed branch procedure from `dev`.
2. Before implementation, independently estimate `est_human_hours` using the approved methodology and story scope. Record the estimate and rationale; never revise a recorded estimate retroactively. Record actual start, pause, resume, completion, and available provider-reported usage according to `design/AI_METRICS.md`; never invent missing timestamps or usage.
3. Implement **only** the story’s approved acceptance criteria. Add appropriate unit and integration tests alongside the work, including the relevant threat-model negative cases.
4. Run all applicable, confirmed quality checks. Manually verify the intended behavior and relevant regressions where applicable. Report what was actually run, what passed or failed, and what was unavailable or not run.
5. Update `design/PROGRESS.md` using its approved status tokens and record actual metrics in `design/AI_METRICS.md`. Do not mark a story complete until its acceptance criteria and applicable checks are satisfied.
6. Merge to `dev` only after required checks and manual verification pass **and** the developer separately authorizes the merge. Then verify eligibility before proceeding to the next story.

If a story is unclear or conflicts with the architecture, stop and ask. Do not change the authoritative story plan or expand scope.

## Project boundaries

Supabase is selected, but its plan, products, APIs, authentication, policies, and trusted server-side mechanism remain undecided. Stop and ask if a missing decision blocks a story. Use clearly identified synthetic test data until menu/options are verified; do not present preview samples as verified.

Preserve trusted validation, private access, pickup-capacity and abuse protections, and the threat-model controls applicable to each story. Do not imply payment, delivery, Square transmission, customer notifications or status lookup, multiple staff roles, or AI recommendations.

## Walking-Skeleton Checkpoint

After Story 6, use the project-established procedures to run the full test suite and exercise the running application. Manually verify the approved checkpoint scenarios:

- Browse the menu and applicable options, edit a cart, and submit a pickup order.
- Verify persistence and confirmation; simulate failure and verify no false success.
- Sign in as staff, view the submitted order, update its status, and verify persistence.
- Exercise the specified access, tampering, duplicate/shared-IP, and concurrent-capacity negative cases.
- Review architecture boundaries, data flow, security controls, unresolved decisions, and the test results listed in the checkpoint.

Hot-reload verification and a release tag appear in the template but are not confirmed project requirements. Report their status and ask before treating them as requirements or creating a tag.

Report completed stories, checks actually run, blockers, deviations, unresolved decisions, and progress/metrics state. **Stop for developer review before Story 7.**

Approval of this prompt saves the guidance only. Execution, implementation, merges, and checkpoint approval each remain subject to their applicable separate authorization and review gates.
````

### Prompt 11 Revision 1
- Approval: approved
- Current: yes

````
# Land the Walking Skeleton

Build the Yunnan Tasty Garden walking skeleton defined in `design/STORIES.md`: Stories 1–6, ending at the Walking-Skeleton Checkpoint After Story 6. Prove the approved customer pickup flow through persistence, confirmation, and staff order management. Do not implement Story 7 or deferred scope.

## Read first

Read `AGENTS.md` if present; `.ai-metrics/workflow-checkpoint.md`; `.ai-metrics/FILE_DEPENDENCIES.md`; `design/VISION.md`; `design/CAPABILITIES.md`; `design/INTEGRATIONS.md`; `design/THREAT_MODEL.md`; `design/ARCHITECTURE.md`; `design/STORIES.md`; `design/CRITICAL_PATH.md`; `design/PROGRESS.md`; `design/AI_METRICS.md`; and applicable project conventions. Verify the approved plan still identifies Stories 1–6 and the checkpoint after Story 6. If the plan, tracker, prerequisites, wave rules, or checkpoint boundary conflict or are unclear, stop and ask.

## Before starting or resuming

- Obtain a separate explicit request to execute this prompt; approval authorizes saving only.
- Verify the design-to-implementation commit/push readiness gate before implementation, before each story, and whenever work resumes. Stop if absent, stale, or unconfirmed.
- Use `dev` as base branch and merge target. Verify it exists and confirm the story-branch procedure before Git changes. Do not invent a branch name or treat this prompt as merge authorization.
- Identify applicable project-confirmed build, lint, type-checking, tests, browser/manual verification, and other quality checks. If required decisions, tools, commands, interfaces, or procedures are missing, stop and ask. Do not silently select a framework, test library, browser, runtime, or release process.

## Work through the skeleton

The approved sequence is Story 1 Test Infrastructure, Story 2 Application Shell, Story 3 Supabase Data and Access Foundation, Story 4 Customer Menu, Story 5 Cart and Pickup Order Submission, and Story 6 Staff Order Management. Work in dependency order, one story at a time:

1. Verify the story exists, is not already complete, prerequisites are complete, and its wave may start. Follow the confirmed story-branch procedure from `dev`.
2. Before implementation, independently estimate `est_human_hours` using approved story scope and the methodology in `design/AI_METRICS.md`; record estimate and rationale, never revising it retroactively. Record actual start, pause, resume, completion, and available provider-reported usage according to that contract; do not invent timestamps or usage.
3. Implement only the story's acceptance criteria. Add appropriate unit and integration tests alongside the work, including relevant threat-model negative cases. Do not expand scope or change the authoritative story plan.
4. Run all applicable confirmed checks, including build, lint, type-check, and tests where established. Manually verify the intended behavior and relevant regressions where applicable using established procedures. Report checks actually run, failures, unavailable checks, and deviations; never claim unrun checks passed.
5. Record actual metrics and update `design/PROGRESS.md` with one approved status token. Mark the story complete only when acceptance criteria and applicable checks are satisfied.
6. Merge to `dev` only after required checks and manual verification pass and the developer separately authorizes the merge. Recheck eligibility before moving to the next story.

If a story is unclear or conflicts with architecture, stop and ask.

## Project boundaries

Supabase is selected, but its plan, products, APIs, authentication, policies, and trusted server-side execution mechanism remain undecided. Stop and ask if a missing decision blocks work. Use clearly identified synthetic test data until menu/options are verified; do not present preview samples as verified.

Preserve trusted validation, private access, pickup-capacity and abuse protections, and applicable threat-model controls. Do not imply payment, delivery, Square transmission, customer notifications or status lookup, multiple staff roles, or AI recommendations.

## Walking-Skeleton Checkpoint

After Story 6, use established project procedures to run the full test suite and exercise the running application. Manually verify the approved checkpoint scenarios:
- Browse menu data from the backend and applicable options, edit a cart, and submit a pickup order.
- Verify persistence and confirmation; simulate failure and verify no false success.
- Sign in as staff, view the submitted order, update its status, and verify persistence.
- Exercise the specified access, tampering, duplicate/shared-IP, and concurrent-capacity negative cases.
- Review architecture boundaries, data flow, security controls, unresolved decisions, and checkpoint test results.

Hot-reload verification and a release tag appear in the template but are not confirmed project requirements. Report their status and ask before treating them as requirements or creating a tag.

Report completed stories, files/components or responsibilities changed, tests and checks actually run, blockers, deviations, unresolved decisions, and progress/metrics state. Stop for developer review before Story 7. Approval of this prompt saves the guidance only; execution, implementation, merges, and checkpoint approval remain subject to their applicable separate authorization and review gates.
````

## Prompt 12: Implement one story

### Prompt 12 Original
- Approval: approved
- Current: yes

````
# Implement One Story

Implement **[TARGET_STORY_NUMBER_AND_TITLE]** from this repository’s `design/STORIES.md`. Replace the placeholder with the exact story number and title before use.

## Read first

Read `AGENTS.md` if present; `.ai-metrics/workflow-checkpoint.md`; `.ai-metrics/FILE_DEPENDENCIES.md`; `design/VISION.md`; `design/INTEGRATIONS.md`; `design/THREAT_MODEL.md`; `design/ARCHITECTURE.md`; `design/STORIES.md`; `design/CRITICAL_PATH.md`; `design/PROGRESS.md`; `design/AI_METRICS.md`; and the contracts, conventions, and examples required by the target story.

## Before editing

- Verify that the target exists, is not already done, its prerequisites are complete, its wave may start, and any preceding checkpoint has been reviewed. List the stories recorded as complete. If a check fails or is unclear, stop and report why.
- Obtain a **separate explicit execution request** and verify the current design-to-implementation commit/push readiness gate. Recheck the gate whenever implementation resumes; stop if it is absent, stale, or unconfirmed.
- Use **`dev` as the base branch and merge target**. Verify it exists and confirm the story-branch procedure before Git changes. Do not invent a branch name or treat this prompt as authorization to merge.
- Identify the applicable project-confirmed build, lint, type-checking, tests, manual-verification, and other quality checks. If a required scope, interface, runtime, tool, or procedure is missing or unclear, stop and ask.

## Implement the selected story

1. Follow the confirmed story-branch procedure from `dev`. Before implementation, independently estimate `est_human_hours` using the approved methodology, story scope, acceptance criteria, and applicable checks. Record the estimate and rationale in the metrics record and raw log; do not ask the developer to supply or approve the number, and never revise it retroactively. Ask only if required scope or methodology is unclear.
2. Record actual story-work start, pause, resume, completion, and available provider-reported usage according to `design/AI_METRICS.md`. Never invent timestamps or usage; record missing information as unknown.
3. Implement **only** the selected story’s approved acceptance criteria, including its relevant pages/components and data responsibilities. Add appropriate unit and integration tests alongside the work, including applicable threat-model negative cases. Do not add stories, change scope, or introduce unapproved tools or runtimes.
4. Run all applicable, confirmed quality checks. Manually exercise the intended behavior end-to-end where applicable and check relevant regressions. Report what was actually run, what passed or failed, and what was unavailable or not run.
5. Record actual metrics and calculate leverage only when valid data exists. Update `design/PROGRESS.md` using one approved status token; do not mark the story done until its acceptance criteria and applicable checks are satisfied.
6. Merge to `dev` only after required checks and manual verification pass **and** the developer separately authorizes the merge.

If the story is unclear or conflicts with the architecture, stop and ask rather than guessing. Report what was built, components or responsibilities changed, test counts where available, checks, metrics, blockers, and deviations.

Check `design/STORIES.md` for a checkpoint reached by this work. If one is reached, perform only its applicable verified checks and **stop for developer review before later-wave work**. Hot-reload verification and a release tag are unconfirmed; do not impose or create them without approval.

Approval of this prompt saves it only. Execution and merging require separate authorization and satisfaction of the applicable gates.
````

## Prompt 13: Review a planned checkpoint

### Prompt 13 Original
- Approval: approved
- Current: yes

````
# Review a Planned Checkpoint

Review **[TARGET_CHECKPOINT_NAME_OR_AFTER_STORY]**. Replace the placeholder with an exact checkpoint named in approved `design/STORIES.md` before use.

## Verify the boundary

Obtain a separate explicit request to perform this review; prompt approval alone does not authorize execution. Derive the checkpoint boundary and covered stories from approved `design/STORIES.md` and `design/CRITICAL_PATH.md`. Verify using `design/PROGRESS.md` and relevant work records that the boundary has been reached and required work through it is complete. If the boundary is unclear, not reached, or incomplete, report why and stop without reviewing later-wave work.

## Read first

Read `AGENTS.md` if present; `.ai-metrics/workflow-checkpoint.md`; `.ai-metrics/FILE_DEPENDENCIES.md`; `design/VISION.md`; `design/INTEGRATIONS.md`; `design/THREAT_MODEL.md`; `design/ARCHITECTURE.md`; `design/STORIES.md`; `design/CRITICAL_PATH.md`; `design/PROGRESS.md`; `design/AI_METRICS.md`; applicable workflow instructions; and the implementation artifacts and confirmed conventions relevant to this checkpoint.

## Review the reached checkpoint

1. **Quality checks:** Run applicable project-confirmed checks, including the full test suite and coverage where confirmed. Report actual results and unavailable or unrun checks; do not invent commands or claim a check passed.
2. **Structure and component health:** Show the relevant actual file/module structure and compare responsibilities and dependency flow with approved Architecture. Review whether relevant components have tests, unexpected dependencies, problematic data/prop flow, or complexity concerns. Do not impose an unapproved line-count threshold or framework-specific tree.
3. **Manual verification:** Exercise the checkpoint’s approved browser and end-to-end scenarios using established procedures. Navigate the implemented areas, check the latest capability and relevant regressions, and inspect observable console errors or warnings where applicable. Do not prescribe unconfirmed browsers or commands.
4. **Architecture and security:** Report deviations in components, boundaries, state, interfaces, and threat controls, including applicable negative-test results. Compare against the approved design without changing it.
5. **Technical debt:** Report relevant TODOs, FIXMEs, workarounds, and risks that could affect later work.
6. **Metrics and progress:** Compare completed stories and checks with `design/PROGRESS.md`; review estimates, actuals, leverage trends, and fast/slow patterns in `design/AI_METRICS.md` where data is sufficient. Identify missing data rather than inventing it.
7. **Outcome:** Summarize whether the evidence supports continuing as planned or whether potential story, architecture, or scope changes require developer decisions. Make evidence-based recommendations without modifying the authoritative plan or implementing changes.

For the currently planned walking-skeleton checkpoint after Story 6, use its scenarios in `design/STORIES.md`, including order persistence/confirmation, staff status updates, failed submission, access boundaries, tampering, duplicate/shared-IP handling, and concurrent capacity.

Hot-reload verification and release tagging are unconfirmed. Report their status and ask before treating either as a requirement or creating a tag. Save the review only at a developer-confirmed or established project location; ask if none is established.

Report files reviewed or changed, checks and results, findings, metrics, unresolved decisions, and blockers. **Stop for developer review before later-wave work.** Proposed changes require the ordinary dependency, per-file, and approval gates; do not silently update the story plan or tracker revision notes.

Approval of this prompt saves it only; it does not authorize execution or approve a checkpoint.
````
