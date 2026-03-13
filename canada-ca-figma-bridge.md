---
name: gc-figma-bridge
description: >
  Bridge between Canada.ca / GCWeb HTML code and Figma designs using the GC Design Library – IRCC.
  Use this skill whenever the user wants to: convert a Canada.ca page or HTML snippet into a Figma design;
  convert a Figma design from the GC Design Library into GCWeb/WET-BOEW HTML; generate design variations
  of a Canada.ca page in Figma; or sync code and design across the Figma ↔ GitHub workflow.
  Also trigger when the user mentions "Figma MCP", "GC Design Library", "IRCC library", "bring to Figma",
  "bring to code", "Figma component", or asks to translate between design and code in a Government of Canada context.
  Always use this skill alongside the canada-ca-coder skill when generating or reviewing HTML.
---

# GC Figma Bridge

You are an expert at moving fluidly between Canada.ca HTML (GCWeb/WET-BOEW) and Figma designs using the **GC Design Library – IRCC**.

The two directions are:
- **HTML → Figma**: Parse WET-BOEW markup, map each element to its Figma library component, build the frame.
- **Figma → HTML**: Read the Figma frame, map each component back to its canonical GCWeb pattern, output compliant code.

Both directions share the same component mapping. Custom elements (no official component) are handled with a documented fallback approach.

---

## Core References

- **Figma library file key:** `*********` (GC Design Library – IRCC)
- **GCWeb docs:** https://wet-boew.github.io/GCWeb/index-en.html
- **Canada.ca design system:** https://design.canada.ca/
- **Full component mapping:** Read the **gc-component-mapping** skill's SKILL.md before starting any conversion task. It contains all 37+ verified Figma component names, canonical HTML patterns, mandatory/provisional status, and reconciliation notes.

---

## Workflow: HTML → Figma

**Goal:** Produce an editable Figma frame where every element uses a GC Design Library component where one exists, and a clearly annotated custom frame where one doesn't.

### Steps

1. **Read the component mapping** — read the `gc-component-mapping` skill's SKILL.md before touching Figma.

2. **Parse the HTML** — identify every structural element:
   - Page-level wrappers (`<main>`, `<header>`, `<footer>`)
   - GCWeb-specific classes (e.g. `gc-features`, `wb-fieldflow`, `gc-subway`)
   - WET-BOEW plugin hooks (e.g. `wb-tabs`, `wb-mltmd`)
   - Custom/departmental patterns (classes not in GCWeb docs)

3. **Map to Figma components** — for each element:
   - If a matching Figma component exists → use it from the library (`***********`)
   - If no component exists → build a custom frame (see Custom Elements below)

4. **Assemble the frame** — lay out components top-to-bottom in page order. Use the GCWeb 12-column grid (992px desktop baseline). Match spacing using the library's spacing tokens where available.

5. **Annotate** — add a notes layer identifying:
   - Which components came from the library vs. custom-built
   - Any content that couldn't be automatically mapped (e.g. dynamic data, AJAX-loaded menus)

---

## Workflow: Figma → HTML

**Goal:** Produce valid, accessible GCWeb/WET-BOEW HTML that faithfully reflects the Figma design, ready for the GitHub repo.

### Steps

1. **Read the component mapping** — read the `gc-component-mapping` skill's SKILL.md before writing any code.

2. **Inventory the Figma frame** — list every component instance and its library name.

3. **Map to HTML** — for each component:
   - Look up the canonical HTML pattern in the mapping
   - Use exact GCWeb classes — never invent class names
   - For custom frames (no library component), apply the Custom Elements rules below

4. **Output the HTML** following the `canada-ca-coder` skill rules:
   - Start at `<main>` — no `<html>`, `<head>`, `<body>`, header, or footer
   - Include all text content verbatim
   - No inline `style=""` — use WET utility classes
   - No custom JS for interactions WET already handles

5. **Flag deviations** — if the Figma design uses a pattern that doesn't map cleanly to a GCWeb component, note it as a comment in the HTML:
   ```html
   <!-- CUSTOM: No GCWeb equivalent for this pattern. Implemented as [description]. Review before publish. -->
   ```

---

## Custom Elements (No Official Component)

Not everything needs to be an official GCWeb component. When a design element has no library equivalent:

### In Figma (HTML → Figma direction)
- Build a custom frame using the GC Design Library's **colour tokens**, **spacing tokens**, and **typography styles** — never hardcode hex values or pixel sizes that exist as tokens.
- Name the layer clearly: `[Custom] Element description` so it's distinguishable from library components.
- Add a note: "No GCWeb component. Built to Canada.ca visual standards. Requires dev review."

### In HTML (Figma → HTML direction)
- Use semantic HTML (`<section>`, `<nav>`, `<ul>`, `<dl>`, `<figure>`, etc.)
- Use GCWeb utility classes for spacing, typography, and grid (`col-md-*`, `mrgn-tp-*`, `text-*`)
- Use Bootstrap 3 patterns (GCWeb's underlying framework) for layout
- Add the comment flag above
- Never write custom CSS unless there is absolutely no WET utility class that achieves the same result — and if you must, note it clearly

### Deciding whether to use a component or go custom
| Situation | Approach |
|---|---|
| Exact match in Figma library | Use the component |
| Close match but wrong variant | Use the closest component + note the deviation |
| Pattern exists in GCWeb but not Figma library | Use GCWeb HTML; note that a Figma component is missing |
| Pattern is IRCC-specific / departmental | Custom (Figma frame + semantic HTML) |
| Pattern violates Canada.ca design system | Flag it; don't silently implement it |

---

## Conversion Quality Rules

These apply in both directions:

1. **Component-first** — always check the mapping before going custom.
2. **Tokens over values** — use design tokens and GCWeb classes, not hardcoded colours or sizes.
3. **Accessibility preserved** — WCAG 2.1 AA must be maintained. Don't drop `aria-*`, `id`, `property`, or `typeof` attributes when converting to/from Figma.
4. **Bilingual readiness** — designs and code must accommodate both English and French. Flag any hardcoded strings that would need translation.
5. **Mandatory components stay mandatory** — Global Header, Breadcrumb, Footer, Date Modified, and Language Toggle are always present. Never remove them from a design or code output.
6. **Provisional components** — components marked `provisional` in GCWeb (Most Requested, In-page TOC, Subway, etc.) can be used, but flag them: they may change in future GCWeb releases.

---

## Quick Component Lookup

For the full mapping with canonical HTML patterns, read the `gc-component-mapping` skill. Here's a quick reference for the most common components:

| Figma Component | Key GCWeb Class | HTML Element |
|---|---|---|
| Global header | `#wb-bnr` | `<header>` |
| Site Footer | `#wb-info` | `<footer>` |
| Breadcrumb (inside header) | `#wb-bc` | `<nav>` |
| Buttons | `btn btn-[variant]` | `<button>` or `<a>` |
| Alerts and labels | `alert alert-[type]` | `<section>` (not `<div>`) |
| Checkboxes and radio buttons | `.gc-chckbxrdio` | `<fieldset>` |
| Context-Specific Features | `.gc-features` | `<section>` |
| Most requested | `.gc-most-requested` | `<section>` |
| Subway & SIT | `.gc-subway` / `.gc-stp-stp` | `<nav>` / `<div>` |
| Expand/collapse | *(native)* | `<details><summary>` |
| Tabs | `.wb-tabs` | `<div>` |
| Tables | `.wb-tables .table` | `<table>` |
| Topic Doormat | `.gc-drmt` | `<div>` |
| In-page Table of Contents | `.gc-toc` | `<nav>` |
| Steps list | `.lst-steps` | `<ol>` |
| Panel | `.panel .panel-[variant]` | `<div>` |
| Download Links | `.gc-dwnld` | `<ul>` |
| Share this page | `.wb-share` | `<div>` |
| Multimedia | `.wb-mltmd` | `<figure>` |
| Interactive Questions | `.wb-fieldflow` | `<div>` |

---

## Figma MCP Usage Notes

When using the Figma MCP to read or write frames:

- **Always specify the library file key** (`********`) when inserting components — don't use local copies.
- **Component names are case-sensitive** in the Figma API. Use exact names from the mapping table.
- **The GCWeb menu is AJAX-loaded** — represent it in Figma as a static placeholder; don't try to replicate the full dynamic menu.
- **When reading a Figma frame**, check whether components are library instances (linked to `*********`) or detached/custom frames. Detached instances should be treated as custom elements.
- **Page width:** Use 1440px artboard with a 12-column grid at 992px content width (matching GCWeb's Bootstrap 3 grid).

---

## What to Do When Stuck

| Problem | Action |
|---|---|
| GCWeb class not in mapping | Check https://wet-boew.github.io/GCWeb/index-en.html; add to mapping if found |
| Figma component not in mapping | Check the library file directly; add to mapping; flag for skill update |
| Design violates Canada.ca IA spec | Flag it, don't implement silently — note the specific violation |
| Mandatory component missing from design | Add it back; note the addition in output |
| Provisional component used | Implement it; add `<!-- PROVISIONAL: may change in future GCWeb releases -->` |
