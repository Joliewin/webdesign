# Architecture — Yunnan Tasty Garden

## Tech Stack (from Integrations)

Supabase is the selected managed backend/database provider for menu and order data. Framework/version, routing, server-state library, styling, forms/validation, testing/build tools, runtime, hosting, auth product, Supabase APIs, and package choices are **undecided**. Confirmed rationale: order integrity, pickup capacity, and private access require trusted server-side enforcement. No alternatives are confirmed as evaluated or rejected.

## Application Structure

| Page/area (route undecided) | Responsibility and data needs |
|---|---|
| Customer menu/cart/checkout | Read active menu/options; edit cart; collect required name/phone and optional email/notes; choose pickup; submit; display confirmation only after persistence |
| Staff dashboard | Authenticate; read orders and necessary contact/details; update status |
| Admin menu management | Authenticate with menu-edit permission; create/update items, prices, availability, spice choices, and add-ons |

**Shared components:** keep a flat set grouped by Layout, Data Display, Input, Feedback, and Navigation. Shared UI implements the approved frontend design system in `design/CAPABILITIES.md`, including palette, typography and fallbacks, spacing, warm editorial atmosphere, interaction states, and reduced-motion guidance across applicable areas. Unspecified tokens and production asset choices remain open. Controlled/uncontrolled choices are undecided.

**API client/data boundary:** conceptual operations are `read active menu/options`, `submit pickup order`, `authenticate staff/admin`, `read orders`, `update order status`, and `create/update menu`. These are descriptions, not endpoint names or approved contracts. No paths, methods, schemas, error format, or backend API spec are confirmed.

**Data fetching/state:** queries are needed for menu and staff order lists/details; mutations for order submission, status changes, and menu edits. Hook names, cache keys, stale-time, invalidation, and optimistic/refetch strategy are undecided. Types needed conceptually: menu item/options, cart/order input, persisted order/confirmation, status, auth context, form values, and component props. Exact schemas and TypeScript use are undecided.

## Dependency Flow

`Pages → shared Components → data/state responsibilities → API/data-access boundary → trusted server-side operations → Supabase`

Styling supports shared components. The browser may initiate requests but must not perform privileged operations directly. Trusted processing validates and authorizes before persistence.

## Key Design Decisions

- **Composition:** separate customer, staff, and admin areas; exact modules/routes undecided.
- **Forms:** customer/admin input needs validation and clear errors; control model/timing undecided. Server validation remains authoritative.
- **Uploads:** none required or confirmed.
- **Filtering/sorting:** menu/order needs exist; backend support is unknown, so responsibility is undecided.
- **Errors:** distinguish loading, validation/rejection, service failure, and success; never show order success before persistence. Error-boundary placement/retry policy undecided.
- **Auth:** login required for staff/admin. Provider, token/session storage and injection, refresh, and authorization policy undecided. Privileged secrets stay server-side.
- **Dialogs:** URL-based versus state-based behavior undecided.

## Security and Control Placement

| Threat-model control | Component/boundary home; negative verification |
|---|---|
| Least privilege, private order access, staff/admin permissions | Trusted authorization/data boundary; anonymous users cannot read orders; staff cannot edit menu |
| Server-side item/options/price validation | Trusted order submission; tampered totals, inactive items, and invalid options rejected/recalculated |
| Atomic scheduled capacity and timing | Trusted processing plus persistence; concurrent requests cannot exceed 8 per slot or bypass hours/notice |
| Duplicate and abuse controls | Trusted submission boundary; duplicate attempts controlled and shared-IP customers not categorically blocked |
| Safe rendering/XSS defense | Shared rendering boundary; malicious-looking menu text/notes stay inert |
| Secret/token and diagnostic-data protection | Server configuration and logging/error boundaries; no privileged secret in browser assets/URLs/logs/errors or unnecessary customer data in diagnostics |
| Conditional CSRF protection | State-changing auth boundary if cookie sessions are selected; cross-origin unprotected mutations rejected |
| Conditional third-party script restriction | Browser asset boundary if scripts are introduced; unapproved script sources do not load |
| Secure transport | Production browser/backend boundary; sensitive traffic is not sent unprotected |
| Backup/recovery | Restaurant/provider operational boundary; agreed recovery is tested before production |
| Service-state monitoring | Production operations boundary monitors service state; monitoring owner, method, provider, and configuration remain undecided |

Controls are requirements, not claims of implementation. Provider-internal compromise and user-installed extension behavior remain outside application control; their impacts remain residual risks.

## File Structure (Conceptual)

```text
application/
  customer-area/   staff-area/   admin-area/
  shared-ui/       data-state/
  api-boundary/    trusted-operations/
  domain-types/    utilities-config/
```

Names are illustrative groupings only; no framework or concrete file tree is selected.

## Data Flow and Open Decisions

Customers read active menu/options, build a cart, and submit contact details/items/pickup choice. Trusted processing revalidates data/prices, enforces pickup and abuse rules, persists the order, and returns a confirmation only on success. Staff read orders/update status; admins manage menu data.

Scheduled pickup: 15-minute slots, 30-minute minimum notice, maximum 8 orders per slot, daily 11:00 a.m.–9:30 p.m. Final cutoff, ASAP capacity, and timezone remain unresolved. Order-time item/price/options snapshots are also unresolved.

Still undecided: Supabase account/plan/products/APIs/policies/auth; trusted server mechanism; hosting/region/environment; monitoring owner, method, provider and configuration; backup/recovery owner and procedure; API contracts; exact menu/options; supported browsers; detailed accessibility targets; and order snapshots. Deferred: payment, delivery, Square, notifications/status lookup, multiple staff roles, and AI recommendations.

## Cross-Check

| Approved capability/constraint | Architecture home |
|---|---|
| Browse full active menu and applicable options | Customer area; active menu read |
| Cart and pickup checkout/contact fields | Customer area; cart and form responsibilities |
| Order persistence and success confirmation | Trusted submit operation; Supabase |
| Abuse protection, price integrity, pickup limits | Trusted processing/persistence boundary |
| Staff login, order visibility, status updates | Private staff area; auth/read/update operations |
| Admin menu/options maintenance | Separate admin area; authorized menu mutations |
| Responsive/accessibility and feedback states | Shared UI and page responsibilities; exact standards remain open |
| Frontend design system | Shared UI and page responsibilities implement the approved visual and interaction guidance |
| Supabase, remote assets, hosting and operational constraints | Data/API boundary and deployment decisions above |
| Threat controls | Mapped above, including conditional controls and negative expectations |

No backend endpoint is confirmed, so conceptual operations above have no approved endpoint functions/contracts yet. No specific package/component implementation is selected. Menu data, pickup edge rules, auth/access policies, deployment, and recovery remain gaps to resolve.
