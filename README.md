# Canada.ca Skills for Claude

A collection of Claude skills for Government of Canada web teams. These skills help writers, coders, designers, and UX practitioners produce web content that follows the [Canada.ca design system](https://design.canada.ca/), the [Content Style Guide](https://www.canada.ca/en/treasury-board-secretariat/services/government-communications/canada-content-style-guide.html), and the [WET-BOEW / GCWeb](https://wet-boew.github.io/GCWeb/index-en.html) framework.

---

## Skills

### ✍️ canada-ca-writer
**File:** `canada-ca-writer-SKILL.md`

Reviews, rewrites, and creates web content for Canada.ca pages following the official Content Style Guide. Catches plain-language issues, heading problems, verb-first formatting, and bilingual consistency. Also scores content against GC writing standards and explains each improvement.

**Use it when you want to:** draft new page content, improve existing copy, score a page against GC writing standards, or get specific feedback on plain language and structure.

---

### 💻 canada-ca-coder
**File:** `canada-ca-code-SKILL.md`

Generates and reviews HTML for Canada.ca pages using the WET-BOEW framework and GCWeb theme. Applies canonical component patterns, correct class names, and proper page structure. Works alongside the `gc-component-mapping` skill to ensure every element matches the GCWeb specification.

**Use it when you want to:** convert content into a coded Canada.ca page, audit existing HTML for GCWeb compliance, or get correct markup for any GCWeb component.

---

### 🚪 canada-ca-doormat
**File:** `canada-ca-doormat-SKILL.md`

Writes and reviews doormat text for Canada.ca topic pages — the short linked headings and descriptions that guide users to subtopics. Applies the plain-language and scannability rules specific to this navigation pattern.

**Use it when you want to:** write new doormats, review existing ones, or create a full set of doormats for a topic page redesign.

---

### 📊 canada-ca-feedback-analyst
**File:** `canada-ca-feedback-SKILL.md`

Analyzes batches of user feedback collected from Canada.ca pages (GC Feedback tool, surveys, usability sessions). Surfaces themes, top issues, key phrases, and actionable recommendations — without fabricating or paraphrasing quotes.

**Use it when you want to:** make sense of a list of user comments, identify the most common pain points on a page, or prepare a feedback summary for your team.

---

### 🔍 canada-ca-seo
**File:** `canada-ca-metadata-SKILL.md`

Generates and reviews SEO metadata (title tags, meta descriptions, dcterms fields) and structured data (JSON-LD schema.org markup) for Canada.ca pages. Follows both GC standards and general SEO best practices, and only uses content actually present on the page.

**Use it when you want to:** write metadata for a new page, audit existing metadata, add JSON-LD structured data, or improve a page's findability in search engines.

---

### 🎨 gc-figma-bridge
**File:** `canada-ca-figma-bridge.md`

Bridges between Canada.ca HTML and Figma designs using the GC Design Library – IRCC. Converts GCWeb markup into Figma frames (HTML → Figma) and Figma components back into compliant WET-BOEW code (Figma → HTML). Designed to work with the Figma MCP and the IRCC design library.

**Use it when you want to:** bring a coded Canada.ca page into Figma, turn a Figma mockup into production-ready HTML, or keep design and code in sync across a project.

---

### 🧪 ux-reviewer
**File:** `canada-ca-heuristics_SKILL.md`

Conducts heuristic evaluations of Canada.ca pages, service flows, and interface designs. Applies established usability, accessibility, and service design frameworks to produce direct, evidence-grounded findings with severity ratings and specific recommendations.

**Use it when you want to:** get a professional UX critique of a page or flow, evaluate a design decision, assess accessibility and usability, or prepare findings for a design review.

---

### 📋 job-stories-writer
**File:** `canada-ca-job-stories.md`

Turns user feedback, research notes, and raw observations into structured UX artifacts: Job Stories, usability testing scenarios, and user need statements. Uses the standard "When I… I want to… so I can…" format and keeps every story grounded in real user data.

**Use it when you want to:** write job stories for a service redesign, create usability test tasks, structure insights from a research session, or articulate user needs for a product backlog.

---

### 🗺️ gc-component-mapping
**File:** `component-mapping.md`

A shared reference skill — **not meant to be invoked directly**. It contains the canonical mapping between GC Design Library – IRCC Figma component names and their GCWeb/WET-BOEW HTML equivalents (37+ components). Used internally by `canada-ca-coder` and `gc-figma-bridge` to ensure correct class names, element structure, and mandatory vs. provisional status.

**GCWeb version:** 18.2.0 (2026-02-03)
**Figma library:** GC Design Library – IRCC (`********)

---

## How to use these skills

These are [Claude](https://claude.ai) skills — prompt files that give Claude specialized knowledge and behaviour for a specific task. You can use them in **Claude Cowork** (desktop) or **Claude Code** (terminal).

### In Claude Cowork
1. Load the skills folder into your Cowork session.
2. Describe your task in plain language. Claude will automatically select the right skill.
3. You can also mention the skill by name to invoke it directly (e.g. "Use the canada-ca-writer skill to review this page").

### In Claude Code
Add the skills folder to your Claude Code configuration. Each `.md` file is a self-contained skill that Claude will activate based on your request.

---

## References

- [Canada.ca design system](https://design.canada.ca/)
- [Canada.ca Content Style Guide](https://www.canada.ca/en/treasury-board-secretariat/services/government-communications/canada-content-style-guide.html)
- [WET-BOEW framework](https://wet-boew.github.io/wet-boew/index-en.html)
- [GCWeb theme](https://wet-boew.github.io/GCWeb/index-en.html)
- [GC Design Library – IRCC (Figma)](https://www.figma.com/community/file/8vPYwBpcscTJfI4Z6qzESX)

---

## Contributing

To add a new skill, create a `.md` file with a YAML front matter block containing `name` and `description` fields, followed by the skill instructions. Follow the conventions of the existing skills for formatting and structure.
