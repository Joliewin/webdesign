# Threat Model — Yunnan Tasty Garden

## Assets

Impact ratings are qualitative and reflect current project information.

| Asset | Owner | Disclosure impact | Alteration impact | Unavailability impact |
|---|---|---:|---:|---:|
| Customer name, phone, optional email/notes, and submitted order | Customer and restaurant | High | High | High during service |
| Orders, confirmation identifiers, and pickup capacity/schedule | Restaurant and customers | Medium | High | High during service |
| Menu items, prices, availability, spice choices, and add-ons | Restaurant | Low | High | Medium |
| Staff/admin credentials and authorization configuration | Restaurant | High | High | Medium |
| Supabase project configuration/privileged credentials, if provisioned | Restaurant | High | High | High |
| Pre-submit cart/form data in the browser | Customer | Medium; exact exposure depends on fields and browser behavior | Medium | Low |
| Public client configuration and backend endpoint information | Restaurant | Low unless it contains secrets (none confirmed) | Medium | Medium |
| Browser session/token data, if used | Restaurant and staff/admin users | High | High | Medium |
| Third-party request metadata if remote assets remain | Site visitors | Low/uncertain | Low | Low |

## Actors and Trust Assumptions

- **Anonymous customers:** Confirmed public users; their form/cart inputs and requests are untrusted.
- **Staff/admins:** Must authenticate to access private order/menu operations. Authentication method and detailed permissions are undecided.
- **Abusive automated clients/attackers:** Plausibly submit manipulated or repeated requests and attempt unauthorized access.
- **Supabase:** Selected managed backend/database provider; account, plan, products, policies, and availability configuration are undecided.
- **Third-party asset providers:** Google Fonts, Unsplash, Google Maps, and Instagram appear in preview references; production use varies by service and is unconfirmed. No third-party script integration is confirmed.
- **Browser extensions and network attackers:** Possible actors at the client boundary; browser-extension privileges, network conditions, and deployment transport configuration are not established.
- **Attacker with a stolen token:** Conditional on an authentication/token mechanism being selected; no token method is confirmed.

## Trust Boundaries

| Boundary | Authentication/trust status |
|---|---|
| Customer browser → application/backend/Supabase | Customer identity is not required for public ordering; the browser and all requests/fields are untrusted. Trusted server-side validation is required; exact protocol/path is undecided. |
| User input/cart → application and stored/rendered content | Input is untrusted. Menu descriptions, customer notes, and other stored text remain untrusted when rendered. |
| Staff/admin session → order/menu operations | Login is required; provider, session mechanism, and authorization rules are undecided. The receiving operation must verify identity and permission. |
| Browser → third-party assets/links | Applies only if retained. No external script is confirmed; remotely loaded resources and outbound links remain separate providers. |
| Browser extensions → application state | Extension permissions are outside the application’s control; page data may be exposed depending on installed extensions. |
| Client ↔ network/backend | Transport/security configuration is not yet selected. Network interception is a plausible risk; production transport protections must be confirmed in architecture/deployment. |

## In-Scope Abuse Cases and Required Controls

| Abuse case | Required testable control | Negative-test expectation |
|---|---|---|
| Unauthorized order/customer-data access or privilege escalation | Least-privilege authorization at trusted data-access operations; separate public menu access from private order access. | Anonymous users and unrelated customers cannot retrieve orders or contact details. |
| Forged items/options/prices | Revalidate active menu items and applicable options and derive totals from authoritative menu data on a trusted server path. | Tampered totals, inactive items, and invalid options are rejected or safely recalculated. |
| Duplicate/abusive submissions | Server-side duplicate and abuse protections; do not block solely because users share an IP. | Repeated submissions do not create unintended duplicate orders; legitimate shared-IP users are not categorically denied. |
| Scheduled-slot oversubscription | Atomically enforce hours, minimum notice, and maximum 8 orders per 15-minute slot with order persistence. | Concurrent submissions cannot exceed capacity; invalid/out-of-window times are rejected. |
| Unauthorized menu edits/staff-to-admin escalation | Verify authenticated identity and permission for each order or menu operation. | Anonymous users and staff without admin permission cannot change menu/pricing/options. |
| XSS or client-side injection through menu descriptions/notes | Validate input as appropriate and contextually encode/safely render stored content; do not evaluate untrusted data as code. | Script/HTML-like input remains inert in customer, staff, and admin views. |
| CSRF on state-changing requests | If cookie-based sessions are selected, use an appropriate CSRF defense and same-site/session protections; otherwise document the selected mechanism’s relevant protections. | Cross-origin state-changing requests without valid protections are rejected. |
| Token/secret leakage via browser storage, URLs, logs, console, or errors | Keep privileged secrets server-side; minimize client token exposure; redact sensitive data from logs/errors and never place credentials in URLs. | Built assets, browser storage, URLs, console, and user-facing errors expose no privileged secret or unnecessary customer data. |
| Sensitive data exposure through browser diagnostics | Avoid logging full customer/order payloads and suppress sensitive details in error/diagnostic output. | Normal failures and diagnostic views do not reveal unnecessary contact/order data. |
| Third-party compromise | No third-party scripts are currently confirmed. If scripts are introduced, restrict permitted sources and prevent access to sensitive application data where feasible; re-review the dependency. | Unapproved script sources are not loaded; any retained script cannot access privileged credentials. |
| Service interruption, plan pause, or data loss | Select a production plan, monitor service state, and establish/test backup and recovery before launch. | Failed persistence never yields order confirmation; recovery procedure is successfully exercised before production. |
| Network interception | Confirm secure transport and certificate handling for production browser/backend traffic. | Production traffic does not transmit credentials or customer/order data over an unprotected connection. |

Conditional controls must be finalized after authentication, hosting, and external-resource decisions. None of these controls is claimed to be implemented.

## Out-of-Scope Attacks

- **Resource exhaustion confined to an attacker's own browser:** out of scope for application availability because it does not affect other customers or shared service capacity. Abuse or denial of service affecting order submission remains in scope.
- **Compromise of a provider's internal infrastructure:** outside this application-level model and not assessed here; provider assurance, contract, and recovery options remain open. Resulting customer-data exposure or order unavailability remains a project risk.
- **Malicious behavior by a user’s independently installed browser extension:** the extension is outside application control, but it remains a client trust boundary and a residual privacy risk; the application must not expose unnecessary secrets/data to the page.

## Story and Tool Implications

- Story 1 test infrastructure must support XSS/inert-rendering tests and verification that secrets/tokens are not exposed in client assets, URLs, logs, or errors; no test framework is selected.
- Order-submission stories need negative tests for tampered items/prices/options, duplicates, shared-IP legitimate customers, failed persistence, and concurrent slot-capacity races.
- Staff/admin stories need tests for unauthenticated and insufficiently authorized reads/writes.
- If cookie sessions are selected, state-changing stories need CSRF negative tests.
- If third-party scripts are added, test/verify the allowed source boundary and review access to application data.
- Recovery testing is a production-readiness requirement, not a claim that a current backup exists.

## Residual Risk

- **Basic staff/admin access model:** detailed roles are deferred; an over-privileged or compromised account could affect orders and menu data. Owner: restaurant. Authentication/account practices are undecided.
- **Production recovery:** plan and backup process are undecided; loss or corruption may be unrecoverable without verified backups. Owner: restaurant.
- **Third-party asset requests:** if remote assets remain, visitors contact those providers and may expose request metadata; production privacy and fallback effects need review. Owner: restaurant.
- **Browser extensions and network conditions:** outside application control; exact exposure depends on user environment and production transport configuration, which remains unresolved.
- **Provider-internal compromise:** outside application-level control; impact and provider assurance are unknown. Owner for provider selection/review: restaurant.

## Cross-Check

- High-impact customer/order, credential, and availability assets have corresponding access, secret-handling, validation, recovery, or transport controls.
- Confirmed Supabase and conditional external assets appear in the actor/boundary model; no unsupported third-party script or auth mechanism is asserted.
- Every listed control is intended to receive a component/boundary home in Architecture; exact service, protocol, and authentication choices remain open.
- Online payment, delivery, Square POS, customer notifications/status lookup, multiple staff roles, and AI recommendations are deferred; assess their threat surfaces before enabling them.
