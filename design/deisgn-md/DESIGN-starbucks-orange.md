# Restaurant Design System — Starbucks-Inspired Structure

## 1. Visual Theme & Atmosphere

A warm, confident restaurant experience built on the same clean café rhythm as the reference Starbucks system, recolored for an appetizing, intriguing dining brand. Warm cream and white surfaces keep the experience welcoming; deep burgundy brings richness and appetite; burnt orange adds lively energy to food imagery and calls to action; espresso anchors text and dark feature bands. Sage is a restrained freshness cue for ingredients, dietary notes, and subtle utility states.

The system favors generous whitespace, confident typography, rounded geometry, and clear color-block sections. Food photography—not decoration—provides the strongest appetite appeal. Cream hero → white menu/content sections → burgundy feature band → cream utility sections → burgundy footer creates a warm, memorable page rhythm.

**Key Characteristics**
- Deep burgundy is the restaurant’s signature brand color; burnt orange is the energetic action accent.
- Warm cream replaces cool gray as the primary page canvas.
- Espresso is the default text color for comfortable contrast on warm surfaces.
- Sage appears sparingly as a freshness cue, never competing with food photography.
- Full-pill buttons, rounded cards, soft layered shadows, and generous spacing carry over from the reference.
- Use high-quality, natural-light food photography with close crops, visible texture, and warm tonal balance.
- No decorative gradients; use solid color blocks and photography for depth.

## 2. Color Palette & Roles

### Primary Brand Colors

- **Deep Burgundy** (`#6B1F2A`): Signature brand color. Use for major headings, dark feature bands, footer, and important brand moments.
- **Burgundy CTA** (`#6B1F2A`): Primary filled-action color. White text; use for “Order now,” “Reserve a table,” and other conversion actions.
- **Warm Burgundy** (`#842D38`): Hover and active treatment where a lighter interaction shade is needed.
- **Burgundy Deep** (`#48151D`): Dark band/footer shade and high-emphasis dark surface.
- **Burnt Orange** (`#D96B32`): Secondary accent for links, badges, menu highlights, prices, and occasional secondary CTAs.
- **Sage Green** (`#74856A`): Optional restrained accent for freshness, ingredient labels, vegetarian indicators, and subtle supportive details.

### Surface & Background

- **Warm Cream** (`#FFF4E5`): Primary page canvas and warm section backgrounds.
- **Cream Deep** (`#F5E8D6`): Alternate section surface and subtle separators.
- **White** (`#FFFFFF`): Cards, menus, modals, and form surfaces.
- **Espresso** (`#2B211D`): Dark text and dark utility surfaces.

### Text

- **Primary Text** (`#2B211D`): Headlines and body text on cream or white.
- **Secondary Text** (`#665750`): Descriptions, captions, and metadata on light backgrounds.
- **Text on Burgundy** (`#FFFFFF`): Primary text and icons on burgundy surfaces.
- **Soft Text on Burgundy** (`rgba(255,255,255,0.76)`): Supporting copy on dark bands.

### Semantic Colors

- **Success / Fresh** (`#74856A`): Success states and ingredient/freshness indicators.
- **Warning** (`#D96B32`): Attention and limited-time notices.
- **Error** (`#B3261E`): Validation and destructive states; keep distinct from the brand burgundy.
- **Input Border** (`#D8C9B8`): Quiet form outlines and separators.

### Color Usage Rules

- Keep warm cream as the dominant canvas; use white for individual content cards.
- Burgundy is the primary brand signal and the preferred high-contrast CTA.
- Burnt orange is an accent, not a second dominant background color. Use it in small, intentional doses.
- Sage should occupy only a small fraction of the interface and should not be used for primary actions.
- On burgundy or espresso surfaces, use white text and verify contrast for all text sizes.
- Avoid using burgundy and burnt orange together for adjacent small text; maintain clear visual separation.

## 3. Typography Rules

### Font Family

- **Primary:** `Manrope, "Helvetica Neue", Arial, sans-serif` — warm, clean, highly legible interface type.
- **Fallback:** `"Helvetica Neue", Helvetica, Arial, sans-serif`.
- **Editorial accent:** `Lora, Georgia, serif` — optional for a small number of menu-story or chef-feature headlines.

Keep the serif localized to editorial moments. Navigation, ordering, menu details, forms, and buttons remain sans-serif.

### Hierarchy

| Role | Size | Weight | Line Height | Letter Spacing | Notes |
|------|------|--------|-------------|----------------|-------|
| Display | 80px | 500–700 | 1.1–1.2 | `-0.02em` | Large campaign or hero headline |
| Jumbo | 58px | 500–700 | 1.15 | `-0.02em` | Secondary hero headline |
| Hero | 44px | 600–700 | 1.2 | `-0.02em` | Landing-section heading |
| H1 | 32px | 700 | 1.2 | `-0.02em` | Page title |
| H2 | 24px | 600 | 1.35 | `-0.01em` | Section title |
| Body Large | 19px | 400–500 | 1.65 | normal | Hero and feature-band copy |
| Body | 16px | 400 | 1.5 | normal | Default body and menu description |
| Small | 14px | 400–600 | 1.5 | normal | Metadata, labels, button text |
| Micro | 12px | 500 | 1.4 | `0.02em` | Dietary labels and fine print |

### Principles

- Use weight and color to establish hierarchy before adding more type sizes.
- Keep body copy espresso-colored on light backgrounds; avoid pure black.
- Use uppercase sparingly for short labels, with modest tracking.
- Ensure menu names, prices, and dietary details remain easy to scan.

## 4. Component Stylings

### Buttons

**Primary Filled**
- Background: Deep Burgundy (`#6B1F2A`)
- Text: White (`#FFFFFF`)
- Border: `1px solid #6B1F2A`
- Radius: `50px`
- Padding: `12px 24px` (minimum 44px touch height)
- Font: Manrope, 15–16px, weight 700
- Hover: Burgundy Warm (`#842D38`)
- Active: `transform: scale(0.97)`
- Transition: `all 0.2s ease`

**Secondary Outlined**
- Background: transparent
- Text and border: Deep Burgundy (`#6B1F2A`)
- Same pill radius and padding as primary
- Hover: light burgundy tint (`rgba(107,31,42,0.07)`)

**Accent**
- Background: Burnt Orange (`#D96B32`)
- Text: White
- Use selectively for limited-time offers or secondary emphasis, not every CTA.

**Inverted on Dark**
- Background: White
- Text: Deep Burgundy
- Use as the primary action on a burgundy feature band.
- Secondary action: transparent with a 1px white border and white text.

**Floating Order Button**
- Background: Deep Burgundy
- Icon: White shopping bag or plate-and-cutlery mark
- Size: `56px` diameter; `40px` mini variant
- Radius: `50%`
- Fixed bottom-right with a comfortable mobile safe-area offset
- Shadow: `0 0 6px rgba(43,33,29,0.22), 0 8px 14px rgba(43,33,29,0.16)`
- Active: scale to `0.95`

### Cards & Containers

**Menu Item Card**
- Background: White
- Radius: `12px`
- Shadow: `0 0 1px rgba(43,33,29,0.14), 0 2px 6px rgba(43,33,29,0.10)`
- Image: 4:3 or square crop, natural light, consistent aspect ratio
- Content: dish name, concise description, price, optional dietary tags
- Keep card copy concise and avoid placing text over busy photography.

**Editorial / Chef Feature Card**
- Background: Warm Cream (`#FFF4E5`)
- Radius: `12px`
- Use a large food or chef photograph with a short story and one clear action.

**Offer Badge**
- Background: Burnt Orange (`#D96B32`)
- Text: White
- Small pill or compact rounded rectangle
- Reserve for genuine specials, seasonal menus, or limited-time offers.

**Dietary Tags**
- Vegetarian / fresh tag: Sage (`#74856A`) with white text, or a pale sage background with espresso text.
- Allergens: neutral cream or white surface with espresso text.
- Do not rely on color alone; include readable text or an icon.

**Modal**
- White background, `12px` radius, `24px` padding
- Soft layered shadow; clear close control and visible focus states.

### Inputs & Forms

- White field surface with `1px solid #D8C9B8` border and `8px` radius.
- Label: 14px, weight 600, espresso.
- Focus: 2px burgundy outline or border, with visible keyboard focus ring.
- Valid state: subtle pale-sage tint.
- Invalid state: pale red tint and explicit error message.
- Inputs and controls should be at least 44px tall on touch devices.

### Navigation

**Global Nav**
- Fixed or sticky top bar; white or warm-cream background.
- Height: approximately `72px` mobile and `88px` desktop.
- Soft shadow: `0 2px 8px rgba(43,33,29,0.08)`.
- Left: restaurant wordmark.
- Main links: Menu · Our Story · Locations (or Reservations).
- Right: location/reservation utility plus a prominent burgundy “Order” pill.

**Mobile Nav**
- Collapsed hamburger drawer below tablet width.
- Keep the order action prominent and reachable.
- Floating order button may persist where it does not obscure content or consent controls.

### Image Treatment

- **Hero photography:** Close, tactile food photography with warm natural light; use an asymmetric split layout, roughly 40% image / 60% copy.
- **Menu photography:** Consistent crop ratios and lighting across menu items; show ingredients and texture clearly.
- **People and place:** Use candid hospitality photography to communicate warmth and atmosphere.
- **Avoid:** Generic stock-photo collages, excessive filters, artificial saturation, and text over visually busy images.
- Images fade in with `opacity 0.3s ease-in`; preserve aspect ratios and use intentional `object-position`.

### Feature Band

Full-width Deep Burgundy (`#6B1F2A`) section:
- White headline and body copy; supporting copy at `rgba(255,255,255,0.76)`.
- Pair with appetizing food photography or a restaurant interior.
- Primary CTA: white-filled pill with burgundy text.
- Secondary CTA: outlined white pill.
- Split ratio around 40/60 or 50/50; stack image and copy on mobile.

### Menu Detail / Dish Page

- Breadcrumb above title in secondary text.
- Dish title, price, and concise description grouped together.
- Prominent dish photography, not hidden below long copy.
- Dietary/allergen notes appear near the dish details, not only in a footer.
- Add-to-order action uses the burgundy primary pill.
- Related dishes may use the standard menu card.

## 5. Layout Principles

### Spacing System

Use a 4px-based scale, with 16px as the default rhythm:

| Token | Pixels | Typical Use |
|-------|--------|-------------|
| `--space-1` | 4px | Tight inline spacing |
| `--space-2` | 8px | Compact gaps |
| `--space-3` | 16px | Default card padding and mobile gutter |
| `--space-4` | 24px | Section inner spacing |
| `--space-5` | 32px | Card groups and content blocks |
| `--space-6` | 40px | Desktop gutters and large gaps |
| `--space-7` | 48px | Section spacing |
| `--space-8` | 56px | Large breathing space |
| `--space-9` | 64px | Major section padding |

### Grid & Container

- Content max width: approximately `1280–1440px`.
- Standard desktop content: 12-column grid with generous gutters.
- Hero: asymmetric 40/60 image/content split on desktop; stacked on mobile.
- Menu: 3–4 columns on desktop, 2 on tablet, 1 on narrow phones.
- Keep text measures comfortable; avoid overly wide paragraph columns.

### Whitespace Philosophy

Use generous `40–64px` section padding on desktop and `24–40px` on mobile. Separate content through whitespace and background changes rather than heavy dividers. Let food photography have room to breathe.

### Border Radius

| Value | Use |
|-------|-----|
| `8px` | Inputs and compact controls |
| `12px` | Cards, modals, menu tiles |
| `50px` | Pill buttons and badges |
| `50%` | Circular icons and floating order button |

## 6. Depth & Elevation

| Level | Treatment | Use |
|-------|-----------|-----|
| Card | `0 0 1px rgba(43,33,29,0.14), 0 2px 6px rgba(43,33,29,0.10)` | Menu and feature cards |
| Navigation | `0 2px 8px rgba(43,33,29,0.08)` | Sticky header |
| Floating CTA | `0 0 6px rgba(43,33,29,0.22), 0 8px 14px rgba(43,33,29,0.16)` | Persistent order action |

Use soft, layered shadows. Burgundy and cream color blocks establish most of the depth; avoid heavy shadows and decorative gradients.

## 7. Do's and Don'ts

### Do
- Use `#FFF4E5` as the warm page canvas and white for content cards.
- Use `#6B1F2A` consistently for brand moments and primary actions.
- Use burnt orange `#D96B32` sparingly for lively accents and special offers.
- Keep sage `#74856A` to subtle freshness and dietary details.
- Use espresso `#2B211D` for readable text on light surfaces.
- Give food photography prominent placement and consistent crops.
- Keep buttons pill-shaped with clear hover, active, and focus states.
- Ensure important menu and allergen information is text-readable.

### Don't
- Don't turn every section burgundy or orange; the warm cream canvas is essential.
- Don't use orange as the default for every button or link.
- Don't use sage for primary conversion actions.
- Don't overlay small text on busy food imagery.
- Don't use color alone to communicate dietary or allergen status.
- Don't add gradients, heavy shadows, or excessive decorative flourishes.
- Don't sacrifice readable contrast for a moodier aesthetic.

## 8. Responsive Behavior

### Breakpoints

| Name | Width | Key Changes |
|------|-------|-------------|
| Mobile | `< 480px` | Compact nav, single-column menu, full-width primary action where useful |
| Tablet | `480–767px` | Two-column menu grid, reduced section padding |
| Small desktop | `768–1023px` | Hero split begins; two or three menu columns |
| Desktop | `1024–1439px` | Full hero split, three or four menu columns |
| Wide | `1440px+` | Content width capped; additional outer breathing space |

### Touch & Collapse

- Make interactive controls at least 44px tall.
- Stack hero image and copy on mobile; keep the headline and order action visible early.
- Collapse menu grids to one column on narrow phones and two columns at larger mobile widths.
- Keep navigation actions reachable without crowding the header.
- Account for safe areas when positioning a floating order button.

## 9. Agent Prompt Guide

### Quick Color Reference

- Primary CTA / brand: Deep Burgundy (`#6B1F2A`)
- CTA hover: Warm Burgundy (`#842D38`)
- Deep band/footer: Burgundy Deep (`#48151D`) or Deep Burgundy (`#6B1F2A`)
- Accent / special offer: Burnt Orange (`#D96B32`)
- Freshness accent: Sage Green (`#74856A`)
- Page canvas: Warm Cream (`#FFF4E5`)
- Alternate surface: Cream Deep (`#F5E8D6`)
- Card surface: White (`#FFFFFF`)
- Primary text: Espresso (`#2B211D`)
- Secondary text: `#665750`
- Text on dark: White (`#FFFFFF`)

### Example Component Prompts

1. “Create a restaurant primary CTA pill with Deep Burgundy (`#6B1F2A`) background, white ‘Order now’ text, Manrope 16px weight 700, `50px` radius, and `12px 24px` padding. Use Warm Burgundy (`#842D38`) on hover and a visible keyboard focus ring.”

2. “Design a menu-item card on a Warm Cream (`#FFF4E5`) page canvas. Use a white `12px` rounded card, soft layered shadow, appetizing 4:3 food photography, dish name, concise description, price, and optional readable dietary tags.”

3. “Build a burgundy feature band with Deep Burgundy (`#6B1F2A`) background, white headline, soft white supporting copy, food photography, and a white-filled primary pill with burgundy text. Stack image and content below 768px.”

4. “Create a seasonal special badge in Burnt Orange (`#D96B32`) with white text. Keep it compact and use it only for a genuine featured or limited-time menu item.”

5. “Design a restaurant hero on Warm Cream (`#FFF4E5`) with a 40/60 image-and-copy split, natural-light close-up food photography, espresso body text, burgundy headline, and a prominent burgundy ‘Reserve a table’ action.”

### Iteration Guide

1. Refine one component at a time.
2. Use the named color roles and exact hex values in this document.
3. Preserve the cream/white/burgundy surface rhythm.
4. Keep orange and sage accents restrained.
5. Check text contrast, touch target size, and mobile image crops.
6. Let real food photography provide the appetite appeal.
