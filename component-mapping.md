---
name: gc-component-mapping
description: >
  GCWeb / WET-BOEW component mapping reference for the GC Design Library – IRCC (Figma).
  This is a shared reference skill — do not invoke it directly. It is used by the canada-ca-coder
  and gc-figma-bridge skills when they need the canonical Figma component name ↔ GCWeb HTML mapping.
  Contains all 37+ verified Figma component names, their GCWeb classes, canonical HTML patterns,
  mandatory vs. provisional status, grid system, utility classes, and reconciliation notes.
---

# GCWeb / WET-BOEW Component Mapping
**For use with Claude Code + Figma MCP + GC Design Library (IRCC)**
Figma Library File Key: `8vPYwBpcscTJfI4Z6qzESX`
Source: Canada.ca patterns and templates audit spreadsheet
GCWeb version: 18.2.0 (2026-02-03)

---

## How to use this mapping

When converting Figma designs → HTML or HTML → Figma:
- **Figma → HTML**: Match Figma component names to the "GCWeb Class(es)" column and use the canonical HTML pattern.
- **HTML → Figma**: Match WET-BOEW CSS classes to the Figma component name in the GC Design Library.
- Components marked `(no URL / no WET component)` have no direct GCWeb equivalent and must be handled with Canada.ca content guidance only.

---

## Mandatory Site Components

### Global Header
**GCWeb doc:** `sites/header/header-docs-en.html`
**Key classes:** `#wb-bnr`, `#wb-lng`, `#wb-srch`, `.brand`
**Canonical pattern:**
```html
<header>
  <div id="wb-bnr" class="container">
    <section id="wb-lng" class="text-right">
      <h2 class="wb-inv">Language selection</h2>
      <ul class="list-inline margin-bottom-none">
        <li><a lang="fr" href="[fr-url]">Français</a></li>
      </ul>
    </section>
    <div class="row">
      <div class="brand col-xs-5 col-md-4" property="publisher" typeof="GovernmentOrganization">
        <a href="https://www.canada.ca/en.html" property="url">
          <img src="/GCWeb/assets/sig-blk-en.svg" alt="" property="logo">
          <span class="wb-inv" property="name"> Government of Canada / <span lang="fr">Gouvernement du Canada</span></span>
        </a>
      </div>
      <section id="wb-srch" class="col-lg-8 text-right visible-md visible-lg">
        <h2>Search</h2>
        <form action="#" method="post" role="search" class="form-inline">
          <div class="form-group">
            <label for="wb-srch-q" class="wb-inv">Search Canada.ca</label>
            <input id="wb-srch-q" class="wb-srch-q form-control" name="q" type="search" size="34" maxlength="170" placeholder="Search Canada.ca">
          </div>
          <button type="submit" class="btn btn-primary btn-small"><span class="glyphicon-search glyphicon"></span><span class="wb-inv">Search</span></button>
        </form>
      </section>
    </div>
  </div>
  <!-- GCWeb Menu goes here -->
</header>
```
**Notes:** Mandatory on all pages. Government of Canada signature must link to Canada.ca home. Language toggle mandatory.

---

### Government of Canada Signature
**GCWeb doc:** Part of header (`sites/header/header-docs-en.html`)
**Key classes:** `.brand`, `sig-blk-en.svg` / `sig-blk-fr.svg`
**Canonical pattern:**
```html
<div class="brand col-xs-5 col-md-4">
  <a href="https://www.canada.ca/en.html">
    <img src="/GCWeb/assets/sig-blk-en.svg" alt="">
    <span class="wb-inv"> Government of Canada / <span lang="fr">Gouvernement du Canada</span></span>
  </a>
</div>
```

---

### Theme and Topic Menu (GCWeb Menu)
**GCWeb doc:** `sites/gcweb-menu/gcweb-menu-docs-en.html`
**Key classes:** `nav.gcweb-menu`, `typeof="SiteNavigationElement"`
**Canonical pattern:**
```html
<nav class="gcweb-menu" typeof="SiteNavigationElement">
  <h2 class="wb-inv">Menu</h2>
  <button type="button" aria-haspopup="true" aria-expanded="false">
    Menu <span class="expicon glyphicon glyphicon-chevron-down"></span>
  </button>
  <ul role="menu" aria-orientation="vertical" data-ajax-replace="https://www.canada.ca/content/dam/canada/sitemenu/sitemenu-v2-en.html">
    <!-- Menu items loaded via Ajax -->
  </ul>
</nav>
```
**Notes:** Use CDN-hosted menu via `data-ajax-replace`. Current EN CDN: `https://cdn.canada.ca/gcweb-cdn-live/sitemenu/sitemenu-v5-en.html`

---

### Breadcrumb Trail
**GCWeb doc:** `sites/breadcrumbs/breadcrumbs-en.html`
**Key classes:** `#wb-bc`, `.breadcrumb`, `typeof="BreadcrumbList"`
**Status:** Stable | **Mandatory:** Yes
**Canonical pattern:**
```html
<nav id="wb-bc" property="breadcrumb">
  <h2>You are here:</h2>
  <div class="container">
    <ol class="breadcrumb" typeof="BreadcrumbList">
      <li property="itemListElement" typeof="ListItem">
        <a property="item" typeof="WebPage" href="https://www.canada.ca/en.html">
          <span property="name">Canada.ca</span>
        </a>
        <meta property="position" content="1">
      </li>
      <li property="itemListElement" typeof="ListItem">
        <a property="item" typeof="WebPage" href="[parent-url]">
          <span property="name">[Parent page]</span>
        </a>
        <meta property="position" content="2">
      </li>
      <!-- Current page is NEVER included as last item -->
    </ol>
  </div>
</nav>
```
**Rules:** First item always "Canada.ca". Current page never shown. Use chevron right (›) as separator. Shorten long titles.

---

### Language Toggle Link
**GCWeb doc:** `sites/language/language-en.html`
**Key classes:** `#wb-lng`
**Canonical pattern:**
```html
<section id="wb-lng" class="text-right">
  <h2 class="wb-inv">Language selection</h2>
  <ul class="list-inline margin-bottom-none">
    <li><a lang="fr" href="[equivalent-fr-page]">Français</a></li>
  </ul>
</section>
```

---

### Site Search Box
**GCWeb doc:** Part of header (`sites/header/header-docs-en.html`)
**Key classes:** `#wb-srch`, `.wb-srch-q`
**Notes:** Integrated into header. See Global Header pattern above.

---

### Global Footer
**GCWeb doc:** `sites/footers/footers-en.html`
**Key classes:** `#wb-info`, `.gc-contextual`, `.gc-main-footer`, `.gc-sub-footer`
**Status:** Stable | **Mandatory:** Yes
**Canonical pattern:**
```html
<footer id="wb-info">
  <h2 class="wb-inv">About this site</h2>

  <!-- Band 1: Contextual (optional, institution-specific) -->
  <div class="gc-contextual">
    <div class="container">
      <nav>
        <h3>[Contextual footer header]</h3>
        <ul class="list-col-xs-1 list-col-sm-2 list-col-md-3">
          <li><a href="#">Contextual link 1</a></li>
        </ul>
      </nav>
    </div>
  </div>

  <!-- Band 2: Main footer (Government of Canada links) -->
  <div class="gc-main-footer">
    <div class="container">
      <nav>
        <h3>Government of Canada</h3>
        <ul class="list-col-xs-1 list-col-sm-2 list-col-md-3">
          <li><a href="https://www.canada.ca/en/contact.html">All contacts</a></li>
          <li><a href="https://www.canada.ca/en/government/dept.html">Departments and agencies</a></li>
          <li><a href="https://www.canada.ca/en/government/system.html">About government</a></li>
        </ul>
      </nav>
    </div>
  </div>

  <!-- Band 3: Sub-footer (mandatory links + wordmark) -->
  <div class="gc-sub-footer">
    <div class="container d-flex align-items-center">
      <nav>
        <h3 class="wb-inv">Government of Canada Corporate</h3>
        <ul>
          <li><a href="https://www.canada.ca/en/social.html">Social media</a></li>
          <li><a href="https://www.canada.ca/en/mobile.html">Mobile applications</a></li>
          <li><a href="https://www.canada.ca/en/government/about.html">About Canada.ca</a></li>
          <li><a href="https://www.canada.ca/en/transparency/terms.html">Terms and conditions</a></li>
          <li><a href="https://www.canada.ca/en/transparency/privacy.html">Privacy</a></li>
        </ul>
      </nav>
      <div class="wtrmrk align-self-end ms-auto">
        <img src="/GCWeb/assets/wmms-blk.svg" alt="Symbol of the Government of Canada">
      </div>
    </div>
  </div>
</footer>
```

---

### Date Modified
**GCWeb doc:** `sites/date-modified/date-modified-en.html`
**Key classes:** `.gc-pg-lst-dt`, `.provisional.dl-inline`
**Status:** Stable | **Mandatory:** Yes
**Canonical pattern:**
```html
<dl id="wb-dtmd">
  <dt>Date modified:</dt>
  <dd>
    <time property="dateModified">YYYY-MM-DD</time>
  </dd>
</dl>
```

---

### Page Feedback Tool
**GCWeb doc:** `sites/feedback/feedback-docs-en.html`
**Key classes:** `.gc-pg-feedback`
**Canonical pattern:**
```html
<div class="row row-no-gutters mrgn-tp-xl">
  <div class="col-sm-7 col-lg-6">
    <section class="gc-pg-feedback provisional">
      <h2>Did you find what you were looking for?</h2>
      <ul class="list-unstyled list-inline">
        <li class="list-inline-item mrgn-bttm-md">
          <button class="btn btn-success">Yes</button>
        </li>
        <li class="list-inline-item mrgn-bttm-md">
          <button class="btn btn-default btn-danger">No</button>
        </li>
      </ul>
    </section>
  </div>
</div>
```

---

### Report a Problem
**GCWeb doc:** `sites/feedback/report-problem-en.html`
**Key classes:** `#gc-pg-crnt`
**Notes:** Usually paired with Page Feedback Tool in the page details section.

---

## Design Patterns (Components)

### Buttons
**GCWeb doc:** `common/button/button-en.html`
**Status:** Stable
**Key classes:**

| Variant | Class | Use case |
|---|---|---|
| Default | `btn btn-default` | Secondary actions |
| Primary | `btn btn-primary` | Main action |
| Call to Action (Supertask) | `btn btn-call-to-action` | Top task / hero CTA |
| Success | `btn btn-success` | Positive confirmation |
| Warning | `btn btn-warning` | Caution action |
| Danger | `btn btn-danger` | Destructive action |
| Info | `btn btn-info` | Informational action |
| Link | `btn btn-link` | De-emphasized action |

**Size modifiers:** `btn-lg`, `btn-sm`, `btn-xs`
**Canonical patterns:**
```html
<!-- Primary button -->
<button type="button" class="btn btn-primary">Primary</button>

<!-- Supertask / Call to Action -->
<button type="button" class="btn btn-call-to-action">Apply now</button>

<!-- Link styled as button -->
<a class="btn btn-primary" href="#">Link button</a>
```
**Rule:** Never use `role="button"` on `<a>` tags. Use actual `<button>` for actions, `<a>` for navigation.

---

### Contextual Alerts
**GCWeb doc:** `common/alert/alerts-en.html`
**Status:** Stable
**Key classes:** `alert alert-[type]`

| Variant | Class | When to use |
|---|---|---|
| Success | `alert alert-success` | Positive outcome |
| Info | `alert alert-info` | General information |
| Warning | `alert alert-warning` | Caution / attention needed |
| Danger | `alert alert-danger` | Error or critical issue |

**Canonical pattern (GCWeb specific — uses `<section>` not `<div>`):**
```html
<section class="alert alert-warning">
  <h3>Warning title</h3>
  <p>Alert content with optional <a href="#" class="alert-link">link text</a>.</p>
</section>
```
**Note:** GCWeb uses `<section>` (not `<div>`) with a heading inside. This differs from plain Bootstrap.

---

### Checkboxes and Radio Buttons
**GCWeb doc:** `components/gc-chckbxrdio/gc-chckbxrdio-doc-en.html`
**Status:** Stable
**Key classes:** `.gc-chckbxrdio`
**Canonical pattern:**
```html
<!-- Large checkboxes (default) -->
<fieldset class="gc-chckbxrdio">
  <legend>Choose options</legend>
  <ul class="list-unstyled lst-spcd-2">
    <li class="checkbox">
      <input type="checkbox" id="opt1">
      <label for="opt1">Option 1</label>
    </li>
  </ul>
</fieldset>

<!-- Inline form (smaller tickbox) -->
<div class="checkbox gc-chckbxrdio">
  <input id="remember" type="checkbox">
  <label for="remember">Remember me</label>
</div>
```
**Rule:** Must use explicit labels only. Cannot use implicit labels.

---

### Context-Specific Features
**GCWeb doc:** `components/gc-features/gc-features-en.html`
**Status:** Stable
**Key class:** `.gc-features`
**Canonical pattern (3-column default):**
```html
<section class="gc-features">
  <h2>[Features title]</h2>
  <div class="row wb-eqht-grd">
    <div class="col-lg-4 col-sm-6">
      <div class="well well-sm eqht-trgt">
        <img src="[img]" alt="[alt]">
        <h3><a class="stretched-link" href="#">[Feature title]</a></h3>
        <p>[Description]</p>
      </div>
    </div>
  </div>
</section>
```

---

### Data Tables
**GCWeb doc:** `components/gc-table/gc-table-en.html`
**Status:** Provisional
**Key classes:** `.wb-tables`, `.table`, `.table-bordered`
**Canonical pattern:**
```html
<table class="wb-tables table table-bordered" data-wb-tables='{"paging": false}'>
  <caption>[Table caption]</caption>
  <thead>
    <tr>
      <th scope="col">Column 1</th>
      <th scope="col">Column 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Data</td>
      <td>Data</td>
    </tr>
  </tbody>
</table>
```

---

### Download Links
**GCWeb doc:** `components/gc-dwnld/download_link-en.html`
**Status:** Stable
**Key class:** `.gc-dwnld`
**Canonical pattern:**
```html
<ul class="gc-dwnld">
  <li>
    <a class="gc-dwnld-lnk" href="[file.pdf]">
      <img src="/GCWeb/assets/gc-dwnld.svg" alt="">
      [File title] <span class="gc-dwnld-info">(<abbr title="Portable Document Format">PDF</abbr>, 1.5 <abbr title="megabytes">MB</abbr>)</span>
    </a>
  </li>
</ul>
```

---

### Expand/Collapse (Details/Summary)
**GCWeb doc:** `wet-boew/demos/details/details-en.html`
**Key elements:** `<details>`, `<summary>`
**Canonical pattern:**
```html
<details>
  <summary>[Collapsed heading / question]</summary>
  <p>[Expanded content]</p>
</details>
```

---

### In-Page Table of Contents
**GCWeb doc:** `components/gc-toc/toc-en.html`
**Status:** Provisional
**Key class:** `.gc-toc`
**Canonical pattern:**
```html
<nav class="gc-toc">
  <h2 class="wb-inv">On this page</h2>
  <ol>
    <li><a href="#section1">Section 1</a></li>
    <li><a href="#section2">Section 2</a></li>
  </ol>
</nav>
```

---

### Interactive Questions (Fieldflow)
**GCWeb doc:** `components/wb-fieldflow/fieldflow-doc-en.html`
**Key class:** `.wb-fieldflow`
**Canonical pattern:**
```html
<div class="wb-fieldflow" data-wb-fieldflow='{"defaultRedir":"#no-match"}'>
  <p>What do you want to do?</p>
  <ul>
    <li><a href="[url-1]">Option 1</a></li>
    <li><a href="[url-2]">Option 2</a></li>
  </ul>
</div>
```

---

### Most Requested
**GCWeb doc:** `components/gc-most-requested/gc-most-requested-en.html`
**Status:** Provisional
**Key class:** `.gc-most-requested`
**Canonical pattern:**
```html
<section class="gc-most-requested provisional">
  <h2>Most requested</h2>
  <ul>
    <li><a href="#">Top task 1</a></li>
    <li><a href="#">Top task 2</a></li>
    <li><a href="#">Top task 3</a></li>
  </ul>
</section>
```

---

### Ordered Multi-Page Navigation (Step by Step)
**GCWeb doc:** `components/gc-stp-stp/gc-stp-stp-doc-en.html`
**Status:** Stable
**Key class:** `.gc-stp-stp`
**Notes:** Insert directly after the institutional byline. Shows numbered steps with current step highlighted.

---

### Services and Information
**GCWeb doc:** `components/gc-servinfo/gc-srvinfo.html`
**Key class:** `.gc-srvinfo`
**Canonical pattern:**
```html
<section class="gc-srvinfo">
  <h2 class="wb-inv">Services and information</h2>
  <div class="row wb-eqht-grd">
    <div class="col-sm-6">
      <h3><a href="#">[Service title]</a></h3>
      <p>[Short description]</p>
    </div>
  </div>
</section>
```

---

### Sign In Button (Authentication)
**GCWeb doc:** `sites/authentication/authentication-en.html`
**Key classes:** `#wb-so`, `.btn-primary`
**Canonical pattern (contextual sign-in):**
```html
<section id="wb-so">
  <h2 class="wb-inv">Sign in</h2>
  <a class="btn btn-primary" href="[sign-in-url]">Sign in</a>
</section>
```

---

### Subway Navigation
**GCWeb doc:** `components/gc-subway/docs-en.html`
**Status:** Provisional
**Key class:** `.gc-subway`
**Notes:** Used for multi-section service flows. Index page layout differs from section pages. Do not include sub-section items on index page.

---

## Page Templates

### Basic Page Layout (Content Page)
**GCWeb doc:** `templates/content-page/content-en.html`
**Key structure:**
```html
<!DOCTYPE html>
<html class="no-js" lang="en" dir="ltr">
<head>
  <meta charset="utf-8">
  <title>[Page title] - Canada.ca</title>
  <link rel="stylesheet" href="/GCWeb/css/theme.min.css">
</head>
<body vocab="http://schema.org/" typeof="WebPage">
  <!-- Skip links, header, breadcrumb, main, footer, JS -->
  <main property="mainContentOfPage" resource="#wb-main" typeof="WebPageElement" class="container">
    <h1 property="name" id="wb-cont">[Page title]</h1>
    <!-- Content -->
    <dl id="wb-dtmd">
      <dt>Date modified:</dt>
      <dd><time property="dateModified">YYYY-MM-DD</time></dd>
    </dl>
  </main>
  <script src="/wet-boew/js/wet-boew.min.js"></script>
  <script src="/GCWeb/js/theme.min.js"></script>
</body>
</html>
```

---

### Campaign Page
**GCWeb doc:** `templates/campaign/campaign-en.html`
**Notes:** Has a distinct look with hero banner. Uses the promotional thematic system.

### Contact Us Page
**GCWeb doc:** `templates/institutional/institution-contact-en.html`

### Departments and Agencies Page
**GCWeb doc:** `templates/dept-en.html`

### Government-Wide Audience Page
**GCWeb doc:** `templates/gc-audience-en.html`
**Key class:** `.gc-audience`

### Guidance on Legislation / Act Profile Page
**GCWeb doc:** `templates/legislation/act-en.html`

### Home Page
**GCWeb doc:** `templates/home/home-en.html`
**Notes:** Requires `class="home"` on `<body>`.

### Institutional Landing Page
**GCWeb doc:** `templates/institutional/institution-en.html`

### Ministerial Profile Page
**GCWeb doc:** `templates/ministerial/ministerial-doc-en.html`

### News Landing Page
**GCWeb doc:** `templates/news/news-doc-en.html`

### Promotional Events Page
**GCWeb doc:** `templates/event-en.html`

### Regulation Profile Page
**GCWeb doc:** `templates/legislation/regulations-en.html`

### Search Page
**GCWeb doc:** `templates/search/api-en.html`

### Service Initiation Page
**GCWeb doc:** `templates/advancedservice/index-en.html`

### Theme and Topic Page
**GCWeb doc:** `templates/topic/topic-en.html`
**Notes:** Also hosts: Contributors, More information for, Social media channels block, What we are doing.

---

## Components with No GCWeb URL (content/policy-level only)

These components exist as Canada.ca design guidance but have no dedicated GCWeb HTML template. They are implemented through content organization and writing, not WET-BOEW classes.

| Component | Notes |
|---|---|
| Canada.ca domain | Domain policy, not a coded component |
| Colours | Use GCWeb CSS variables/theme — no standalone component |
| Consultation profile page | No current GCWeb template |
| Contact information | Content pattern — no dedicated template |
| Faceted finder page | No current GCWeb template |
| Finder page | No current GCWeb template |
| Institutional byline | Rendered via GCWeb page details section |
| Layouts | Covered by Bootstrap 3 grid (`div.row`, `div.col-*-*`) |
| News product page | No current GCWeb template |
| News results page | No current GCWeb template |
| Partnering and collaborative arrangement profile page | No current GCWeb template |
| Privacy disclaimer | Content pattern — no dedicated component |
| Program description page | No current GCWeb template |
| Related links | Content pattern |
| Short index page | No current GCWeb template |
| Typography | GCWeb global CSS (Lato font, heading hierarchy) |

---

## WET-BOEW Plugins (from audit — legacy/external)

| Component | WET Plugin | Key class/attribute |
|---|---|---|
| Carousels | Tabbed interface carousel | `.wb-tabs`, `data-wb-tabs='{"cycle": true}'` |
| Charts and graphs | Charts plugin | `.wb-charts` |
| Multimedia (video/audio) | Multimedia player | `.wb-mltmd` |
| Share this page | Share widget | `.wb-share` |
| Tabbed interface | Tabs plugin | `.wb-tabs` |

---

## Grid System Reference

GCWeb uses Bootstrap 3 grid. Always use these — never custom CSS grid or flexbox overrides.

```html
<!-- Two-column layout -->
<div class="row">
  <div class="col-md-8">Main content</div>
  <div class="col-md-4">Sidebar</div>
</div>

<!-- Full-width -->
<div class="row">
  <div class="col-xs-12">Full width</div>
</div>
```

**Breakpoints:** `xs` (<768px), `sm` (>=768px), `md` (>=992px), `lg` (>=1200px)

---

## Key CSS Utility Classes

| Class | Purpose |
|---|---|
| `.wb-inv` | Visually hidden (screen-reader only) |
| `.mrgn-tp-*` | Margin top (sm/md/lg/xl) |
| `.mrgn-bttm-*` | Margin bottom |
| `.mrgn-rght-*` / `.mrgn-lft-*` | Margin right/left |
| `.text-right` / `.text-left` | Text alignment |
| `.pull-right` / `.pull-left` | Float |
| `.visible-md` / `.hidden-xs` | Responsive visibility |
| `.eqht-trgt` | Equal height target (with `.wb-eqht-grd`) |
| `.list-unstyled` | Remove list bullets |
| `.lst-spcd-2` | List with 2x spacing |
| `.stretched-link` | Make entire card/container clickable |

---

## Figma → HTML Mapping (Verified Component Names)

These are the **exact component names** as they appear in the GC Design Library – IRCC (Figma file key: `8vPYwBpcscTJfI4Z6qzESX`), mapped to their canonical GCWeb/WET-BOEW HTML patterns.

| Figma Component Name | GCWeb Key Class(es) | Canonical HTML Element | Notes |
|---|---|---|---|
| **Alerts and labels** | `alert alert-[warning\|info\|success\|danger]` | `<section class="alert alert-warning">` | GCWeb uses `<section>` + heading, not `<div>` |
| **And/or** | *(utility pattern)* | `<p class="text-center"><strong>or</strong></p>` | Separator between form options; no dedicated class |
| **Bands (zebra)** | `.bg-[light\|dark]`, `.well` | `<div class="well">` | Alternating background sections |
| **Buttons** | `btn btn-[primary\|default\|call-to-action\|warning\|danger\|success\|info\|link]` | `<button type="button" class="btn btn-primary">` | See full button table above |
| **Carousels** | `.wb-tabs` + `data-wb-tabs='{"cycle":true}'` | `<div class="wb-tabs">` | WET-BOEW tabs plugin in carousel mode |
| **Checkboxes and radio buttons** | `.gc-chckbxrdio` | `<fieldset class="gc-chckbxrdio">` | Must use explicit labels; `<fieldset>` + `<legend>` required |
| **Contact Information** | *(content pattern)* | `<address>` or `<dl>` | No dedicated GCWeb class; use semantic HTML |
| **Context-Specific Features** | `.gc-features` | `<section class="gc-features">` | 2- or 3-column image+link cards |
| **Contributors** | `.gc-contributors` | `<section class="gc-contributors">` | Part of topic/page details; lists contributing institutions |
| **Definition list** | *(native HTML)* | `<dl>`, `<dt>`, `<dd>` | Use `.dl-horizontal` for side-by-side layout |
| **Download Links** | `.gc-dwnld` | `<ul class="gc-dwnld">` | Includes file type icon, size info |
| **Dropdown menu** | `.wb-navcurr`, `.dropdown` | `<li class="dropdown">` | Bootstrap 3 dropdown; used in nav contexts |
| **Expand/collapse** | *(native HTML)* | `<details><summary>` | WET polyfill for older browsers; no extra class needed |
| **Global header** | `#wb-bnr`, `.brand`, `#wb-lng`, `#wb-srch` | `<header><div id="wb-bnr">` | Includes GC signature, language toggle, search |
| **H1 Heading and banner** | `#wb-cont`, `.page-header` | `<h1 property="name" id="wb-cont">` | Page title; `id="wb-cont"` required for skip links |
| **In-page Table of Contents** | `.gc-toc` | `<nav class="gc-toc">` | Provisional; auto-generates from headings or manual `<ol>` |
| **Institutional Landing Page** | *(template)* | Full page template | See `templates/institutional/institution-en.html` |
| **Interactive Questions** | `.wb-fieldflow` | `<div class="wb-fieldflow">` | WET-BOEW fieldflow plugin; decision tree/wizard |
| **Latest News** | `.gc-nws`, part of institutional template | `<section class="gc-nws">` | Part of institutional landing page pattern |
| **Lightbox** | `.wb-lbx` | `<a class="wb-lbx" href="#overlay-id">` | WET-BOEW lightbox plugin; modal overlay |
| **Ministerial Profile Page** | *(template)* | Full page template | See `templates/ministerial/ministerial-doc-en.html` |
| **More Information For** | `.gc-most-requested` or topic template section | `<section>` in topic template | Part of the topic page pattern |
| **Most requested** | `.gc-most-requested` | `<section class="gc-most-requested provisional">` | Provisional; lists top tasks |
| **Multimedia** | `.wb-mltmd` | `<figure class="wb-mltmd">` | WET-BOEW multimedia player; handles video + audio |
| **Panel** | `.panel`, `.panel-[default\|primary\|warning\|danger\|info\|success]` | `<div class="panel panel-default">` | Bootstrap 3 panel with optional header/footer |
| **Privacy Disclaimer** | *(content pattern)* | `<section>` with plain prose | No dedicated GCWeb class; policy-level content |
| **Related Links** | *(content pattern)* | `<nav>` or `<ul>` | No dedicated GCWeb class; use semantic list |
| **Share this page** | `.wb-share` | `<div class="wb-share">` | WET-BOEW share widget plugin |
| **Site Footer** | `#wb-info`, `.gc-contextual`, `.gc-main-footer`, `.gc-sub-footer` | `<footer id="wb-info">` | 3-band footer; see full pattern above |
| **Social media channels** | `.gc-follow-us` | `<section class="gc-follow-us">` | Part of topic template; follow us block |
| **Social Media Feeds** | `.wb-feeds` | `<div class="wb-feeds">` | WET-BOEW feeds plugin; pulls RSS/social content |
| **Steps list** | `.lst-steps` | `<ol class="lst-steps">` | Numbered steps with circle styling |
| **Subway & SIT** | `.gc-subway` / `.gc-stp-stp` | `<div class="gc-subway">` | Subway = multi-section nav; SIT = Step-in-time ordered nav |
| **Tables** | `.wb-tables`, `.table`, `.table-bordered` | `<table class="wb-tables table">` | WET-BOEW datatable plugin; add `data-wb-tables` for options |
| **Tabs** | `.wb-tabs` | `<div class="wb-tabs">` | WET-BOEW tabs plugin; keyboard accessible tabbed interface |
| **Theme and Topic Page** | *(template)* | Full page template | See `templates/topic/topic-en.html` |
| **Topic Doormat** | `.gc-drmt` | `<div class="gc-drmt">` | Navigation card linking to subtopics; part of topic template |
| **What we are doing** | part of topic template | `<section>` in topic template | Lists upcoming/current initiatives; part of topic page |

---

## Reconciliation Notes

### In Figma library but NOT in the spreadsheet audit
These components exist in the GC Design Library (IRCC) but were not catalogued in the audit spreadsheet. They still have GCWeb equivalents and should be handled correctly.

| Figma Component | Status | Notes |
|---|---|---|
| **And/or** | Utility pattern | Text separator — `<p class="text-center">or</p>` |
| **Bands (zebra)** | GCWeb utility | `.well` or alternating `.bg-*` sections |
| **Definition list** | Native HTML | `<dl class="dl-horizontal">` |
| **Dropdown menu** | Bootstrap 3 | `.dropdown` class in nav contexts |
| **H1 Heading and banner** | GCWeb site component | `<h1 id="wb-cont">` — required for skip links |
| **Latest News** | Part of institutional template | `.gc-nws` section |
| **Lightbox** | WET-BOEW plugin | `.wb-lbx` |
| **Panel** | Bootstrap 3 | `.panel .panel-default` etc. |
| **Privacy Disclaimer** | Content pattern | No GCWeb class; prose only |
| **Related Links** | Content pattern | No GCWeb class; semantic `<nav>` or `<ul>` |
| **Social Media Feeds** | WET-BOEW plugin | `.wb-feeds` |
| **Steps list** | GCWeb utility | `.lst-steps` |
| **Topic Doormat** | GCWeb component | `.gc-drmt` |

### In the spreadsheet audit but NOT in Figma library
These components were audited but don't have a Figma component in the GC Design Library (IRCC). When generating HTML for these, use GCWeb patterns directly without a Figma counterpart.

| Spreadsheet Component | Notes |
|---|---|
| Basic page layout | Full page template — no single Figma component |
| Campaign page | Full page template |
| Canada.ca domain | Policy, not a component |
| Colours | GCWeb CSS variables only |
| Consultation profile page | No template exists |
| Contact us page | Institutional template |
| Departments and agencies page | Full page template |
| Faceted/Finder pages | No template exists |
| Global footer sub-components (breadcrumb, language toggle, search, sign-in) | Covered inside Global Header component in Figma |
| Government-wide audience page | Full page template |
| Home page | Full page template |
| Icons | WET-BOEW Glyphicons / Font Awesome |
| Images | Native `<img>` with WET utility classes |
| Institutional service performance reporting page | Full page template |
| Language toggle link | Part of Global Header in Figma |
| Long/Short index page | Page template |
| News landing/product/results pages | Templates |
| Ordered multi-page navigation | Covered by Subway & SIT in Figma |
| Page feedback tool | No Figma component — add manually |
| Partnering/collaborative arrangement page | No template |
| Program description page | No template |
| Report a problem | No Figma component — add manually |
| Search page | Full page template |
| Service initiation page | Full page template |
| Site search box | Part of Global Header in Figma |
| Typography | GCWeb global CSS |

---

*Last updated: 2026-02-26*
*Sources: wet-boew.github.io/GCWeb v18.2.0, Canada.ca patterns and templates audit, GC Design Library – IRCC (Figma file: `8vPYwBpcscTJfI4Z6qzESX`)*