# Vision — Yunnan Tasty Garden

## Problem
Customers need a convenient way to browse Yunnan Tasty Garden’s full menu and submit pickup orders online. The restaurant needs a simple way to receive and manage those orders and keep menu items, prices, spice levels, and add-ons current without editing code.

## Users
- **Customers:** Browse the menu, customize applicable dishes, choose ASAP or scheduled pickup, submit an order, and receive a confirmation number.
- **Restaurant staff:** Sign in to view incoming orders and update their status.
- **Admins:** Maintain menu items, prices, and dish-specific options through a private interface.

## Success
- The ordering flow reliably accepts and records pickup orders, with a confirmation number shown to the customer.
- Staff can manage order status and admins can maintain the menu through protected interfaces.
- The site supports a target of **20 online pickup orders per week**.

## Non-Goals
- Delivery.
- Online payment at initial launch.
- Square POS integration at initial launch.
- Customer email/text notifications or order-status lookup.
- Multiple staff roles and permissions.
- Customer-facing AI recommendations in the initial release. A later release may deploy a small AI model that uses customer preferences—taste/spice preferences, dietary needs, budget, and group size—to suggest a selection from existing menu items. Customers can choose one or more suggested dishes individually, or none, to add to their order; they are not required to accept the entire selection. The AI does not create or publish new menu items. Model choice and deployment approach remain undecided.

## Constraints
- Use the public-facing name **Yunnan Tasty Garden**.
- Offer the full menu for pickup. Spice levels and add-ons apply only to dishes configured with those options; exact dish-level option data remains to be provided.
- Pickup may be ASAP or scheduled. Scheduled times use 15-minute slots, require at least 30 minutes’ notice, and allow at most 8 orders per slot.
- Intended ordering hours are daily, 11:00 a.m.–9:30 p.m. local time. Exact handling of the last available slot and order cutoff remains to be defined.
- An order is accepted when submitted, stored in a backend database, and acknowledged with an on-site confirmation number. No online payment is taken.
- Protect order submission from accidental duplicates and abuse using server-side controls. Do not impose a blanket one-order-per-IP-per-15-minutes rule; specific detection signals and thresholds remain to be designed.
- Checkout requires customer name and phone number; email and order notes are optional.
- Staff order management and admin menu management require private, basic-login interfaces. More detailed roles and permissions are deferred.
- Square is currently used for in-store POS only; the initial website order flow must not imply Square receives orders.
- Address, phone, and other business details in `docs/yunnan/yunnan_info.md` come from third-party listings and require restaurant confirmation before publication. Hosting, technology, browser support, accessibility requirements, and verified menu content remain undecided.
