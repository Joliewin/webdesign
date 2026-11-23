# Thirsty Cow Korean BBQ — Warm Restaurant Colorway

**Basis:** Thirsty Cow homepage structure and published CSS, restyled with the color system in [`DESIGN-starbucks-orange.md`](DESIGN-starbucks-orange.md). This is a colorway adaptation, not a claim about the current live site's colors. Layout, content, typography, photography, and motion remain grounded in the Thirsty Cow design reference; colors are intentionally replaced with the warm restaurant palette.

## 1. Visual Theme & Atmosphere

Keep Thirsty Cow's premium, photo-led Korean BBQ experience—cinematic hero slideshow, editorial serif headlines, meat carousel, feature cards, award moment, and location storytelling—but warm the visual identity. Warm cream and white provide welcoming breathing room; deep burgundy anchors brand moments and key actions; burnt orange adds appetite and energy; espresso replaces charcoal as the main dark text and feature-band color. Sage stays a restrained freshness cue.

The adapted page rhythm is: full-bleed photography hero with dark photo overlay → warm-cream experience section and photo cards → cream/white meat showcase → burgundy editorial feature band → warm award moment → cream location area with photo cards → espresso/burgundy footer. Keep dark photographic overlays only where needed for white text legibility; they are image treatments, not large solid charcoal surfaces.

**Key Characteristics**
- Thirsty Cow's existing hierarchy and image-led composition remain intact.
- Warm Cream (`#FFF4E5`) becomes the primary canvas; White (`#FFFFFF`) supports clean content panels.
- Deep Burgundy (`#6B1F2A`) is the signature brand color and primary CTA.
- Burnt Orange (`#D96B32`) is a selective accent for highlights, labels, and special moments.
- Espresso (`#2B211D`) anchors text and occasional deep sections; sage (`#74856A`) is subtle.
- Retain Bitter display headlines, Montserrat eyebrow labels, and Inter body copy from the source design.
- Use food and venue photography as the primary visual texture; do not add decorative gradients.

## 2. Color Palette & Roles

### Brand Colors

- **Deep Burgundy** (`#6B1F2A`): Brand headline/accent, primary CTA, key feature bands, and footer.
- **Warm Burgundy** (`#842D38`): CTA hover and active color.
- **Burgundy Deep** (`#48151D`): Deep feature/footer surface when stronger contrast is needed.
- **Burnt Orange** (`#D96B32`): Secondary accent for small labels, highlighted details, and award/special callouts.
- **Sage Green** (`#74856A`): Restrained freshness accent; use sparingly.

### Surfaces

- **Warm Cream** (`#FFF4E5`): Main page canvas and open content sections.
- **Cream Deep** (`#F5E8D6`): Alternate section background and soft separators.
- **White** (`#FFFFFF`): Cards, clean content panels, and inverted CTA surfaces.
- **Espresso** (`#2B211D`): Main text color and optional dark feature/footer surface.
- **Photo Overlay** (`rgba(0,0,0,0.45–0.75)`): Image-only overlay range to protect legibility; retain source-style black overlays on photography as needed.

### Text & Borders

- **Primary Text** (`#2B211D`): Headlines and body copy on cream/white.
- **Secondary Text** (`#665750`): Captions, supporting copy, and metadata on light surfaces.
- **Text on Burgundy/Espresso** (`#FFFFFF`): High-priority text and icons on dark color blocks.
- **Soft Text on Dark** (`rgba(255,255,255,0.76)`): Secondary copy over burgundy or espresso.
- **Input / Divider Border** (`#D8C9B8`): Quiet outlines on light surfaces.
- **Photo-card border:** Use a subtle cream/white translucent border, e.g. `rgba(255,255,255,0.48)`, over darkened photography.

### Color Usage Rules

- Keep cream and white as the dominant surfaces; burgundy is the strong brand punctuation.
- Use burnt orange in small doses rather than as a full-page background or default button color.
- Sage is not a primary CTA color.
- On cream and white, use espresso text; on burgundy/espresso, use white.
- Preserve black photo overlays when photographs need contrast; avoid replacing image overlays with opaque burgundy tints.
- Do not use adjacent burgundy and orange for small text without sufficient separation.

## 3. Typography Rules

Typography is retained from the Thirsty Cow source design; the palette change does not change the brand's editorial voice.

### Font Families

- **Body / general UI:** `Inter, Arial, Helvetica, sans-serif`.
- **Theme heading fallback:** `Quicksand, Arial, Helvetica, sans-serif`, bold, uppercase, tracked.
- **Homepage editorial headings:** `Bitter`, typically medium weight and capitalized.
- **Eyebrow labels:** `Montserrat`, 12px, weight 600, uppercase, `0.18em` tracking.
- `Cormorant Garamond` and `Playfair Display` are loaded/configured in the theme kit but are not the principal homepage display face.

### Hierarchy

| Role | Size | Weight | Line Height | Treatment |
|------|------|--------|-------------|-----------|
| Hero headline | 88px desktop; 72px tablet; 48px mobile | 500 | `0.95em` | Bitter, Espresso on cream or white over image overlay |
| Main section headline | 60px desktop; 36px mobile | 500 | Default / compact mobile | Bitter, espresso on light; white on dark |
| Large editorial headline | 72px desktop; 36px mobile | 500 | Default / `1em` mobile | Bitter |
| Feature-card title | 30px | 400–500 | Theme default | Bitter, white over photography |
| Eyebrow | 12px | 600 | — | Montserrat, uppercase, `0.18em` tracking; burnt orange or burgundy |
| Body copy | 16px | 400 | `1.7` | Inter; hero source uses Montserrat at 16px |
| Feature-card copy | 14px | 400 | — | Montserrat, white/soft white over image |
| Theme heading fallback | h1 36.9px; h2 33.5px; h3 30.5px | 700 | `1.4` | Quicksand, uppercase, `0.1em` tracking |

### Principles

- Keep oversized Bitter headlines as the editorial focal point.
- Use burnt orange or burgundy for small tracked eyebrow labels on light surfaces.
- On burgundy bands, use white headlines and soft-white supporting text.
- Keep body copy espresso-colored on cream/white; muted brown (`#665750`) for secondary text.
- Continue to use black photo overlays behind white card labels.

## 4. Component Stylings

### Header & Navigation

- Brand logo image at approximately `150px` maximum width.
- Retain the static/transparent-over-hero header and theme auto-hide behavior.
- Desktop links: Home · Menu (location submenu) · Bar · About · Location.
- Mobile navigation retains hamburger and close controls.
- Over the hero, retain the photo-aware transparent header and light logo/nav for contrast.
- On light content sections, use espresso or burgundy navigation text; use a cream/white header surface only if the header transitions away from the hero.

### Buttons

**Primary Hero CTA — “View Menu”**
- Background: Deep Burgundy (`#6B1F2A`)
- Text/icon: White
- Border: `1px solid #6B1F2A`
- Padding: `16px 28px`; retain source button proportions
- Right-arrow icon alongside label
- Hover/focus: Warm Burgundy (`#842D38`)
- Active: subtle `scale(0.97)`; transition around `0.2s ease`

**Feature CTA**
- On cream/white: transparent background, `2px solid #6B1F2A`, burgundy label.
- On burgundy/espresso: transparent background, `2px solid #FFFFFF`, white label.
- Padding: `16px 28px`.
- Hover: fill with burgundy on light surfaces; use white-filled/burgundy-text inversion on dark surfaces.

**Location CTA**
- Low-chrome text action with right-arrow affordance.
- Over photography: white label with dark overlay behind.
- On hover/focus, change to Burnt Orange (`#D96B32`) rather than the source's yellow.

### Photo Feature Cards

- Three-card desktop grid: Premium Meats, The Bar, The Experience.
- Approximate heights: `478px` desktop, `400px` tablet, `370px` mobile.
- Full-bleed photography and dark image overlay remain essential for legibility.
- Thin translucent-white border; content anchored to bottom with approximately `28px` desktop / `20px` mobile inset.
- Background image zooms to `scale(1.1)` over `0.5s`; maintain overlay during hover.
- Heading: Bitter 30px, white. Description: Montserrat 14px, soft white.
- Place the group on Warm Cream or Cream Deep rather than a solid charcoal section.

### Meat Image Carousel

- One image per slide across the existing 31-image premium meat, seafood, sides, and soup sequence.
- Keep autoplay (~3s), infinite loop, 500ms transition, lazy loading, and previous/next arrows.
- Place on a Warm Cream (`#FFF4E5`) or White content section.
- Pair with an editorial text block: burgundy/orange eyebrow, espresso headline, secondary brown description, and burgundy outlined CTA.
- Retain original wide food-photo format and avoid enclosing each slide in a generic menu card.

### Location Cards

- Two-column photo-led layout: Garden Grove and City of Industry.
- Approximate heights: `500px` desktop, `400px` tablet, `370px` mobile.
- Keep darkened photography and white title/action near the bottom.
- Use a cream/white translucent fine border.
- Place the cards within cream/white section surfaces; do not put opaque cream overlays over the photos.
- Each card continues to link to its location-specific menu.

### Location Details

- Display each venue's address, phone, and day-by-day hours in clearly separated groups.
- Use espresso headlines and text on Warm Cream/White; burgundy links and phone actions.
- Use Burnt Orange only for small labels or separators.
- Keep Facebook and Instagram links in the footer.

### Inputs (Theme-Level)

- On light surfaces: white field with `1px solid #D8C9B8` border, espresso text, muted brown placeholder.
- Focus: burgundy border/outline and visible keyboard focus ring.
- Labels: retain Quicksand bold, uppercase, tracked style, recolored espresso.
- Error: distinct red state (`#B3261E`) with explicit message.
- Do not use the source theme's dark field surface by default in this light colorway.

## 5. Layout Principles

### Section Rhythm

1. **Hero:** full-width photo slideshow, black gradient overlay, centered brand and headline, supporting copy, burgundy “View Menu” CTA.
2. **Experience intro:** Warm Cream section with burnt-orange/burgundy eyebrow, espresso Bitter title, three photo feature cards.
3. **Meat showcase:** cream/white section with the single-image carousel and editorial headline/copy/outlined CTA.
4. **Brand/award moments:** alternate light content surfaces with a Burgundy Deep or Espresso feature band for high-emphasis storytelling.
5. **Locations:** Warm Cream section with two photo cards, then grouped addresses and hours.
6. **Footer:** Burgundy Deep (`#48151D`) or Espresso (`#2B211D`) surface with white text, orange accent links, and social links.

### Spacing & Containers

- Keep source spacing: common theme utilities `20px`, `40px`, `80px`; desktop section padding about `128px`.
- Main content max width around `1280px`; editorial blocks approximately `730–800px`.
- Hero desktop padding about `160px` top / `112px` bottom; tablet minimum height around `600px`.
- Section padding: approximately `128px` desktop → `96px` tablet → `64px` mobile.
- Feature-card insets: `28px` desktop / `20px` mobile.
- Use section surface changes and generous whitespace instead of heavy dividers.

### Grid

- Experience cards: 3 columns desktop → 2 tablet → 1 mobile.
- Location cards: 2 columns desktop/tablet → 1 mobile.
- Main boxed container: approximately `1140px`, with homepage sections reaching about `1280px`.

## 6. Depth, Overlays & Motion

- **Hero overlay:** retain source black horizontal fade (approximately `rgba(0,0,0,0.65)` to `rgba(12,12,20,0.28)`) to preserve headline contrast over the slideshow.
- **Feature/location photo overlay:** black at roughly `0.4–0.75` opacity, tuned to each image.
- **Light surfaces:** use cream/white color blocking for depth; avoid heavy card shadows.
- **Card hover:** background image scales to `1.1` over `0.5s ease`.
- **Hero slideshow:** six images; 2.5s slide duration, 800ms transition, looping.
- **Meat carousel:** 3s autoplay, 500ms transition, looping.
- **Theme transitions:** links and field states retain approximately `0.4s ease-in-out`.
- Do not add decorative gradients to solid color bands. Photo overlays remain allowed because they support text readability.

## 7. Do's and Don'ts

### Do
- Use Warm Cream (`#FFF4E5`) as the dominant page canvas and white for clean panels.
- Use Deep Burgundy (`#6B1F2A`) for primary CTAs and major brand moments.
- Use Burnt Orange (`#D96B32`) sparingly for eyebrow labels, small highlights, and hover accents.
- Keep Espresso (`#2B211D`) as the default text color on light surfaces.
- Retain black translucent overlays over photography where white text appears.
- Preserve Bitter headlines, tracked labels, meat carousel, and two-location storytelling.
- Use burgundy/espresso dark bands selectively for award or editorial emphasis and footer.

### Don't
- Don't carry the original charcoal palette across every section; cream is now the default canvas.
- Don't use orange as the primary CTA or fill every section with burgundy.
- Don't use sage for conversion actions.
- Don't remove dark photo overlays when white text is on photography.
- Don't substitute a generic split hero for the source's full-width slideshow.
- Don't invent reservation/online-order interactions not present in the referenced homepage.
- Don't introduce decorative gradients or heavy shadows.

## 8. Responsive Behavior

### Breakpoints

| Range | Behavior |
|-------|----------|
| `≤ 767px` | Hamburger nav; feature/location grids one column; hero headline 48px; main headings 36px; section padding about 64px; cards around 370px |
| `768–1024px` | Feature/location grids two columns; hero headline 72px; section padding around 96px; feature cards around 400px |
| `≥ 1025px` | Three experience cards; two location cards; hero headline 88px; section padding around 128px; feature cards around 478px |

### Mobile Guidance

- Keep the hamburger, logo, and hero CTA legible over the slideshow.
- Stack photo cards and locations without reducing text contrast or tap areas.
- Keep card text white over darkened photos; use light-colorway text only in separate light sections.
- Preserve responsive image positioning and crop for the source photography.
- Ensure phone, address, hours, and social links remain easy to read and tap.

## 9. Agent Prompt Guide

### Quick Reference

- Page canvas: Warm Cream (`#FFF4E5`)
- Alternate surface: Cream Deep (`#F5E8D6`)
- Card/content surface: White (`#FFFFFF`)
- Brand / primary CTA: Deep Burgundy (`#6B1F2A`)
- CTA hover: Warm Burgundy (`#842D38`)
- Deep band/footer: Burgundy Deep (`#48151D`) or Espresso (`#2B211D`)
- Accent: Burnt Orange (`#D96B32`)
- Freshness accent: Sage Green (`#74856A`)
- Light-surface text: Espresso (`#2B211D`); secondary `#665750`
- Dark/photo text: White (`#FFFFFF`); supporting `rgba(255,255,255,0.76)`
- Display: Bitter, 88px desktop / 72px tablet / 48px mobile
- Body: Inter 16px / 1.7; eyebrow: Montserrat 12px/600, uppercase, `0.18em`

### Example Prompts

1. “Build the Thirsty Cow photo-slideshow hero with the original centered editorial hierarchy and dark photo overlay. Use a white Bitter headline and a Deep Burgundy `#6B1F2A` ‘View Menu’ pill CTA, with Burnt Orange `#D96B32` as a restrained small accent.”

2. “Create the Premium Meats / The Bar / The Experience photo-card grid on a Warm Cream `#FFF4E5` section. Keep full-bleed images, black readability overlays, thin translucent cream borders, bottom-aligned white Bitter headings, Montserrat captions, and a subtle 0.5s zoom hover.”

3. “Design the meat carousel section on cream or white: one large food photo per slide, previous/next arrows, and an editorial copy block with a burgundy eyebrow/headline, espresso body text, and a burgundy outlined CTA. Preserve looping autoplay.”

4. “Create the two location cards on a warm cream section, retaining darkened venue photography and white bottom-aligned labels. Follow with espresso address/hour details, burgundy phone links, and a Burgundy Deep footer with white social links.”

### Known Limits

- This document deliberately combines exact layout/type/motion observations from the Thirsty Cow source with the requested alternate palette.
- The new palette values are specified in `DESIGN-starbucks-orange.md`; they are not extracted from the live Thirsty Cow site.
- Exact responsive behavior for every footer/navigation detail and interior-page component was not measurable from the homepage.
