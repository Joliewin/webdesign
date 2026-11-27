# Stories — Yunnan Tasty Garden

## Table of Contents
- [Story 1: Test Infrastructure](#story-1-test-infrastructure)
- [Story 2: Application Shell](#story-2-application-shell)
- [Story 3: Supabase Data and Access Foundation](#story-3-supabase-data-and-access-foundation)
- [Story 4: Customer Menu](#story-4-customer-menu)
- [Story 5: Cart and Pickup Order Submission](#story-5-cart-and-pickup-order-submission)
- [Story 6: Staff Order Management](#story-6-staff-order-management)
- [Walking-Skeleton Checkpoint After Story 6](#walking-skeleton-checkpoint-after-story-6)
- [Story 7: Admin Menu Management](#story-7-admin-menu-management)
- [Deferred Scope](#deferred-scope)

## Story 1: Test Infrastructure
- **Depends on**: none
- **Enables**: Story 2
- **Builds**: Tool-neutral automated test foundation and organization.
- **Acceptance Criteria**:
  - A documented, repeatable procedure runs unit and integration tests and reports failures.
  - Test boundaries support substitutes for conceptual backend operations without assuming endpoint paths/contracts.
  - A small example demonstrates both failing and passing assertions; coverage collection is supported without imposing a target or tool.
  - The foundation can test safe rendering/XSS cases and verify privileged secret/token leakage is absent from client assets, URLs, logs, and errors.
  - Each subsequent story adds appropriate unit and integration tests alongside the capability; no specific framework, package, path, CI, or test database is selected.
- **Complexity**: M

## Story 2: Application Shell
- **Depends on**: Story 1
- **Enables**: Story 3
- **Builds**: Runnable application shell, navigation, and shared layout responsibility from Architecture.
- **Acceptance Criteria**:
  - The application can be started using the established project procedure and renders a usable primary view and navigation.
  - Layout adapts without horizontal overflow; interactive controls have visible keyboard focus.
  - The shell and shared UI establish the approved palette, typography with fallbacks, and reference spacing guidance in `design/CAPABILITIES.md`, using warm editorial surfaces rather than dashboard-like card grids. Unspecified values and production asset choices remain undecided.
  - Shared controls provide visible focus, hover and selected states where applicable, distinct feedback states, and respect reduced-motion preferences; tests and visual review verify these behaviors as applicable to the shell.
  - Tests cover shell rendering, navigation behavior, and relevant responsive/accessibility states.
  - Add both unit and integration tests appropriate to this increment, alongside implementation.
  - No production menu content, backend behavior, or unapproved route path is fabricated.
- **Complexity**: M

## Story 3: Supabase Data and Access Foundation
- **Depends on**: Story 2
- **Enables**: Stories 4, 5, and 7
- **Builds**: Supabase persistence boundary and conceptual menu/order data access required by customer, staff, and admin stories.
- **Acceptance Criteria**:
  - The data model can represent active menu items, prices, item-specific options, orders, customer contact fields, pickup choice/time, status, and confirmation identifiers.
  - The implementation uses Supabase but does not assume a plan, auth product, API contract, schema detail, or trusted execution mechanism not yet approved.
  - Public menu access is separated from private order/customer data and privileged menu operations.
  - Privileged credentials are absent from browser-delivered assets.
  - Tests verify unauthorized order reads/writes are denied, no privileged credentials are exposed in assets/URLs/logs/errors, and any implemented client/backend traffic uses secure transport.
  - Before implementation, the owner resolves whether order lines preserve item/price/option snapshots; the story does not silently choose.
- **Complexity**: L

## Story 4: Customer Menu
- **Depends on**: Story 3
- **Enables**: Stories 5 and 7
- **Builds**: Customer menu area, menu data display, and applicable option presentation.
- **Acceptance Criteria**:
  - Customers can browse active menu items with current names, descriptions, prices, and only the options configured for each item.
  - Inactive/unavailable items are not orderable; loading, empty, and service-error states are clear and never substitute unverified preview dishes/prices.
  - Menu content is safely rendered as untrusted data.
  - Keyboard and assistive-technology users can navigate item/category content with meaningful labels and visible focus.
  - Tests cover active/inactive items, loading/empty/error cases, data display, keyboard access, and inert rendering of malicious-looking text.
  - Verified menu/options are supplied before production use.
- **Complexity**: M

## Story 5: Cart and Pickup Order Submission
- **Depends on**: Stories 3 and 4
- **Enables**: Story 6
- **Builds**: Customer cart/checkout, trusted order-submission operation, persistence, and confirmation response.
- **Acceptance Criteria**:
  - Customers can add items, choose applicable options, review/change/remove selections, and provide required name/phone with optional email/notes.
  - Customers can choose ASAP or scheduled pickup. Scheduled slots are 15 minutes, require 30 minutes’ notice, are within daily 11:00 a.m.–9:30 p.m. hours, and allow at most 8 orders per slot. Final cutoff and ASAP capacity remain unresolved.
  - Trusted server-side processing revalidates active items/options and authoritative prices and atomically enforces pickup timing/capacity; browser-only checks are insufficient.
  - Duplicate and abuse controls apply server-side without blocking a customer solely for sharing an IP. Exact thresholds/challenges remain undecided.
  - A confirmation number appears only after successful storage; rejected/failed submission never appears successful.
  - No payment, delivery, Square transmission, email/text notification, or status lookup is implied.
  - Unit/integration negative tests cover missing/invalid fields, inactive/forged items, option/price tampering, duplicate attempts, failed persistence, legitimate shared-IP users, concurrent slot-capacity races, and safe handling of customer notes.
- **Complexity**: L

## Story 6: Staff Order Management
- **Depends on**: Story 5
- **Enables**: none
- **Builds**: Private staff login/dashboard, order display, and status update responsibilities.
- **Acceptance Criteria**:
  - Unauthenticated visitors cannot open the private view or retrieve order/customer details.
  - Authenticated staff can see submitted order contents/options, pickup choice/time, confirmation identifier, and necessary contact details.
  - Staff can update status to new, preparing, ready, completed, or cancelled; changes persist and appear on revisit.
  - Staff cannot perform admin-only menu changes.
  - Loading, empty, and failure states are clear and accessible.
  - Tests cover anonymous/unauthorized access, staff permission boundaries, status persistence, sensitive diagnostic-data leakage, and safe rendering of stored content.
  - If cookie-based sessions are selected, cross-origin state-changing requests without valid CSRF protection are rejected.
  - Authentication provider, session/token approach, and detailed policy remain undecided until implementation planning.
- **Complexity**: L

## Walking-Skeleton Checkpoint After Story 6

This checkpoint is a review gate, not a story or dependency-graph node. Stop here for developer review before Story 7.

**Manual verification**
- Use clearly identified synthetic test menu data—not preview samples presented as verified—to browse, configure options, edit a cart, and submit a pickup order.
- Verify persisted order details and confirmation number; simulate failed persistence and verify no success confirmation appears.
- Sign in as staff, view that order, update its status, and verify it remains updated.
- Verify anonymous users cannot retrieve order or contact information.
- Exercise price/item/option tampering, duplicate submissions, legitimate shared-IP customers, and near-capacity concurrent scheduled requests.

**Architecture/security review**
- Confirm customer UI → data boundary → trusted operation → Supabase flow and staff order visibility match Architecture.
- Review public/private access, authorization, safe rendering, token/secret/log/error handling, secure transport, capacity atomicity, and any conditional CSRF/third-party controls.
- Confirm test infrastructure supports unit/integration and relevant negative tests without an unapproved tool choice.
- Review production service-state monitoring readiness, including whether the owner, method, provider, and configuration have been decided; unresolved choices remain open and monitoring must not be represented as implemented without evidence.

**Decision point**
- Review verified menu/options and temporary test-data handling; final cutoff; ASAP capacity; timezone; Supabase plan/auth/policies; hosting/region/environment; backup/recovery; order-time snapshots; and browser/accessibility targets.
- Run the full test suite and exercise the running application using project-established procedures; no specific command/tool is prescribed here.

## Story 7: Admin Menu Management
- **Depends on**: Stories 3 and 4
- **Enables**: none
- **Builds**: Separate private admin area for menu item/options maintenance.
- **Acceptance Criteria**:
  - Authorized admins can create/edit menu names, descriptions, prices, availability, spice choices, and add-ons.
  - Validation feedback distinguishes invalid input, save success, and save failure; updates appear in subsequent customer menu reads/orders.
  - Public users and staff without admin authorization cannot edit menu data.
  - Stored/admin-controlled content is safely rendered; tests cover unauthorized writes, invalid values, and XSS-style input.
  - If cookie-based sessions are selected, admin state-changing operations receive the approved CSRF protection and negative tests.
  - Verified menu data is provided before production use; sample preview content remains unverified.
  - Add unit and integration tests for menu form behavior and persisted edits.
- **Complexity**: L

## Deferred Scope

No implementation stories are included for online payment, delivery, Square POS, customer email/text notifications, customer status lookup, multiple staff roles, or customer-facing AI recommendations. Reassess their security and integration needs before enabling them.

## Coverage Cross-Check

- **Capabilities:** menu browsing—Story 4; menu administration—Story 7; cart/checkout/order submission/abuse protection—Story 5; staff order management—Story 6; frontend design system—Story 2; visual/accessibility and feedback expectations—Stories 2, 4–7.
- **Architecture:** test foundation—Story 1; application shell/shared layout—Story 2; Supabase/data/API/access boundary—Story 3; customer area—Stories 4–5; trusted order processing—Story 5; staff area/auth—Story 6; admin area/auth/menu mutations—Story 7; security controls, service monitoring readiness, and operational recovery—applicable stories and checkpoint.
- **Known gaps:** exact endpoint contracts, auth/policies, hosting/runtime, final pickup edge rules, verified menu data, backup plan, and order snapshot behavior remain unresolved rather than silently decided.
