# Yuannan Tasty Garden menu preview

Reproduce `preview_01_menu.html` as a responsive, warm, modern restaurant menu. Use its embedded category and dish data as the content source, preserving names, prices, order, and category anchors. The preview contains 16 categories and 189 dishes. Header links are placeholders in this standalone preview.

## Visual system

- Fonts: Bitter 400/600 for headings and brand; Inter 400–700 for body, controls, and prices. Body is 15px/1.6, dark espresso `#2b211d`, on warm off-white `#f5f0e9`.
- Palette: burgundy `#6b1f2a`, deep burgundy `#48151d`, muted copper `#8c3e35`, pale border `#e4dacf`. Use generous whitespace and restrained borders.
- Header: 72px high, `#fffaf3`, fine bottom border; brand left and Our Story, Menu, Locations right. Constrain content to 1440px. On mobile use 60px height and smaller type.
- Intro: compact 108px minimum height, left-aligned eyebrow, “Our Menu” and “Explore the flavors of Yunnan, made for sharing and savoring.” White text over a left-to-right deep burgundy overlay and noodle photograph `https://images.unsplash.com/photo-1569718212165-3a8278d5f624?auto=format&fit=crop&w=1600&q=85`, cover, centered at 58%. Title `clamp(30px, 3vw, 40px)`; eyebrow 10px uppercase with .22em tracking; description 13px. Mobile minimum height 95px, 29px title, 12px description.

## Desktop layout

- Center content at max-width 1440px with 32px horizontal padding. Use a 220px navigation column, 48px gap, and flexible menu column. Start 32px below the intro.
- Navigation sticks 20px from viewport top, with max-height `calc(100vh - 40px)`. Keep heading and search visible while the category links scroll independently. Heading “Explore the menu” is 18px/1.25 Bitter 600 with 6px bottom margin.
- Search sits directly beneath the heading, 42px high, with a search icon left and an always-visible Clear button right. Use ivory `#fffcf8`, a fine `#ddd0c2` border, and a subtle copper focus ring.
- Category links are 13px with 9px vertical padding. Highlight the current category with burgundy bold text, a slim burgundy left edge, a pale warm gradient fading right, and a small northeast arrow at the right. Hover uses a slightly deeper warm tint. Track the category visible while scrolling.
- Menu sections are separated by 48px. Each category has a sticky heading at viewport top, 30px Bitter 600, burgundy, with 10px 12px padding and a warm gradient `#e9ddd2` on the left fading to page background on the right. A thin muted line extends from the heading. Place a small `−` or `+` immediately after the category name.
- Dish rows form two equal columns with a 48px gutter. Align dish name left and price right on the baseline. Use 14px names, 13px bold tabular prices, 15px vertical padding, and a fine bottom divider. On hover, give the row a white background extending 8px beyond its sides.

## Mobile at 700px and below

- Replace the sidebar with a sticky toolbar at the top of the viewport. Show a labeled category select and search side by side, with 10px gap and page-colored background. Keep both controls at least 42px high.
- Use 18px horizontal page padding, a single dish column, 25px category headings, and a sticky category heading offset of 85px below the toolbar. Use 95px scroll margin for category anchors.

## Behavior and accessibility

- Category links and the mobile selector jump to the corresponding section. Active desktop navigation uses `aria-current="location"`.
- Every section starts expanded. Clicking its heading toggles its dish list and the adjacent `−`/`+`. Use a real button with `aria-expanded` and `aria-controls`; retain collapsed state during search.
- Search filters immediately, case-insensitively, against decoded category titles, shortened navigation labels, and dish names. A category match shows all its dishes; a dish match shows matching rows within its category. Filter navigation links and mobile options to matching categories. Show a live dish count and an empty state when appropriate. Clear empties search, restores the full menu, and returns focus to the field. Keep desktop and mobile search values synchronized.
- Provide visible keyboard focus, semantic navigation and headings, accessible search and clear labels, and keyboard-operable controls.
