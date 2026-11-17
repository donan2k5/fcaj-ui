---
name: Cloud Enterprise Events
colors:
  surface: '#f8f9f9'
  surface-dim: '#d9dada'
  surface-bright: '#f8f9f9'
  surface-container-lowest: '#ffffff'
  surface-container-low: '#f3f4f4'
  surface-container: '#edeeee'
  surface-container-high: '#e7e8e8'
  surface-container-highest: '#e1e3e3'
  on-surface: '#191c1c'
  on-surface-variant: '#44474c'
  inverse-surface: '#2e3131'
  inverse-on-surface: '#f0f1f1'
  outline: '#75777c'
  outline-variant: '#c5c6cc'
  surface-tint: '#535f70'
  primary: '#0e1a28'
  on-primary: '#ffffff'
  primary-container: '#232f3e'
  on-primary-container: '#8a97a9'
  inverse-primary: '#bbc7db'
  secondary: '#005eb2'
  on-secondary: '#ffffff'
  secondary-container: '#509cff'
  on-secondary-container: '#003365'
  tertiary: '#0e1a29'
  on-tertiary: '#ffffff'
  tertiary-container: '#232f3f'
  on-tertiary-container: '#8b97aa'
  error: '#ba1a1a'
  on-error: '#ffffff'
  error-container: '#ffdad6'
  on-error-container: '#93000a'
  primary-fixed: '#d7e3f7'
  primary-fixed-dim: '#bbc7db'
  on-primary-fixed: '#101c2b'
  on-primary-fixed-variant: '#3c4858'
  secondary-fixed: '#d5e3ff'
  secondary-fixed-dim: '#a7c8ff'
  on-secondary-fixed: '#001c3b'
  on-secondary-fixed-variant: '#004788'
  tertiary-fixed: '#d7e3f8'
  tertiary-fixed-dim: '#bbc7dc'
  on-tertiary-fixed: '#101c2b'
  on-tertiary-fixed-variant: '#3c4758'
  background: '#f8f9f9'
  on-background: '#191c1c'
  surface-variant: '#e1e3e3'
typography:
  headline-xl:
    fontFamily: Open Sans
    fontSize: 40px
    fontWeight: '700'
    lineHeight: 48px
  headline-xl-mobile:
    fontFamily: Open Sans
    fontSize: 30px
    fontWeight: '700'
    lineHeight: 38px
  headline-lg:
    fontFamily: Open Sans
    fontSize: 28px
    fontWeight: '700'
    lineHeight: 36px
  headline-md:
    fontFamily: Open Sans
    fontSize: 20px
    fontWeight: '700'
    lineHeight: 26px
  headline-sm:
    fontFamily: Open Sans
    fontSize: 16px
    fontWeight: '700'
    lineHeight: 22px
  body-lg:
    fontFamily: Open Sans
    fontSize: 16px
    fontWeight: '400'
    lineHeight: 24px
  body-md:
    fontFamily: Open Sans
    fontSize: 14px
    fontWeight: '400'
    lineHeight: 20px
  body-sm:
    fontFamily: Open Sans
    fontSize: 12px
    fontWeight: '400'
    lineHeight: 16px
  label-lg:
    fontFamily: Open Sans
    fontSize: 14px
    fontWeight: '600'
    lineHeight: 20px
  label-md:
    fontFamily: Open Sans
    fontSize: 12px
    fontWeight: '600'
    lineHeight: 16px
  label-sm:
    fontFamily: Open Sans
    fontSize: 11px
    fontWeight: '600'
    lineHeight: 14px
rounded:
  sm: 0.125rem
  DEFAULT: 0.25rem
  md: 0.375rem
  lg: 0.5rem
  xl: 0.75rem
  full: 9999px
spacing:
  gutter: 1.5rem
  gutter-mobile: 1rem
  margin: 2rem
  margin-mobile: 1rem
  space-xs: 0.25rem
  space-sm: 0.5rem
  space-md: 1rem
  space-lg: 1.5rem
  space-xl: 2.5rem
---

## Brand & Style

This design system establishes an authoritative, reliable, and modern enterprise aesthetic for event discovery, conference navigation, and technical learning portals. It eliminates high-energy promotional warmth in favor of structured architectural clarity, developer precision, and institutional trust.

### Style Archetype
- **Corporate / Modern Enterprise:** Dominated by deep squid inks, clean light surfaces, crisp structural divisions, and purposeful interactive accents.
- **Tone & Mood:** Direct, technical, highly organized, and calm. The visual experience puts session data, speaker profiles, dates, and event credentials at the forefront without extraneous visual noise.
- **Principles:**
  - *Utility-Driven Hierarchy:* Content organization reflects enterprise workflows—scannable titles, discrete metadata badges, and definitive calls-to-action.
  - *Restraint over Ornamentation:* Depth is conveyed via structural hair-lines and quiet tonal surfaces rather than heavy blur dynamics or ambient lighting.
  - *Disciplined Contrast:* Deep dark navies anchor navigation and headers, while pure white cards rest on neutral off-white canvases.

## Colors

The palette is engineered around high legibility, strict contrast ratios, and deliberate exclusion of warmer orange hues. 

### Core Palette Tokens
- **Primary (`#232F3E`):** AWS Deep Navy ("Squid Ink"). Used for main typographic headings, high-priority icons, standard dark backgrounds, and prominent framing elements.
- **Secondary / Action Blue (`#0972D3`):** Interactive focal point. Applied to interactive links, primary buttons, active tab indicators, and focused input states.
- **Tertiary / Header Dark (`#0F1B2A`):** The deepest navy tier, reserved for global navigation headers, utility banners, and high-tier enterprise anchor bars.
- **Secondary Dark Accent (`#1A2433`):** Intermediate dark tone used for secondary header elements, subnav background fills, and dark-card variants.
- **Neutral Canvas (`#F8F9FA` to `#F2F3F3`):** Low-glare foundational light grey background that provides soft separation for white content containers.
- **Card & Elevated Surface (`#FFFFFF`):** High-clarity pure white surfaces for content cards, session panels, and modal containers.
- **Border & Dividers (`#D5DBDB` / `#E9EBED`):** Subtle neutral hairline borders providing crisp boundary definition without visual weight.
- **Body Charcoal (`#16191F`):** Standard reading color for body copy, sub-bullets, and general metadata, ensuring effortless long-form scanning.

## Typography

Typography relies on a clean, universal humanist grotesque (`Open Sans`) that mirrors cloud console interfaces and enterprise documentation. It balances compact UI real estate with clear legibility across complex multi-column event agendas.

### Hierarchy & Style Rules
- **Headlines:** Use solid weights (`700`) paired with tight, calculated line-heights to ground large screen titles. Event names use `headline-md` within card grids to maintain a stable horizontal horizon.
- **Body:** Kept at standard regular (`400`) weight in `#16191F` for maximum contrast against white cards and slate backgrounds.
- **Labels & Metadata:** Use semi-bold (`600`) weights for timestamps, event categories, location tags, and interactive button text.
- **Responsive Adaptations:** Titles scale down smoothly below tablet breakpoints (`768px`) using dedicated `-mobile` variants to avoid awkward line breaks on event names.

## Layout & Spacing

The layout is built upon an 8px base rhythm arranged inside a responsive 12-column grid.

### Layout Architecture
- **Desktop (1024px+):** Max-width content boundary of `1280px` centered with `2rem` margins. Standard grid runs 12 columns with `1.5rem` gutters. Event cards comfortably sit in 3-column clusters (`col-span-4`).
- **Tablet (768px – 1023px):** 8-column layout with `1.5rem` margins and gutters. Cards reflow to 2-column configurations (`col-span-4`).
- **Mobile (< 768px):** 4-column layout with `1rem` margins and `1rem` gutters. Cards collapse into full-width stacks (`col-span-4`).
- **Vertical Spacing:** Section partitions maintain `space-xl` (40px) separation, while intra-component elements (card header to body copy) respect `space-sm` (8px) and `space-md` (16px) rhythms.

## Elevation & Depth

Visual separation emphasizes structure and tonal tiers rather than deep, diffused shadows.

### Surface Hierarchy
- **Level 0 (Base Canvas):** `#F8F9FA` or `#F2F3F3`. Neutral foundational field for page backgrounds and content staging.
- **Level 1 (Cards & Structural Containers):** Pure `#FFFFFF` background bound by a 1px continuous border of `#D5DBDB`.
- **Level 2 (Dropdowns & Popovers):** Elevated `#FFFFFF` surfaces with subtle border `#D5DBDB` and an ambient, low-profile drop shadow: `0 4px 12px rgba(15, 27, 42, 0.08)`.
- **Level 3 (Modals & Overlays):** Grounded by a backdrop scrim of `#0F1B2A` at `65%` opacity, paired with a centered container elevated by `0 8px 24px rgba(15, 27, 42, 0.16)`.

### Border Guidelines
- Avoid heavy drop shadows on card components.
- Rely on structural `1px` lines (`#E9EBED` internally, `#D5DBDB` externally) to separate content modules cleanly.

## Shapes

The interface embraces a tailored, subtle roundedness (`0.25rem` / `4px` baseline) reflecting enterprise precision, with slightly elevated card headers and media elements matching `0.5rem` (`rounded-lg`).

### Application Specs
- **Default (4px):** Form inputs, buttons, filter pills, dropdown items, and navigation indicators.
- **Rounded-LG (8px):** Event preview cards, modal containers, and graphic media containers.
- **Pill / Circular:** Reserved exclusively for user profile avatars and status notification counters.

## Components

### Buttons
- **Primary:** Background `#0972D3`, text `#FFFFFF`, 4px border radius, padding `0.5rem 1.25rem`. Hover state transitions to `#005AAB`. Focus ring is a 2px offset `#0972D3` ring.
- **Secondary / Ghost:** Transparent background with a `1px` border of `#232F3E`, text `#232F3E`. Hover background fills with `#F2F3F3`.
- **Navigation Action ("Create account" / "Sign in"):** Solid `#232F3E` background, white text, 4px radius for primary administrative calls-to-action.

### Cards (Event Display)
- **Container:** `#FFFFFF` background, `1px solid #D5DBDB`, `8px` corner radius.
- **Media Thumbnail:** Aspect ratio 16:9, fixed to top corners with `8px` top radius. Holds branded event typography or imagery on dark squid ink/deep indigo gradients.
- **Body Content:** Internal padding of `1.25rem`. Title set in `headline-md` (`#232F3E`), followed by sub-metadata in `body-sm` (`#545B64`), and short description in `body-md` (`#16191F`).
- **Card Action Link:** Anchored at the bottom as an inline link in `#0972D3` with hover underline (`Register now`, `View upcoming events`).

### Navigation & Header Bars
- **Utility Nav (Topmost):** Height 36px, background `#0F1B2A`, typography `12px` in `#D5DBDB` with hover state in pure white.
- **Main Nav:** Height 64px, background `#FFFFFF`, bottom border `1px solid #E9EBED`. Logo aligned left; navigation links in `body-md` semi-bold (`#16191F`).
- **Sub-Navigation Filter Bar:** Contained pill-shaped container or flat border-bottom tab strip with active indicator in `#0972D3` (2px solid bottom bar).

### Input Fields & Search
- **Input Surface:** `#FFFFFF` with `1px solid #AAB7B8`, `4px` border radius, padding `0.5rem 0.75rem`.
- **Focus State:** Border shifts to `#0972D3` with a subtle box-shadow glow `0 0 0 1px #0972D3`.
- **Placeholder:** `#545B64`.

### Chips & Badges
- **Status Badges:** Flat background `#F2F3F3`, text `#232F3E`, `1px solid #D5DBDB`, 4px radius, uppercase `label-sm` tracking.
- **Active Filter Chips:** Background `#EBF5FB`, border `1px solid #0972D3`, text `#0972D3`.