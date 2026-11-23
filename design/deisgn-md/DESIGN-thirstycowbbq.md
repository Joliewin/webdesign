# Thirsty Cow Korean BBQ — Website Design System

**Source:** [thirstycowbbq.com](https://www.thirstycowbbq.com/) homepage and its published stylesheet/page CSS, reviewed November 2026. This document describes the observed site, not a proposed redesign. Exact values below come from the available CSS; visual measurements not specified there are identified as approximate.

## 1. Visual Theme & Atmosphere

Thirsty Cow presents Korean BBQ as a premium, after-dark experience: dark charcoal surfaces, muted warm neutrals, restrained wine-red accents, cinematic food and venue photography, and editorial serif headlines. The mood is confident and upscale without losing the social energy of all-you-can-eat barbecue and a full bar.

The homepage sequence is deliberately immersive: transparent/static header over a full-bleed rotating-photo hero → near-black experience section with three photographic feature cards → premium meat image carousel → dark editorial meat feature → award/brand moment → two location cards → location details and hours → social/footer links. Repeated dark surfaces let the photography and accent red carry the visual contrast.

**Key Characteristics**
- Predominantly dark palette: charcoal-black (`#171314`, `#262328`) with warm-white and gray text.
- Muted wine red (`#953031`) is the key action/brand accent; deeper red is used for hover.
- Large, elegant serif display typography contrasts with tracked uppercase sans-serif labels.
- Large background photographs use dark overlays; text sits near the bottom of feature cards.
- Food is presented through a 31-image, one-slide-at-a-time carousel with arrow navigation and autoplay.
- Layout uses spacious section padding, hairline borders, and photo-led cards rather than bright menu tiles.
- Content emphasizes premium meat provenance, signature drinks, award recognition, and two Southern California locations.

## 2. Color Palette & Roles

### Brand Colors

- **Muted Wine Red** (`#953031`): Main CTA, accent divider, and primary brand/action color.
- **Deep Red** (`#570D0E`): Main hero-button hover state.
- **Alternate Deep Red** (`#521112`): Hover treatment for the later feature CTA.
- **Rose Accent** (`#D06D6E`): Small uppercase eyebrow labels on dark sections.
- **Warm Charcoal** (`#171314`): Main dark section surface and global dark canvas.
- **Charcoal Surface** (`#262328`): Form/control surface and dark secondary panels.
- **Near Black** (`#000000`): Hero and photo-card underlay/overlay.
- **Deep Ink** (`#1C191D`): Inline code/preformatted surface in the theme.

### Neutrals & Text

- **Warm White** (`#F4F0E7`): Warm light text/section accent (Elementor global color).
- **Soft White** (`#EAEAEA`): Core theme light color and prominent text on dark backgrounds.
- **Secondary Light Gray** (`#DCDCDC`): Feature-card descriptions.
- **Muted Gray** (`#B3ADA4`): Secondary copy and subdued text.
- **Body Text on Dark** (`rgba(234,234,234,0.8)`): Default body text in the theme.
- **Card Border** (`#605B54`): Fine border around photo cards.
- **Dark Border** (`#3C3638`): Dark structural border/accent.
- **Muted Gold** (`#C09752`): Theme token for restrained premium accents; not a dominant homepage color.

### Theme Tokens Not Used as Homepage Brand Colors

The shared Elementor kit includes default blue/green tokens (`#6EC1E4`, `#61CE70`) and generic WordPress defaults. These are framework presets; the homepage styles instead use wine red, charcoal, warm-white, and muted neutrals.

## 3. Typography Rules

### Font Families

- **Body / general UI:** `Inter, Arial, Helvetica, sans-serif`.
- **Theme headings:** `Quicksand, Arial, Helvetica, sans-serif`, bold, uppercase, tracked.
- **Homepage editorial headings:** `Bitter`, typically medium weight, title case/capitalized.
- **Eyebrow labels:** `Montserrat`, 12px, weight 600, uppercase, `0.18em` tracking.
- **Supporting display option in global kit:** `Cormorant Garamond` and `Playfair Display` are loaded/configured; the homepage hero and section headlines use Bitter in the observed page CSS.

### Hierarchy

| Role | Size | Weight | Line Height | Treatment |
|------|------|--------|-------------|-----------|
| Hero headline | 88px desktop; 72px tablet; 48px mobile | 500 | `0.95em` | Bitter, white, centered |
| Main section headline | 60px desktop; 36px mobile | 500 | Default / compact mobile | Bitter, white, centered |
| Large editorial headline | 72px desktop; 36px mobile | 500 | Default / `1em` mobile | Bitter, white |
| Feature-card title | 30px | 400–500 | Theme default | Bitter, white |
| Eyebrow | 12px | 600 | — | Montserrat, uppercase, `0.18em` tracking |
| Body copy | 16px | 400 | `1.7` theme default | Inter; hero uses Montserrat, 16px |
| Feature-card copy | 14px | 400 | — | Montserrat, light gray |
| Theme heading fallback | h1 36.9px; h2 33.5px; h3 30.5px | 700 | `1.4` | Quicksand, uppercase, `0.1em` tracking |

### Principles

- Keep oversized Bitter headlines as the editorial focal point.
- Use small, widely tracked uppercase labels to introduce sections (“At the table,” “Selected for the grill”).
- Use Inter for general reading and utility controls; Montserrat appears in homepage supporting copy and card descriptions.
- Preserve strong light-on-dark contrast; muted grays are secondary copy rather than headline colors.

## 4. Component Stylings

### Header & Navigation

- Brand logo image at approximately `150px` maximum width.
- Header is static and transparent over the hero; theme includes an auto-hide header behavior.
- Desktop navigation is a horizontal row: Home · Menu (submenu by location) · Bar · About · Location.
- Mobile navigation uses a hamburger trigger and a close control.
- Header and hero share the immersive dark/photo treatment; no prominent light nav panel is used.

### Buttons

**Primary Hero CTA — “View Menu”**
- Background: Muted Wine Red (`#953031`)
- Text/icon: White
- Padding: `16px 28px`
- Icon: right-arrow icon, visually placed alongside the label
- Hover/focus: Deep Red (`#570D0E`)

**Feature CTA**
- Transparent/dark background with a `2px` wine-red border.
- White uppercase label.
- Padding: `16px 28px`
- Hover/focus fills with Wine Red.

**Location CTA**
- Low-chrome text action over each photo card, white with a right-arrow affordance.
- Hover/focus changes label/icon to bright yellow (`#FFEC01`) in the observed page CSS.

### Photo Feature Cards

- Three-card desktop grid: Premium Meats, The Bar, The Experience.
- Approximate desktop minimum height: `478px`; tablet `400px`; mobile `370px`.
- Full-bleed background photography with black/dark overlay.
- Thin `1px solid #605B54` border.
- Content anchored to the bottom with roughly `28px` desktop and `20px` mobile inset.
- Background image gently zooms on hover (`scale(1.1)` over `0.5s`); dark overlay preserves legibility.
- Heading: Bitter, 30px, white. Supporting copy: Montserrat, 14px, `#DCDCDC`.

### Meat Image Carousel

- Single image visible per slide; 31 premium meat, seafood, side, and soup images.
- Autoplay enabled at approximately 3 seconds per slide; infinite loop.
- 500ms slide transition with previous/next arrow controls positioned inside the carousel.
- Images use their original wide food-photography format and are lazy-loaded.
- Use the image sequence to communicate ingredient breadth and premium cuts, not as a text-heavy product grid.

### Location Cards

- Two-column photo-led layout: Garden Grove and City of Industry.
- Approximate card height: `500px` desktop and `400px` tablet; mobile cards around `370px`.
- Darkened photographic background, subtle border, and white location title/action near bottom.
- Each card links to the location-specific menu; location details follow in a separate section.

### Location Details

- Each location has a distinct address, phone number, and day-by-day operating hours.
- Keep contact information grouped by venue and scannable; phone should be a direct `tel:` action.
- Social links (Facebook and Instagram) appear in the footer area.

### Inputs (Theme-Level)

Though not a visible homepage focus, the theme’s form controls use:
- Dark field surface (`#262328`) and a `2px` translucent light border.
- Muted light text and placeholder; focus shifts to `#19171A` with a solid `#EAEAEA` border.
- Labels use Quicksand, bold, uppercase, and tracked styling.
- Error state uses red (`#C84646`).

## 5. Layout Principles

### Section Rhythm

1. **Hero:** full-width slideshow background, dark overlay, centered wordmark-style name and headline, supporting line, red menu CTA.
2. **Experience intro:** dark (`#171314`) section with small rose eyebrow, large white serif title, three image cards.
3. **Meat showcase:** one-image carousel paired with “Selected for the grill” title, explanatory copy, and outlined CTA.
4. **Brand/award features:** dark photographic/editorial moments and award recognition.
5. **Locations:** two large photo cards, followed by a location summary and detailed address/hours.
6. **Footer:** social links and site credit on the dark theme.

### Spacing & Containers

- Theme utility spacing commonly uses `20px`, `40px`, and `80px`; Elementor sections use about `128px` vertical padding on desktop.
- Main content width reaches approximately `1280px`; smaller editorial blocks range around `730–800px`.
- Hero desktop padding: about `160px` top and `112px` bottom; tablet hero has a `600px` minimum height.
- Section padding reduces from `128px` desktop to `96px` tablet and `64px` mobile.
- Feature cards use `28px` desktop and `20px` mobile internal padding.
- Use section spacing, tonal changes, and photographs to separate content; avoid excessive dividers.

### Grid

- Experience cards: 3 columns desktop → 2 tablet → 1 mobile.
- Location cards: 2 columns desktop/tablet → 1 mobile.
- Main boxed container: approximately `1140px` default, with homepage content areas reaching `1280px`.

## 6. Depth, Overlays & Motion

- **Hero overlay:** black horizontal gradient, approx. `rgba(0,0,0,0.65)` to `rgba(12,12,20,0.28)`; the section overlay is also configured at 0.8 opacity.
- **Feature card overlay:** black, typically around 0.4 opacity, with card-specific overlays configured between 0.6 and 0.9.
- **Location/photo overlay:** black overlay to maintain white text contrast.
- **Card hover:** background photo scales to `1.1` over `0.5s ease`.
- **Hero slideshow:** six images, 2.5-second slide duration, 800ms slide-down transition, looping.
- **Food carousel:** 3-second autoplay, 500ms slide transition, looping.
- **Theme transitions:** links and form states commonly transition over `0.4s ease-in-out`.

## 7. Do's and Don'ts

### Do
- Keep the dominant surfaces charcoal and near-black.
- Use wine red (`#953031`) for primary calls to action and small brand accents.
- Use Bitter for large editorial headlines and tracked uppercase for small section labels.
- Darken image backgrounds enough for text to remain legible.
- Make food, drinks, and venue imagery the main emotional content.
- Keep feature-card borders thin and muted, and content anchored toward the bottom.
- Preserve the distinct Garden Grove and City of Industry menu/location paths.
- Use responsive column reduction and tighter padding on mobile.

### Don't
- Don't introduce a bright cream-first or burgundy-first palette; that would depart from the observed charcoal identity.
- Don't replace the editorial serif display style with uniformly geometric sans-serif.
- Don't let photo-card backgrounds compete with white labels.
- Don't treat all theme-kit colors as brand colors; the blue and green presets are generic framework defaults.
- Don't invent online ordering, reservation, or interaction features that are not evidenced on the inspected homepage.
- Don't overwhelm the page with extra borders, card shadows, or decorative gradients.

## 8. Responsive Behavior

### Breakpoints

| Range | Observed Behavior |
|-------|-------------------|
| `≤ 767px` | Hamburger navigation; feature and location grids become one column; hero headline 48px; main headings 36px; section padding about 64px; card heights around 370px |
| `768–1024px` | Two-column feature/location grids; hero headline 72px; section padding about 96px; feature-card heights around 400px |
| `≥ 1025px` | Three-column experience cards; two-column locations; hero headline 88px; section padding around 128px; feature cards around 478px |

### Mobile Guidance

- Keep the hamburger navigation clear and the logo visually prominent.
- Preserve the centered headline and menu CTA in the hero.
- Stack feature and location cards without shrinking text into the image detail.
- Crop backgrounds thoughtfully; source CSS adjusts image positioning at tablet/mobile widths.
- Keep contact details, hours, and social links readable and easy to tap.

## 9. Agent Prompt Guide

### Quick Reference

- Main surface: Warm Charcoal (`#171314`)
- Secondary surface: Charcoal (`#262328`)
- Primary CTA: Muted Wine Red (`#953031`)
- CTA hover: Deep Red (`#570D0E`)
- Eyebrow: Rose Accent (`#D06D6E`)
- Main light text: Soft White (`#EAEAEA`) / White (`#FFFFFF`)
- Secondary copy: Muted Gray (`#B3ADA4`) or Light Gray (`#DCDCDC`)
- Display headline: Bitter, 88px desktop / 72px tablet / 48px mobile
- Body: Inter 16px, line height 1.7
- Eyebrow: Montserrat 12px/600, uppercase, `0.18em` tracking
- Photo card: dark overlay, thin `#605B54` border, bottom-aligned white text

### Example Prompts

1. “Build a Thirsty Cow-style hero: full-bleed rotating Korean BBQ/restaurant photography with a dark horizontal overlay, centered white 88px Bitter headline, small tracked uppercase label, concise muted-gray supporting copy, and a wine-red `#953031` ‘View Menu’ button. Scale the headline to 72px tablet and 48px mobile.”

2. “Create three dark photo feature cards titled ‘Premium Meats,’ ‘The Bar,’ and ‘The Experience.’ Use full-bleed background photos, a black legibility overlay, a fine warm-gray border, and bottom-aligned Bitter 30px white titles with 14px Montserrat light-gray descriptions. Add a subtle 0.5s image zoom on hover.”

3. “Design a premium meat showcase with a single-image looping carousel, previous/next arrows, and a neighboring editorial block: tracked eyebrow, large white Bitter headline, short muted copy, and a wine-red outlined CTA.”

4. “Create two location photo cards for Garden Grove and City of Industry, then a scannable dark location-details section with address, phone, daily hours, and social links.”

### Known Limits

- Exact navigation sizing, footer colors by individual element, and full details for every interior page were not measurable from the homepage extraction.
- A few configured colors are shared theme defaults rather than necessarily visible in the page.
- Treat inferred image crops and card composition as practical reproduction guidance, not guaranteed source measurements.
