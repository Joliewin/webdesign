# Yuannan Tasty Garden — website recreation specification

## 1. Goal

Recreate the interactive, responsive restaurant website in `design/preview/preview-yunnan.html` as a self-contained HTML preview. It presents three hash-routed views—home, full menu, and Our Story—with a shared header and footer. The home page introduces the restaurant, showcases sample favorites, and provides visit information; the menu page makes the complete menu easy to browse and search.

This is a design preview, not a working ordering or AI service. Preserve its visible controls and existing behavior without inventing backend functionality.

## 2. References and source of truth

- **Primary visual and behavior reference:** `design/preview/preview-yunnan.html`. Open it locally and inspect the home page, `#menu`, and `#our-story` at desktop and mobile sizes. Its later CSS overrides earlier rules; reproduce the final rendered result, not unused legacy styles.
- **Full-menu content reference:** the `.menu-category` sections embedded in the primary HTML; also see `design/preview/options/preview_01_menu.html` and `design/preview/options/preview_01_menu.md` for the original menu dataset. Preserve the 16 categories, 189 dishes, prices, spelling, order, and `category-*` anchor IDs exactly. Do not replace them with invented data.
- **Business details and provenance:** `docs/yunnan/yunnan_info.md`. The address, phone, and hours are from third-party listings and should be confirmed before publication.
- **Header inspiration:** https://www.thirstycowbbq.com/ — its navigation overlays the hero image. Adapt the effect to the existing Yuannan branding; do not copy its branding or content.

## 3. Structure and content

### Shared header

- Sticky header overlays the hero with no visible separate bar or divider at the top. It contains a circular `雲` mark, **Yuannan Tasty Garden**, the caption **Flavors of Southwest China**, and links **Home**, **Menu**, **Our Story**, **Visit Us**, and outlined **Explore the Menu ↗**.
- On mobile, replace the inline links with a hamburger button opening a dark full-screen navigation panel.

### Home (`#home`)

1. **Hero:** full-height food photograph with dark left-to-right overlay. Eyebrow “A little taste of Yunnan”; heading “Come hungry. / Leave enchanted.”; copy “Bright herbs, warming spice, hand-pulled noodles, and the kind of dishes that bring everyone closer to the table.” Buttons: **Full Menu ↗**, **Your Favorites**, **Find Our Location**, **Order Now**.
2. **Favorites (`#favorites`):** heading **Your Favorites**, gradient **Let AI Decide ✦** button, outlined **View full menu ↗** button, and a divider. Under the divider are hanging category tabs: **All favorites**, **Noodles & soup**, **Small plates**, **From the wok**. A selected tab is burgundy with light text. The whole toolbar stays sticky under the site header while the user scrolls within this section and leaves naturally with the section.
3. **Favorite dishes:** two columns of horizontal, unboxed rows on desktop; one on mobile. Each row has a rounded square image, a name and price, a short description, and a small uppercase tag. Use the following sample content exactly, in this order:

   | Category | Dish and price | Description | Tag |
   | --- | --- | --- | --- |
   | Noodles & soup | Yunnan Crossing Bridge Noodles — $16 | A comforting signature bowl with rich broth, rice noodles, herbs, and bright accompaniments. | Guest favorite |
   | Small plates | House Handmade Dumplings — $12 | Delicate wrappers, savory filling, and a house dipping sauce with a little warmth. | Made by hand |
   | From the wok | Garden Wok Vegetables — $15 | Seasonal vegetables tossed over high heat with garlic, ginger, and a savory house sauce. | Plant-forward |
   | Noodles & soup | Spicy Yunnan Noodles — $15 | Springy noodles with chili fragrance, fresh greens, and a deeply savory finish. | A little fiery |
   | Small plates | Cool Cucumber & Herb Salad — $9 | Crisp cucumber, garden herbs, and a bright dressing to wake up the table. | Fresh & bright |
   | From the wok | Wok-Tossed House Special — $18 | Our kitchen’s savory, aromatic special—made for sharing and best eaten hot. | For the table |

   These favorites and their prices are **sample content**, not verified recommendations. Do not add `+` buttons or claim online ordering is operational.
4. **Visit Us (`#locations`):** a centered rounded two-column card on the same cream background as the favorites. Left: restaurant image with dark overlay, “Visit Us,” and “Bring your favorite people. We’ll take care of the rest.” Right: **Location**, `5115 Spring Mountain Road, Ste 103–105`, `Las Vegas, NV 89146`; **Opening hours**, `Daily · 11:00 a.m.–9:30 p.m.`, phone `(702) 826-4888`; burgundy **Get directions ↗** link to `https://www.google.com/maps/dir/?api=1&destination=5115+Spring+Mountain+Road+Ste+103-105%2C+Las+Vegas%2C+NV+89146`. Phone links to `tel:+17028264888`. Keep only a small gap above this section.

### Full menu (`#menu`)

- Compact noodle-photo banner with **Our Menu**, a light-colored **Let AI Decide ✦** button beside the title, and “Explore the flavors of Yunnan, made for sharing and savoring.”
- Desktop: sticky left sidebar titled **Explore the menu**, search input and persistent **Clear** button, and independently scrollable category links. Main area contains expandable category sections and dish rows in two columns.
- Category order and IDs: Appetizer (`category-appetizer`); Fried Rice/Noodle/Rice Noodle (`category-fried-rice-noodle-rice-noodle`); Rice Noodle/Noodle/Wonton (`category-rice-noodle-noodle-wonton`); Shrimp; Chicken & Duck; Beef & Lamb; Fish; From The Water; Pork; Spicy Boiled; Dry Pot; Vegetable; Soup; Rice; Drinks; Dessert. For the exact IDs of the remaining categories and all 189 dish names/prices, copy the embedded HTML data rather than generating IDs or rewriting content. Shorten the two long sidebar labels to **Fried Rice & Noodles** and **Noodles & Wonton** without changing section titles.
- Mobile: replace the sidebar with a sticky toolbar holding a labeled category select and synchronized search. Dish rows become one column.
- The search status is a live count, for example `1 dish found` or `3 dishes found`; show “No dishes or categories found. Try another search.” when appropriate.

### Our Story (`#our-story`)

- Full-height darkened photo hero with eyebrow **From Yunnan, with love**, title **One province. / A world of flavor.**, introductory text from the reference, and **Get to know us ↗** to `#story-details`.
- Follow with **Pull up a chair**, **Good food is even better together.**, the reference paragraph, **Explore the menu ↗**, and two overlapping food photos.
- Finish with a deep burgundy signoff, “Fragrant herbs. Warming spice. A place at our table.” and its reference copy. Hide the floating order button on this view.

### Shared footer and floating controls

- Compact deep-burgundy footer with the text brand **Yuannan Tasty Garden**, dynamic `© [current year] Yuannan Tasty Garden` beside it, and horizontal links **Our Story**, **The Menu**, **Visit Us**, **Email Us**, **Instagram ↗**. Wrap on small screens. Do not add the header icon, brand caption, footer description, divider, or bottom tagline.
- Preserve the preview link destinations: Email Us uses `mailto:hello@yuannantastygarden.com`; Instagram currently points to `#home` and is a placeholder, not a verified social link.
- Floating **Your Order** pill with icon and count `0` appears on home and menu, not Story. An equally sized **AI Decide ✦** pill sits above it on both home and menu, and is also hidden on Story. Both move upward when the footer enters the viewport so they do not obscure it; do not hide them at the footer.

## 4. Visual design

- **Mood:** warm, contemporary, inviting restaurant editorial—not a dashboard or rigid grid of boxed cards.
- **Colors:** burgundy `#6b1f2a`, deep burgundy `#48151d`, hover `#842d38`, orange `#d96b32`, cream `#fff4e5`, cream-deep `#f5e8d6`, espresso `#2b211d`, muted brown `#665750`, border `#e6d8c7`. Full menu background `#f5f0e9`, menu heading gradient `#e9ddd2` to `#f5f0e9`.
- **Typography:** Bitter for headings and brand; Inter for body, prices and controls; Montserrat for uppercase eyebrow text. Headings use restrained spacing and serif character; body is clean and readable.
- **Adaptive gutters:** ordinary section containers, Visit Us, and the menu layout use fluid left and right gutters of `clamp(36px, 7.5vw, 144px)` on desktop; at widths ≤700px their content gutters are 27px. The header, footer, and home hero intentionally have narrower gutters: their container width is `calc(100% - clamp(36px, 5vw, 120px))`. These areas expand on wide screens rather than being pulled into a centered 1200px column. Preserve the mobile menu toolbar's full-width background while aligning its controls with the 27px content gutter.
- **Header:** 78px tall on desktop, 70px at widths ≤700px. Transparent at the top, then near-opaque dark brown with subtle blur/shadow after 20px scroll.
- **Hero:** at least `100svh`, photo `cover`, content left-aligned with fluid gutters. Headline is `clamp(3rem, 5.9vw, 112px)`; at ≤700px use `clamp(2.8rem, 10vw, 4.5rem)`. Supporting text uses `clamp(15px, 1.25vw, 21px)`, with 15px on mobile. Dark overlay is primarily left-to-right. Do not add a fade over the bottom of the hero or change browser zoom.
- **Favorites toolbar:** starts beneath a 48px warm-tan space on desktop, 32px mobile; toolbar has a full-viewport-width gradient from `#d3b6a4` through `#ead7c5` to `#fff4e5`, with no visible side edge. The sticky toolbar has a divider above the tabs. Buttons are rounded pills; AI button uses a burgundy-to-copper gradient and circular sparkle badge. Both action button labels and hanging filter labels are 18px; the selected filter has a burgundy fill. The action buttons and filters must remain visually distinct.
- **Favorite rows:** 145px square rounded images on desktop, 110px mobile, `object-fit: cover`; desktop grid gap 32px, row padding approximately 20px, subtle bottom border. Titles are Bitter 600 at 22px; prices are 18px bold/tabular; descriptions are 18px muted; uppercase tags are 14px. Hover slightly zooms the image, respecting reduced motion.
- **Visit card:** use the ordinary adaptive section gutters above, two equal columns, 12px radius, pale border, restrained shadow; photo panel min-height approximately 360px with text at bottom. On mobile stack the panels, use 27px outer margins and a roughly 220px image panel.
- **Menu:** full-width layout with adaptive section gutters above, 220px sidebar and 48px gap; sidebar sticks 98px below viewport top, with separately scrolling category links and visible search. Sidebar links use 16px text, `line-height: 1.35`, and compact 3px vertical padding. Section headings stick under the 78px header; use 30px Bitter, warm left-to-right background, and a thin line. Compact category separation around 28px and dish rows with 10px vertical padding. Menu search is a 44px ivory rounded field with search icon, Clear action, and copper focus ring.
- **Mobile ≤700px:** header 70px; menu toolbar sticks below it, category headings approximately 155px from the viewport top and category anchors have enough scroll margin to remain visible. Use single-column dishes. Favor readable wrapping and avoid horizontal page overflow.

## 5. Interactions and states

- Header changes from transparent to dark after scrolling; mobile menu opens/closes with correct expanded label/state, closes on navigation and Escape, and locks page scrolling while open.
- Hash navigation switches views without a server: `#menu` opens the full menu, `#our-story` opens Story, `#home` opens home, `#favorites` and `#locations` target the home sections, and `#category-*` addresses menu sections. Support direct links and browser back/forward.
- Home **Full Menu**, **View full menu**, header menu links, and **Order Now** currently route to `#menu`; **Order Now** is not a connected checkout. **Your Favorites** and **Find Our Location** scroll to their respective home sections.
- Favorites filters update `aria-selected`, immediately show the relevant cards, and hide nonmatches. All favorites restores all six. Left/right arrow keys move between and activate tabs.
- Every full-menu category starts expanded. Its real heading button toggles the dish list, `aria-expanded`, `aria-controls`, and `−`/`+` indicator. Preserve collapsed state while filtering.
- Search filters immediately and case-insensitively against decoded category titles, shortened category labels, and dish names. Matching a category shows all its dishes; matching a dish shows only matching rows. Hide unmatched sections and sidebar links, update mobile options and the live result count, and show the empty state when necessary. Synchronize desktop and mobile search values. Clear empties both and returns focus to the initiating field.
- Highlight the current visible category with `aria-current="location"`, a left border, pale gradient, and arrow; automatically scroll the sidebar list to keep the active item visible. Selecting a mobile option scrolls to its section. Anchor offsets must account for the document's scroll padding and sticky controls so that selecting Chicken & Duck highlights Chicken & Duck, not Shrimp; the current desktop category scroll margin is 0 and mobile is 95px.
- `Let AI Decide` / `AI Decide` buttons are **visual placeholders**, with no AI implementation or claim of working functionality. The order pill currently only shows an informational toast; there are no dish-add buttons or connected checkout. Preserve these limitations rather than inventing behavior.
- Fixed order and floating AI controls move up by the visible portion of the footer plus their usual viewport gap; recalculate on scroll and resize. Update the copyright year dynamically.

## 6. Assets

Use the same remote assets as the preview; no local image assets are required. They are stock visuals, not verified photos of the restaurant or dishes.

- Fonts: `https://fonts.googleapis.com/css2?family=Bitter:wght@400;500;600;700&family=Inter:wght@400;500;600;700&family=Montserrat:wght@500;600;700&display=swap`.
- Home hero: `https://images.unsplash.com/photo-1563245372-f21724e3856d?auto=format&fit=crop&w=2200&q=88`.
- Menu hero: `https://images.unsplash.com/photo-1569718212165-3a8278d5f624?auto=format&fit=crop&w=1600&q=85`.
- Visit photo: `https://images.unsplash.com/photo-1517248135467-4c7edcad34c4?auto=format&fit=crop&w=1200&q=85`.
- Favorite photos in table order, each URL using `?auto=format&fit=crop&w=900&q=82`: `https://images.unsplash.com/photo-1569718212165-3a8278d5f624`, `https://images.unsplash.com/photo-1563245372-f21724e3856d`, `https://images.unsplash.com/photo-1512058564366-18510be2db19`, `https://images.unsplash.com/photo-1555126634-323283e090fa`, `https://images.unsplash.com/photo-1547592180-85f173990554`, `https://images.unsplash.com/photo-1515003197210-e0cd7184f8b5`.
- Story hero: `https://images.unsplash.com/photo-1547928576-965be7f5f6a4?auto=format&fit=crop&w=2200&q=88`. Story photo pair uses the same photo at `w=1000&q=85` and the menu noodle photo at `w=700&q=85`.
- Icons are text/CSS: `雲`, `↗`, `✦`, `♧`, hamburger lines, and a CSS-drawn magnifying glass. Use font fallbacks if remote fonts fail. Loading remote assets requires network access.

## 7. Technical requirements

- Deliver semantic HTML5 with embedded CSS and vanilla JavaScript; no build step, framework, server, API key, or external JS library. It must work when opened using `file://`.
- Preserve full menu data and anchors from the reference instead of truncating or replacing them. Keep all section content, visible text, and price formatting faithful to the reference unless explicitly identified here as a placeholder.
- Use native buttons, links, inputs, select, semantic nav/headings, and the `hidden` attribute. Keep hashes, history navigation, search, collapsed states, sticky offsets, footer avoidance, and responsive layouts functional.
- Target current Chrome, Edge, Firefox, and Safari, desktop and mobile. Use sensible font and viewport fallbacks and avoid horizontal overflow.
- Do not add menu disclaimer text or favorite add-to-order buttons; do not pretend sample menu content or third-party restaurant details are verified.

## 8. Accessibility

- Provide a single visible main view with sensible heading hierarchy, descriptive image alt text, named navigation landmarks, and labels for search, Clear, mobile category select, hamburger, and order count.
- Use `aria-expanded`/`aria-controls` for the mobile navigation and collapsible menu sections; `aria-selected` for favorite tabs and `aria-current="location"` for the active menu category.
- All controls must be keyboard accessible, with visible `:focus-visible` styles. Preserve arrow-key navigation for the favorites tabs, Escape to close the mobile nav, and focus restoration after clearing search.
- Use a polite live region for search result counts and the order toast. Ensure sufficient text/control contrast against photos and gradients, and respect `prefers-reduced-motion`.
- Keep sticky controls from covering section headings and anchor targets; ensure mobile controls remain usable at narrow widths and zoom.

## 9. Acceptance criteria

- [ ] Home, `#menu`, `#our-story`, direct category anchors, and browser history work when the file is opened locally.
- [ ] Header overlays each hero without a separate initial bar and changes to a readable dark sticky header on scroll; mobile navigation works.
- [ ] Home has four hero actions, sticky Favorites controls, six sample dishes with correct filters, and the Visit Us card with a working maps directions link.
- [ ] Favorite images are square and positioned beside text; desktop has two columns and mobile one; no `+` buttons appear.
- [ ] Full menu contains all 16 categories and 189 dishes from the reference with unchanged order, anchors, names, and prices.
- [ ] Search, clear, count, empty state, mobile selector, expandable headings, active tracking, and automatic sidebar scrolling work; clicking Chicken & Duck highlights the correct category.
- [ ] AI controls are present but do not simulate working AI; the order control does not imply a connected checkout.
- [ ] Floating AI Decide and Your Order controls appear on both home and menu, remain matched in size, and stay above the footer rather than covering footer links.
- [ ] Footer is compact and horizontal where space permits; it includes the dynamic copyright and no extra description or divider.
- [ ] Section gutters and hero type adapt to different viewport sizes; header, footer, and home hero use narrower gutters than other sections. Layout is usable at desktop and mobile widths, keyboard focus is visible, and reduced-motion preferences are respected.
