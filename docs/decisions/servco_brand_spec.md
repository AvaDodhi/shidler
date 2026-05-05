# SERVCO — Brand Consistency Technical Specification

> **Brand Presentation System · v1.0 · May 2026**

---

| Field | Value |
|---|---|
| **Spec Title** | Servco Brand Presentation System — Technical Specification |
| **Created By** | Marketing & Communications |
| **Updated By** | Marketing & Communications |
| **Date Created** | May 2026 |
| **Date Updated** | May 2026 |
| **Version** | 1.0 |
| **Role** | Brand Manager / Marketing Operations |
| **Audience** | CMO, Director of Marketing, Internal Comms Teams |
| **Tool Used** | Claude (Anthropic) — Sonnet 4.6 |

---

## Table of Contents

1. [Problem Statement](#1-problem-statement)
2. [Inputs (Known Variables)](#2-inputs-known-variables)
3. [Assumptions & Constraints](#3-assumptions--constraints)
4. [System Flow](#4-system-flow)
5. [Outputs](#5-outputs)
6. [System Review — What Worked & What to Improve](#6-system-review--what-worked--what-to-improve)
7. [Limitations & Next Steps](#7-limitations--next-steps)
8. [Governance Rules](#8-governance-rules)

---

## 1. Problem Statement

Servco is a diversified, community-rooted organization operating across multiple automotive brands and business lines in the Hawaiian and Pacific markets. As Servco grows and its teams expand, presentation materials produced across departments have increasingly diverged in visual quality, tone, and structure — creating inconsistency that undermines brand credibility in executive, partner, and community-facing communications.

This specification documents the analytical and technical framework for a standardized brand presentation system — a PowerPoint template, a structured brand JSON file, and an HTML brand guide — extracted from Servco's existing approved theme file (`Servco_Theme.pptx`). The system enables all teams to produce presentations that consistently reflect Servco's visual identity, professionalism, and values.

**Key parameters of this engagement:**

- **Organization:** Servco Pacific Inc. (diversified automotive and services)
- **Source artifact:** `Servco_Theme.pptx` — approved corporate PowerPoint template
- **Deliverables:** Brand parameter JSON, interactive HTML brand guide, and this specification
- **Objective:** Establish a scalable, reproducible brand system for presentation communications
- **Decision context:** Internal rollout to marketing, executive, and partner-facing teams; foundation for future template governance

---

## 2. Inputs (Known Variables)

All brand parameters were extracted programmatically from `Servco_Theme.pptx` using XML analysis of the slide master, slide layouts, and embedded theme data. The inputs are grouped below by category.

### Color System

| Variable | Hex Value | Role | Usage |
|---|---|---|---|
| `primary_navy` | `#274291` | Primary | Logo, headings, footer lockup, slide number |
| `primary_blue` | `#3155A6` | Primary | Diagonal line motif, decorative elements |
| `accent_light_blue` | `#1C92D1` | Accent | Footer bar, slash icon, wave tones |
| `white` | `#FFFFFF` | Neutral | Text on dark backgrounds, logo on dark slides |
| `black` | `#000000` | Neutral | Body text on light backgrounds |

### Typography

| Variable | Value | Role | Notes |
|---|---|---|---|
| `heading_font` | Montserrat ExtraBold | Headings / Wordmark | All titles, logo wordmark |
| `body_font` | Montserrat Medium | Body copy | All paragraph text |
| `fallback_font` | Arial | Bullet lists | Bullet point fallback only |
| `size_slide_title` | 54pt / 540,000 EMU | Slide Title | Primary slide headline |
| `size_section_header` | 40pt / 400,000 EMU | Section Header | Divider / section intro |
| `size_heading_large` | 36pt / 360,000 EMU | Heading Large | Primary content heading |
| `size_body_default` | 18pt / 180,000 EMU | Body Default | Standard paragraph text |
| `size_slide_number` | 20pt / 200,000 EMU | Slide Number | Top-right, navy color |

### Canvas & Layout

| Variable | Value | Description |
|---|---|---|
| `canvas_width_emu` | 24,387,175 | Slide canvas width in English Metric Units |
| `canvas_height_emu` | 13,716,000 | Slide canvas height in English Metric Units |
| `canvas_width_inches` | 26.67" | Widescreen format — wider than standard 13.33" |
| `canvas_height_inches` | 15.00" | Standard 16:9 height |
| `aspect_ratio` | 16:9 | Standard widescreen orientation |
| `slide_number_x_emu` | 21,862,278 | Horizontal offset of slide number placeholder |
| `slide_number_y_emu` | 619,847 | Vertical offset of slide number placeholder |
| `bg_image_offset_x` | 1,587 EMU | Background master image horizontal offset |

### Visual Motif Variables

| Motif | Color / Value | Description |
|---|---|---|
| `diagonal_line` | `#3155A6`, 30% opacity | Thin diagonal line — signature brand element on all slides |
| `slash_accent_icon (//)` | `#274291` + `#1C92D1` | Double-slash mark at diagonal intersection — cover/section slides |
| `wave_illustration (light)` | `#C5DCF0` | Watermark wave graphic — lower-right on white cover slides |
| `wave_illustration (dark)` | `#3A6DB5` | Watermark wave graphic — lower-right on navy cover slides |
| `footer_bar_left` | `#1C92D1`, ~75% width | Diagonal hatch section of two-part footer — content slides |
| `footer_bar_right` | `#274291`, ~25% width | SERVCO wordmark in white — content slides |
| `horizontal_rule (light)` | `#1C92D1`, thin | Full-width rule above footer zone — white cover slides |
| `horizontal_rule (dark)` | `#FFFFFF`, thin | Full-width rule above footer zone — navy cover slides |

---

## 3. Assumptions & Constraints

The following conventions and constraints govern this specification and all derivative deliverables:

- All measurements expressed in EMU (English Metric Units) unless noted in points (pt) or inches.
- Font size values are stored in half-points in OOXML (e.g., 36pt = 720 in XML `sz` attribute); this spec uses standard point values for readability.
- Color values are expressed in 6-digit hexadecimal (no alpha channel) unless opacity is separately noted.
- The source theme file (`Servco_Theme.pptx`) defines 12 slide layouts; all parameters are extracted from the slide master and layout XML — not from individual slide content.
- The Office Theme accent palette (Accent 1–6: red, green, purple, orange, etc.) is present in the theme XML but is explicitly excluded from brand use in corporate presentations.
- Montserrat is an embedded font in the PPTX; deployments on systems without this font installed must reference the embedded font data or obtain a license from [Google Fonts](https://fonts.google.com/specimen/Montserrat).
- The background master image (`PP_WIDE_TEMP_BLUE_A.ai`) is a proprietary vector asset; it is referenced in the theme but not redistributed in the JSON or HTML deliverables.
- Slide anatomy rules (which motifs appear on which slide types) are inferred from visual analysis of the rendered template slides and cross-referenced with layout XML — they are prescriptive, not merely descriptive.
- No off-template customization is assumed. Variant sub-brand templates (e.g., Toyota, Subaru) may require controlled deviations documented in a separate specification.

---

## 4. System Flow

The brand specification system was built in three sequential phases. Each phase produced a discrete, usable deliverable.

### Phase 1: Source Extraction

- **Input:** `Servco_Theme.pptx` (uploaded source file)
- Unpack PPTX ZIP archive to access raw OOXML (XML) files
- Parse `ppt/theme/theme1.xml` → extract color scheme, font scheme, and format scheme
- Parse `ppt/slideMasters/slideMaster1.xml` → extract layout dimensions, font sizes, bullet hierarchy, and positioning
- Parse all 12 `ppt/slideLayouts/*.xml` → extract per-layout colors and font sizes
- Parse `ppt/presentation.xml` → extract canvas dimensions (EMU)
- Render slides to JPEG via LibreOffice → visual confirmation of motifs and layout anatomy

### Phase 2: Brand JSON

- Organize all extracted parameters into a structured JSON schema
- Group by: brand metadata, canvas spec, color system, typography, slide layouts, visual motifs, slide anatomy, logo rules, slide number spec, and governance
- Encode named variables (e.g., `primary_navy`, `heading_font`, `footer_bar_left`) for use as references in future template builds and AI prompts
- Include usage notes and governance rules inline with each parameter
- **Output:** `servco_brand.json`

### Phase 3: HTML Brand Guide

- Translate brand JSON into a navigable, interactive single-file HTML document
- Apply Servco brand colors and Montserrat typography throughout the guide itself
- Organize into 7 tabbed sections: Colors, Typography, Layouts, Visual Motifs, Slide Anatomy, Canvas, Governance
- Render live color swatches, font size previews, motif illustrations, slide anatomy diagrams, and governance rule cards
- **Output:** `servco_brand_guide.html`

---

## 5. Outputs

| Output | Description | Format | Purpose |
|---|---|---|---|
| `servco_brand.json` | All brand parameters organized by category with usage notes and governance rules | JSON | Machine-readable source of truth; feeds template builds and AI prompts |
| `servco_brand_guide.html` | Interactive 7-tab brand guide with live swatches, font previews, motif illustrations, and anatomy diagrams | HTML (single file) | Human-readable reference for all teams; shareable without a server |
| `servco_brand_spec.md` | Post-build technical specification documenting inputs, flow, outputs, review, and governance | Markdown / DOCX | Audit trail, onboarding reference, and foundation for future template phases |
| Slide Layout Index | 12 named layouts with per-layout color and font size mapping | Embedded in JSON + HTML | Guides template assembly and layout selection |
| Slide Anatomy Diagrams | Visual rules for 3 slide types: cover (light), cover (dark), content | Rendered in HTML | Ensures correct motif placement per slide type |
| Governance Rules | Required elements, color rules, typography rules, and do-not list | Embedded in JSON + HTML + this doc | Enforcement layer for adoption and quality control |

---

## 6. System Review — What Worked & What to Improve

### What Worked Well

- **Programmatic extraction from PPTX XML was highly reliable.** Color hex values, font names, EMU dimensions, and layout names were pulled directly from source data — no manual interpretation required for these fields.
- **The JSON schema structure proved immediately useful:** grouping by canvas, colors, typography, motifs, and anatomy made the data easy to navigate and reference.
- **The HTML brand guide rendered Servco's actual brand accurately** using the extracted parameters — Montserrat fonts, navy/blue palette, and the two-tone footer bar all appeared as designed.
- **Visual slide rendering (JPEG via LibreOffice) was essential** for identifying motifs that don't exist in the XML directly, such as the diagonal hatch pattern in the footer bar and the wave illustration style.
- **The three-phase build sequence** (extract → JSON → HTML) created clear, auditable handoffs between steps.

### What to Improve

- The body text hierarchy font sizes in the JSON are stored as EMU-scale values from the XML `sz` attribute, not standard points. Future versions should normalize these to `pt` values for readability and usability.
- The 12 slide layout names are non-descriptive (e.g., `4_Custom Layout`, `5_Custom Layout`). A future pass should rename these with functional labels (e.g., `Data Chart Slide`, `Two-Column Content`) based on visual inspection.
- The background master image (`PP_WIDE_TEMP_BLUE_A.ai`) is referenced but not embedded in the JSON or HTML. A future version should include an SVG rendering of the motif for use in non-PPTX environments.
- The HTML brand guide does not currently include a downloadable JSON panel or copy-to-clipboard functionality for hex values and variable names. Adding these would improve usability for developers and template builders.
- Adoption risk is real: without training or a designated template gatekeeper, teams may revert to custom formatting. A one-page quick reference card should accompany the full guide for everyday use.

### What Would Make This More Auditable

- Version-control the JSON file (e.g., in this Git repository) so changes to brand parameters are tracked over time.
- Add a `changelog` section to both the JSON and HTML files so updates are dated and described.
- Link each parameter in the JSON back to its source XML path (e.g., `source: ppt/theme/theme1.xml > a:clrScheme > a:dk2`) for full traceability.

---

## 7. Limitations & Next Steps

### Limitations

- This specification does not incorporate sub-brand variants for Servco's automotive brand lines (Toyota, Subaru, etc.), which may require controlled deviations from the corporate palette.
- The system does not yet include slide content templates (body copy, chart placeholders, image zones) — only visual identity parameters have been formalized.
- Multi-channel applications (email signatures, social media templates, print collateral) are outside the scope of this specification.
- The HTML brand guide is a static reference document; it is not connected to a live design system or token management platform.
- Adoption cannot be enforced through this system alone — governance depends on team training and leadership support.

### Next Steps

| Phase | Action |
|---|---|
| **Phase 2** | Build a modular PowerPoint template using the brand JSON as the specification input — including all 8 slide types from the memo (title, agenda, section divider, data charts, timelines, case studies, team/org, summary/CTA) |
| **Phase 3** | Produce a one-page Brand Quick Reference card for distribution to all presentation authors |
| **Phase 4** | Pilot the template with a real executive deck, collect feedback, and release Version 1.0 for company-wide rollout |
| **Phase 5** | Evaluate sub-brand variant needs and document controlled flexibility rules for automotive brand presentations |
| **Phase 6** | Explore integration with a design token platform (e.g., Style Dictionary) to keep the brand JSON synchronized with digital design tools |

---

## 8. Governance Rules

The following rules are binding for all presentations produced under the Servco corporate brand. They are encoded in `servco_brand.json` and displayed in `servco_brand_guide.html`.

### ✅ Required Elements (Every Slide)

- SERVCO wordmark must appear on every slide
- Diagonal blue line motif (`#3155A6`) is a core brand signature — do not remove
- Wave illustration only on cover and section divider slides — never on content slides
- Two-tone footer bar (light blue left + navy right) required on all content slides
- Slide numbers top-right in navy (`#274291`) on all content slides

### 🎨 Color Rules

- Primary navy (`#274291`) is the dominant color — use for logo, headings, and key UI elements
- Light blue (`#1C92D1`) is the accent — use sparingly for highlights, bars, and icons
- Do not use Office Theme accent colors (red, green, purple, orange) in brand presentations
- White text only on navy or blue backgrounds

### 🔤 Typography Rules

- Montserrat ExtraBold for all headings and the SERVCO wordmark
- Montserrat Medium for all body copy
- Do not introduce other typefaces — Arial is permitted for bullet list fallback only
- Titles left-aligned on content slides; centered on cover slides

### 🚫 Do Not

- Do not add decorative elements that compete with the diagonal line motif
- Do not use accent colors (red, green, orange) in any corporate presentation
- Do not place the logo in the body content area of any slide
- Do not use the wave graphic on data or content slides

---

*Servco Brand Presentation System — Technical Specification v1.0 — May 2026 — Internal Use Only*
