# Capabilities — Yunnan Tasty Garden

## Walking Skeleton (MVP): Pickup Order End to End

**User Story:** As a customer, I want to choose dishes from the available menu and submit a pickup order, so that the restaurant receives it and I know it was recorded; staff need to see and manage the order.

**Acceptance Criteria**
- The customer can open the menu, see available items and prices, select a dish, and configure only options shown for that dish.
- The customer can review the cart, provide required name and phone, optionally add email/notes, and choose ASAP or a valid scheduled pickup.
- The experience clearly displays loading, validation, rejection, and failure states; a backend failure never looks like success.
- On successful order submission and storage, the customer sees an on-site confirmation number.
- Authenticated staff can see the same order and update its status in the private order view.
- No online payment is collected and no screen implies the order was sent to Square.
- Keyboard users can complete the flow with visible focus; labels, errors, status, and confirmation are available to assistive technology.
- The v1 plan also includes admin menu maintenance, although it is not required to prove this smallest end-to-end slice.

## Core Capabilities

### 1. Browse the Active Full Menu — Must

**User Story:** As a customer, I want to browse the restaurant’s current menu and applicable options, so that I can decide what to order.

**Acceptance Criteria**
- The menu shows active item names, descriptions, prices, and only the spice/add-on choices configured for each dish.
- Loading, empty, and unavailable/error states are clear and do not present sample preview content as verified menu data.
- Prices and option labels are readable and consistently formatted; unavailable items are not presented as orderable.
- Keyboard and screen-reader users can navigate menu categories and item details with clear names and focus.
- The verified full menu and dish-specific options are supplied before production use.

**Dependencies:** none.

### 2. Maintain Menu and Item Options — Must

**User Story:** As an admin, I want to maintain menu items and their prices/options without editing code, so that customers see the current menu.

**Acceptance Criteria**
- An authorized admin can create and edit item names, descriptions, prices, availability, applicable spice levels, and add-ons in a distinct private experience.
- Forms identify required and invalid values with understandable field-level feedback; save success and failure are distinguishable.
- Updated menu information is reflected in subsequent customer menu views and orders.
- The interface exposes only the options configured for each item; it does not imply every dish has spice choices or add-ons.
- Keyboard access, visible focus, labels, and assistive-technology feedback are available for menu editing.
- Unauthenticated visitors and staff without admin access cannot perform menu edits.
- Menu source data remains unverified until confirmed by the restaurant.

**Dependencies:** Browse the Active Full Menu.

### 3. Build and Review a Pickup Cart — Must

**User Story:** As a customer, I want to assemble and review my selected dishes and options, so that I can correct my order before submitting it.

**Acceptance Criteria**
- Customers can add one or more available menu items and choose only options applicable to each item.
- Customers can change quantities/selections and remove items before submission; the displayed cart reflects those changes.
- Empty-cart and invalid/unavailable-item states are clear; item names, selected options, and prices are readable.
- Cart controls are keyboard operable, labeled, and announce meaningful updates to assistive technology.

**Dependencies:** Browse the Active Full Menu.

### 4. Submit an ASAP or Scheduled Pickup Order — Must

**User Story:** As a customer, I want to provide my contact details and choose when to pick up, so that I can submit an accurate order.

**Acceptance Criteria**
- Checkout requires name and phone; email and order notes are optional. Missing or invalid required fields receive clear messages and focus can reach the errors.
- Customers can choose ASAP or scheduled pickup. Scheduled times use 15-minute slots, require at least 30 minutes’ notice, are within daily 11:00 a.m.–9:30 p.m. hours, and permit at most 8 orders per slot.
- Final scheduled-slot cutoff behavior and ASAP capacity remain undecided and are not fabricated by the interface.
- The customer receives an on-site confirmation number only after the order has been accepted and stored; a rejected or failed submission does not show success.
- Loading/submitting, accepted, validation/rejection, and service-failure states are distinguishable and usable with keyboard and assistive technology.
- The experience does not collect online payment, claim delivery, imply transmission to Square, or promise email/text notification or later status lookup.

**Dependencies:** Build and Review a Pickup Cart.

### 5. Protect Order Submission from Accidental Duplicates and Abuse — Must

**User Story:** As the restaurant, I want order submission protected from accidental duplicates and abusive traffic, so that legitimate customers can order while the restaurant can rely on submitted orders.

**Acceptance Criteria**
- Repeated submission and abusive traffic receive server-side protection; the customer receives an understandable outcome when a submission is rejected.
- A blanket one-order-per-IP-per-15-minutes rule is not used; legitimate customers sharing an IP are not categorically blocked.
- A duplicate attempt does not silently create an unintended second order.
- Detection signals, thresholds, and any customer-facing challenge remain undecided until reviewed.

**Dependencies:** Submit an ASAP or Scheduled Pickup Order.

### 6. Manage Incoming Orders — Must

**User Story:** As restaurant staff, I want to sign in, see submitted orders, and update their status, so that I can process pickup orders.

**Acceptance Criteria**
- Unauthenticated visitors cannot access the private staff view or customer/order details.
- Authenticated staff can see submitted order contents, selected options, pickup choice/time, confirmation number, and necessary customer contact information.
- Staff can set status to new, preparing, ready, completed, or cancelled; updates remain visible when staff return.
- Loading, empty, and failure states are distinct; status and order information are readable and announced accessibly.
- Staff cannot edit menu data unless authorized as an admin; detailed roles/permissions beyond this boundary are deferred.

**Dependencies:** Submit an ASAP or Scheduled Pickup Order.

## Frontend Design System

The visual direction is warm, contemporary restaurant editorial—not a dashboard or a rigid grid of boxed cards. Existing preview/specification values below are references for the new experience, not proof that remote assets or placeholder behavior must be retained.

### Color Palette

- **Primary/background surfaces:** cream `#fff4e5`, deep cream `#f5e8d6`; the menu reference also uses `#f5f0e9`.
- **Primary action/brand:** burgundy `#6b1f2a`; deep burgundy `#48151d`; hover burgundy `#842d38`; orange/copper `#d96b32`.
- **Text:** espresso `#2b211d`; muted brown `#665750`.
- **Borders/dividers:** `#e6d8c7`.
- **Semantic success, warning, error, and info colors:** not defined by the source; choose and verify accessible values during visual design rather than assuming them.
- The existing menu-heading treatment blends `#e9ddd2` into `#f5f0e9`.

### Typography

- **Families:** Bitter for headings/brand; Inter for body, prices, and controls; Montserrat for uppercase eyebrow text. Provide sensible local/system fallbacks; production use of remote fonts is undecided.
- **Weights:** the reference uses Bitter 600 for favorite titles and Inter/Montserrat weights 400–700 as specified in its font reference. Apply weight by hierarchy; other exact mappings are not established.
- **Sizing hierarchy:** known reference examples include 30px Bitter menu headings, 22px Bitter favorite titles, 18px descriptions/prices, 16px category links, and responsive hero sizing. A complete global scale is not specified.
- **Line height:** menu category links use 1.35; a complete typography line-height scale is not specified.
- **Letter spacing:** restrained heading spacing and uppercase eyebrow treatment; exact values are not specified.

### Spacing System

- Ordinary desktop section gutters use `clamp(36px, 7.5vw, 144px)`; mobile content gutters are 27px.
- Header/footer/home hero use narrower desktop gutters based on `calc(100% - clamp(36px, 5vw, 120px))`.
- Known reference spacing includes 32px desktop favorite-grid gap, approximately 20px favorite-row padding, a 48px menu-sidebar gap, and compact category/row spacing.
- A universal 4px/8px base scale and standard component padding have not been established; do not invent them as approved tokens.

### Texture & Atmosphere

- Favor warm, quiet surfaces and editorial imagery over dashboard-like card grids.
- The reference uses a subtle gradient in selected section backgrounds, restrained shadows, pale borders, and rounded controls. The Visit Us card has a 12px radius; other radii and shadow levels are not globally specified.
- Disabled-state and overlay transparency values are not specified.
- Remote Unsplash photography is sample stock imagery, not verified restaurant/dish photography; its production use remains undecided.

### Interactions

- Provide visible `:focus-visible` states, keyboard-operable controls, clear hover/selected states, and distinct loading, disabled, validation, error, and success feedback.
- Respect `prefers-reduced-motion`; the reference uses restrained hover image zoom that yields to reduced-motion preferences.
- Exact transition durations/easing are not specified.
- Search/filter feedback, if present, must expose updated result counts and an understandable empty state; exact search behavior for the production ordering interface remains a design detail.
- Pickup/order controls must not resemble a completed order until successful storage; deferred AI controls must not appear functional.

## Future Capabilities

- **Customer AI menu recommendations:** deferred beyond initial release. A later small model may use taste/spice preferences, dietary needs, budget, and group size to recommend only existing menu items. Customers may choose one or more suggestions individually—or none; suggestions are never added automatically. Model/deployment, data handling, allergy safeguards, and operational ownership are undecided.
- **Delivery, online payment, Square POS integration, customer email/text notifications, order-status lookup, and multiple staff roles/permissions:** deferred because they are outside the approved initial release.
- Responsive behavior and accessibility are initial-release expectations, not deferred capabilities.
