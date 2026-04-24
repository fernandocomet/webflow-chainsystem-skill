# Webflow ChainSystem Skill for Claude

A Claude skill for building Webflow projects using **ChainSystem** — a kebab-case class naming system designed to be fast, clear, intuitive and productive.

> **Created by [Fernando Comet](https://fernandocomet.com)**. ChainSystem is an original framework built for Webflow projects following the KISS methodology.

---

## What is ChainSystem?

ChainSystem is a class naming convention for Webflow that follows a simple chain structure:

```
page → section → container → element → detail
```

Each class name tells you exactly where you are in the document flow. Every page is a **skin** — all its elements start with the page name, making navigation and debugging fast and intuitive.

```
home-header
home-header-container
home-header-h1
home-header-h2
home-header-cta
```

---

## What this skill covers

- **Core principles** — KISS methodology, one class per element, no magic numbers
- **Kebab-case naming convention** — chain depth rules, context reset, page skin system
- **Custom grid system** — `cs-grid` / `cs-cell` classes with responsive variants
- **Spacing variables** — standardized scale from `0px` to `90px` in rem units
- **Fluid typography** — `clamp()` scale for all heading and text levels (320px → 1440px)
- **Variable collections** — Spacing, Typography, Colors, Theme, Layout
- **Utility classes** — visibility, display, aspect ratio helpers
- **Building workflows** — Scaffolding, Clone, Atomic, Style Guide approaches
- **Anti-patterns** — what to avoid to keep projects clean and maintainable
- **Webflow MCP limitations** — documented known constraints as of early 2026

---

## What works with the Webflow MCP

Tested and validated against live Webflow projects:

### ✅ Works well
- List sites, pages, and CMS collections
- Add fields to CMS collections and populate them with AI-generated content
- List all components and inspect their properties and property IDs
- Create new pages and update their title, slug, and SEO metadata
- Edit text directly on canvas elements — headings, paragraphs, and string nodes
- Hide elements via inline style attributes
- Update page-level settings programmatically

### ⚠️ Known API limitations

1. **Duplicating pages** — no native API endpoint. Create a blank page via API and ask the user to copy content manually in the Designer.
2. **Component property overrides on single-locale sites** — `update_static_content` only works with secondary locales. Button text, Accordion titles, etc. must be edited manually in the Designer's Properties panel.
3. **Rich Text inside nested components** — same locale restriction. Requires manual editing.
4. **Component Slots** — not yet supported by the Webflow MCP. Main blocker for fully automated page building.

---

## How to use

1. Add the `SKILL.md` file to your Claude project or attach it at the start of your conversation
2. Make sure the [Webflow connector](https://webflow.com/blog/webflow-claude-connector) is set up in Claude
3. Start prompting Claude about your ChainSystem-based Webflow project

---

## Demo & Docs

- 🌐 **ChainSystem site:** [chainsystem.webflow.io](https://chainsystem.webflow.io)
- 📦 **Cloneable:** [Clone ChainSystem on Webflow](https://webflow.com/made-in-webflow/website/chainsystem)

---

## Credits

- **ChainSystem** created by [Fernando Comet](https://fernandocomet.com)
- Tested using [Claude](https://claude.ai) + [Webflow MCP](https://developers.webflow.com/mcp/v1.0.0/reference/overview)

---

## Contributing

Found something that works (or doesn't)? PRs and issues welcome. As the Webflow MCP evolves and adds support for Component Slots and primary locale updates, this skill will become significantly more powerful.
