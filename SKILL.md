---
name: chainsystem-skill
description: "Build and structure Webflow projects using the ChainSystem framework by Fernando Comet. Use this skill whenever the user asks about ChainSystem, Webflow class naming with kebab-case, page-section-container-element chain structure, ChainSystem utility classes, ChainSystem spacing variables, or anything related to building a scalable Webflow project with the ChainSystem methodology. Also trigger when the user mentions 'chainsystem', 'chain system', 'chain-system', kebab-case Webflow naming, or any ChainSystem class pattern — even if they don't say 'ChainSystem' explicitly."
---

# ChainSystem — Webflow Structure & Naming

Docs: https://chainsystem.webflow.io/  
Cloneable: https://webflow.com/made-in-webflow/website/chainsystem

ChainSystem is a class naming system for Webflow projects. Fast, clear, intuitive and productive. Based on KISS methodology — wherever possible, avoid complexity.

---

## Core Principles

- **KISS** — Keep It Simple. Avoid complexity wherever possible.
- **One class per element** — use mainly one class per element to minimize errors and avoid issues when repeating classes.
- **Class name = location** — the class name tells you exactly where you are in the page and document flow.
- **Lowercase for classes** — all class names use lowercase kebab-case.
- **Capital letters for Components** — Navbar, Footer, and global components use Capital letters.
- **No Webflow native Columns/Containers** — use divs instead; native elements are harder to maintain.
- **No magic numbers** — avoid fixed arbitrary width/height values.
- **No excessive divs** — avoid "Hadouken" nesting (boxes inside boxes inside boxes).
- **No Combo Classes unless necessary** — they are hard to maintain. Merge or redo instead.
- **Spacing in containers** — margins/paddings belong mainly in containers, not in low-level elements. Use Flex and Grid for placing elements.
- **Alt text on all images** — required without exception.
- **Use rem units** — recommended CSS unit for consistency and accessibility.
- **Avoid Custom Code Blocks** — use Webflow native features. If generic CSS is needed site-wide, create a component for it.
- **No unnamed elements** — "Div Block 37", "Heading 21", "Text Block 34" are not accepted. Name every element correctly.

---

## Class Naming Convention

ChainSystem uses **kebab-case** — all lowercase, words separated by hyphens.

### Core chain structure

```
page-section-container-element-detail
```

Each class name follows the chain from the top down. Each page acts as a **skin** — all elements of a page start with the page name.

### Chain depth rule

Go up to **3 levels** deep in the chain. When a new context starts (e.g. a card inside a wrapper), reset the chain starting from that new context:

```
about-hero                  → section
about-hero-h1               → heading inside hero
about-hero-h2               → subheading inside hero
about-hero-wrapper          → container inside hero
hero-wrapper-card           → card inside wrapper (context resets to wrapper)
hero-wrapper-img            → image inside wrapper
hero-card-h3                → heading inside card (context resets to card)
hero-card-img               → image inside card
hero-card-p                 → paragraph inside card
hero-card-cta               → CTA inside card
```

### Page skins (examples)

Each page defines the first segment of all its element classes:

```
home        → home-header, home-highlights, home-features...
landing     → landing-header, landing-info, landing-blog...
blog        → blog-hero, blog-posts...
faq         → faq-header, faq-questions...
about       → about-hero, about-team, about-values...
```

### Section → Container pattern

```
[page]-[section]                    → section wrapper
[page]-[section]-container          → container inside section
[page]-[section]-[element]          → elements inside container
```

Example for Home page:

```
home-header
home-header-container
home-header-h1
home-header-h2
home-header-cta

home-highlights
home-highlights-container
home-highlights-grid
home-highlights-card

home-features
home-features-container
home-features-list
```

### Naming rules summary

| Rule | Detail |
|---|---|
| Case | Lowercase only |
| Separator | Hyphen `-` between all words |
| Depth | Max 3 levels, then reset context |
| Components | Capital first letter (Navbar, Footer) |
| Elements | Descriptive but short (h1, h2, p, img, cta, btn, card, wrapper, grid, list) |

---

## Page Structure

```html
<div class="page-wrapper">
  <!-- Navbar component -->
  <nav class="Navbar">...</nav>

  <main class="page-main">

    <section class="[page]-[section]">
      <div class="[page]-[section]-container">
        <!-- content -->
      </div>
    </section>

    <!-- additional sections -->

  </main>

  <!-- Footer component -->
  <footer class="Footer">...</footer>
</div>
```

---

## Grid System (Custom cs-grid / cs-cell)

ChainSystem uses a custom flexbox/grid system with `cs-grid` and `cs-cell` classes. The `cs-` prefix (ChainSystem) clearly distinguishes grid classes from page-specific classes.

```html
<div class="[page]-[section]-grid cs-grid cs-grid-3">
  <div class="[page]-[section]-cell cs-cell">...</div>
  <div class="[page]-[section]-cell cs-cell">...</div>
  <div class="[page]-[section]-cell cs-cell">...</div>
</div>
```

### Grid column variants

```
cs-grid-2       → 2 equal columns
cs-grid-3       → 3 equal columns
cs-grid-4       → 4 equal columns
cs-grid-5       → 5 equal columns
cs-grid-6       → 6 equal columns
```

### Cell span variants

```
cs-cell-span-2  → cell spans 2 columns
cs-cell-span-3  → cell spans 3 columns
```

### Breakpoints

| Breakpoint | Fires at |
|---|---|
| Desktop `-lg` | > 992px |
| Tablet `-md` | ≤ 991px |
| Mobile Landscape `-sm` | ≤ 767px |
| Mobile Portrait `-xs` | ≤ 478px |

### Responsive grid variants

```
cs-grid-lg-2 / cs-grid-md-1    → 2 cols desktop, 1 col tablet
cs-grid-lg-3 / cs-grid-md-2 / cs-grid-sm-1
```

---

## Spacing Variables

ChainSystem uses a standardized spacing scale defined as Webflow variables in rem units. Variable names match the px value directly for clarity.

| Variable name | rem value |
|---|---|
| `0px` | 0rem |
| `4px` | 0.25rem |
| `8px` | 0.5rem |
| `12px` | 0.75rem |
| `16px` | 1rem |
| `20px` | 1.25rem |
| `24px` | 1.5rem |
| `32px` | 2rem |
| `40px` | 2.5rem |
| `48px` | 3rem |
| `56px` | 3.5rem |
| `64px` | 4rem |
| `72px` | 4.5rem |
| `80px` | 5rem |
| `90px` | 5.625rem |

Always use spacing variables instead of hardcoded values. Apply spacing mainly to containers and section wrappers, not to low-level elements.

---

## Typography — Fluid Scale

ChainSystem uses a fluid typographic scale based on `clamp()`. Font sizes scale smoothly between a minimum viewport (320px) and a maximum viewport (1440px) — no manual breakpoint overrides needed.

### Heading classes

| Class | Min size | Max size | clamp() value |
|---|---|---|---|
| `h1` | 36px / 2.25rem | 72px / 4.5rem | `clamp(2.25rem, 1.5rem + 3.75vw, 4.5rem)` |
| `h2` | 28px / 1.75rem | 48px / 3rem | `clamp(1.75rem, 1.25rem + 2.5vw, 3rem)` |
| `h3` | 22px / 1.375rem | 36px / 2.25rem | `clamp(1.375rem, 1rem + 1.875vw, 2.25rem)` |
| `h4` | 18px / 1.125rem | 28px / 1.75rem | `clamp(1.125rem, 0.875rem + 1.25vw, 1.75rem)` |

### Paragraph / text classes

| Class | Min size | Max size | clamp() value |
|---|---|---|---|
| `text-xl` | 20px / 1.25rem | 28px / 1.75rem | `clamp(1.25rem, 1rem + 1.25vw, 1.75rem)` |
| `text-lg` | 18px / 1.125rem | 22px / 1.375rem | `clamp(1.125rem, 1rem + 0.625vw, 1.375rem)` |
| `text-base` *(body default)* | 16px / 1rem | 18px / 1.125rem | `clamp(1rem, 0.95rem + 0.25vw, 1.125rem)` |
| `text-sm` | 14px / 0.875rem | 16px / 1rem | `clamp(0.875rem, 0.825rem + 0.25vw, 1rem)` |
| `eyebrow` | 12px / 0.75rem | 14px / 0.875rem | `clamp(0.75rem, 0.7rem + 0.25vw, 0.875rem)` |

### Typography rules

- Heading **element** controls semantics; heading **class** controls visual size
- To use an `h3` tag that looks like an `h2`: set element to `h3`, apply class `h2`
- Never override font sizes at specific breakpoints — let `clamp()` handle it
- Line height: headings `1.1–1.2`, body text `1.5–1.6`

---

## Variables

Variables are organized into collections in Webflow. Update these first when setting up a new project:

| Collection | Controls |
|---|---|
| **Spacing** | Full spacing scale from 0px to 90px in rem units |
| **Typography** | Font families, fluid clamp() sizes for all type levels |
| **Colors** | Base color swatches (primary, secondary, neutral, etc.) |
| **Theme** | Background, text, border, accent colors per mode |
| **Layout** | Container max-width, grid gaps, gutters |

---

## Utility Classes

Utility classes are used sparingly. Avoid Combo Classes unless strictly necessary (e.g. a modal "hide" state).

### Visibility

```
hide              → display: none
hide-tablet       → hidden at tablet breakpoint
hide-landscape    → hidden at mobile landscape
hide-portrait     → hidden at mobile portrait
show              → display: block
show-tablet
show-landscape
show-portrait
opacity-0         → opacity: 0
```

### Display

```
z-index-XXX       → z-index value
overflow-hidden
overflow-scroll
overflow-auto
inline
inline-tablet
inline-mobile
```

### Aspect Ratio (for images and CMS grids)

```
aspect-1x1        → square
aspect-4x3
aspect-3x2
aspect-8x5
aspect-16x9
aspect-21x9
```

---

## Building Workflows

Choose one or combine approaches:

| Workflow | Description |
|---|---|
| **Scaffolding** | Build structure first without naming, then go back and name all elements. Similar to code refactoring. |
| **Clone** | Create a base page structure (skin), then clone it for other pages and name classes on the go. |
| **Atomic** | Build all components first (Navbar, Footer, cards, etc.), then assemble pages. |
| **Style Guide** | Define a style guide first, then build. Best for advanced users. Risk of naming errors is higher. |

---

## Anti-patterns

- **"Div Block 37" or "Text Block 12"** — every element must be named following the chain convention
- **Combo Classes** — avoid unless strictly necessary; merge or redo the class instead
- **Native Webflow Columns/Containers** — use divs; they're easier to maintain
- **Magic numbers** — avoid arbitrary fixed px values for width/height; use spacing variables
- **Hadouken nesting** — avoid excessive divs inside divs inside divs
- **Spacing on low-level elements** — spacing belongs in containers and section wrappers
- **Custom Code Blocks** — use Webflow native features; create a global CSS component if needed
- **Images without alt text** — always add descriptive alt text
- **px units** — prefer rem for consistency and accessibility
- **Manual font size overrides at breakpoints** — use clamp() fluid scale instead

---

## Known Webflow MCP Limitations (as of early 2026)

- **Duplicating pages** — no native API endpoint. Create a blank page via API and ask the user to copy content manually in the Designer.
- **Component property overrides on single-locale sites** — `update_static_content` only works with secondary locales. Button text, Accordion titles, etc. must be edited manually in the Designer's Properties panel.
- **Rich Text inside nested components** — same locale restriction. Requires manual editing.
- **Component Slots** — not yet supported by the Webflow MCP. Main blocker for fully automated page building.
