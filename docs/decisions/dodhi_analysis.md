# Stage 4 — Final Analysis, Prompt Engineering & Recommendation
## Servco Brand Consistency & Presentation System

> **Author:** Marketing & Communications
> **Role:** Brand Manager / Marketing Operations
> **Audience:** CMO, Director of Marketing, Internal Comms Teams
> **Date:** May 2026 | **Version:** 1.0
> **Tool Used:** Claude (Anthropic) — Sonnet 4.6

---

## Table of Contents

- [A. Project & Data Summary](#a-project--data-summary)
- [B. Brand Audit Results Summary](#b-brand-audit-results-summary)
- [C. Interpretation & Key Findings](#c-interpretation--key-findings)
- [D. Brand Consistency Decomposition](#d-brand-consistency-decomposition)
- [E. Strategic Recommendations](#e-strategic-recommendations)
- [F. Structured AI Prompt](#f-structured-ai-prompt)
- [G. Executive Justification](#g-executive-justification)

---

## A. Project & Data Summary

**Organization:** Servco Pacific Inc. — diversified automotive and services company operating across Hawaii and the Pacific region, representing brands including Toyota, Subaru, Lexus, and Chevrolet.

**Project Scope:** This analysis covers Servco's corporate brand presentation system, built from the approved theme file `Servco_Theme.pptx` during May 2026. The objective was to audit the existing brand template, extract all design parameters, and produce a scalable, reproducible brand system for use across executive, partner, and internal-facing communications.

**Data Sources:**

| Source | Description |
|---|---|
| `Servco_Theme.pptx` | Approved corporate PowerPoint master template (primary source) |
| PPTX slide master XML | `ppt/slideMasters/slideMaster1.xml` — layout, fonts, sizing |
| PPTX theme XML | `ppt/theme/theme1.xml` — color scheme, font scheme |
| PPTX layout XML | `ppt/slideLayouts/*.xml` — 12 layout-specific parameters |
| PPTX presentation XML | `ppt/presentation.xml` — canvas dimensions |
| Visual slide renders | JPEG exports via LibreOffice — motif and anatomy confirmation |
| Brand memo | Internal memo: *Why Brand Consistency Matters at Servco* |

**Key Assumptions:**

- All parameters are extracted from the corporate master template; sub-brand variants (Toyota, Subaru, etc.) are out of scope for v1.0.
- The Office Theme accent palette (red, green, purple, orange) is present in the theme XML but excluded from brand use per governance rules.
- `Montserrat` font licensing is assumed to be resolved via Google Fonts or the embedded PPTX font data.
- No multi-channel extensions (email, print, social) are included in this phase.

---

## B. Brand Audit Results Summary

All parameters below were extracted programmatically from the source PPTX and validated against visual slide renders.

### Identity Parameters

| Category | Key Parameters | Status |
|---|---|---|
| **Color System** | 3 core brand colors extracted: `#274291`, `#3155A6`, `#1C92D1` | ✅ Clearly defined |
| **Typography** | 2 brand fonts: Montserrat ExtraBold (headings), Montserrat Medium (body) | ✅ Consistent |
| **Canvas Spec** | 16:9, 26.67" × 15.00", custom widescreen format | ✅ Non-standard — documented |
| **Visual Motifs** | 5 signature elements: diagonal line, `//` slash icon, wave graphic, footer bar, horizontal rule | ✅ All captured |
| **Slide Layouts** | 12 layouts across 3 slide types: cover (light), cover (dark), content | ⚠️ 4 layouts unnamed/non-descriptive |
| **Governance Rules** | 4 rule categories: required elements, color rules, typography rules, do-nots | ✅ Documented and encoded |

### Deliverable Completeness

| Deliverable | Status | Notes |
|---|---|---|
| `servco_brand.json` | ✅ Complete | 9 parameter groups, named variables, governance encoded |
| `servco_brand_guide.html` | ✅ Complete | 7 tabbed sections, live swatches, motif previews, anatomy diagrams |
| `servco_brand_spec.md` | ✅ Complete | 8-section technical specification, GitHub-ready |
| Slide anatomy rules | ✅ Complete | 3 slide types documented with motif placement rules |
| Sub-brand variants | ❌ Not started | Deferred to Phase 5 |
| Content templates | ❌ Not started | Deferred to Phase 2 |

---

## C. Interpretation & Key Findings

### 1. The Brand Has a Strong Visual Identity — But It Lives Only in One File

Servco's existing `Servco_Theme.pptx` contains a well-designed, coherent visual system. The color palette is tightly controlled (three core colors, clearly differentiated by role), the typography is consistent (Montserrat family throughout), and the signature motifs — the diagonal line, the `//` icon, and the wave graphic — are distinctive and professionally executed.

**The problem:** all of this knowledge was locked inside a single binary file. No human-readable documentation existed. Any team member who opened a blank presentation had no guidance on which layout to use, which colors to apply, or which motifs belonged on which slide type. The brand existed, but it wasn't *accessible*.

### 2. Slide Layout Naming Is a Governance Risk

Of the 12 slide layouts, four use non-descriptive internal names (`4_Custom Layout`, `5_Custom Layout`, etc.). This means a team member assembling a presentation cannot tell from the layout picker which template serves which purpose. Without clear names, teams default to whichever layout looks closest — leading to inconsistency and misuse of brand motifs.

**Benchmark:** Best-practice brand systems (e.g., Google's Material Design, Salesforce Lightning) label every component with a clear functional name and a usage note. Servco's layout naming is currently below this standard.

### 3. The Footer Bar Is the Most At-Risk Brand Element

The two-tone footer bar — light blue (`#1C92D1`) on the left with a diagonal hatch pattern, and navy (`#274291`) on the right with the SERVCO wordmark — is a high-impact brand element that appears on every content slide. However, it is also the element most likely to be accidentally deleted or overwritten in custom presentations, because it lives in the slide layout rather than the master.

This is a significant governance concern: losing the footer bar is the fastest way a presentation stops looking like Servco.

### 4. The Widescreen Canvas Is Non-Standard and Undocumented

Servco's template uses a custom canvas size of 26.67" × 15.00" — significantly wider than the PowerPoint default widescreen of 13.33" × 7.5". This means that any new presentation created from a standard PowerPoint template and then re-themed will have sizing mismatches for all placed images, shapes, and text boxes.

Prior to this project, this parameter was undocumented. Teams building new templates would have had no way to know the correct canvas dimensions without opening the source file and checking manually.

### 5. The Three-Phase Build Created a Durable, Reusable System

The extraction → JSON → HTML pipeline produced three artifacts that reinforce each other: the JSON is the source of truth, the HTML is the human interface, and this specification is the audit trail. Any future team member — or AI model — can regenerate the brand system from these files without access to the original PPTX.

**This is the core value of the project:** brand parameters that previously existed only in a binary file now exist in open, readable, version-controllable formats.

---

## D. Brand Consistency Decomposition

Just as a Du Pont analysis decomposes ROE into its drivers, brand consistency can be decomposed into three contributing factors: **identity clarity**, **system usability**, and **adoption infrastructure**. Weakness in any one factor undermines the others.

```
Brand Consistency Score
        │
        ├── Identity Clarity
        │       How well-defined are the brand parameters?
        │       (Colors, fonts, motifs, canvas, rules)
        │       Servco Score: HIGH ✅
        │       → 3 core colors, 2 fonts, 5 motifs, all documented
        │
        ├── System Usability
        │       How easy is it for a team member to apply the brand correctly?
        │       (Named layouts, clear labels, accessible reference)
        │       Servco Score: MEDIUM ⚠️
        │       → HTML guide built; layout names still non-descriptive;
        │         no copy-to-clipboard or downloadable JSON in guide yet
        │
        └── Adoption Infrastructure
                How likely is the brand to be applied consistently without oversight?
                (Training, governance gatekeeper, quick reference card)
                Servco Score: LOW ⚠️
                → Governance rules documented but no rollout plan,
                  no gatekeeper assigned, no quick reference card yet
```

**Key Insight:** Servco's brand consistency risk is not in the quality of the identity — the design is strong. The risk is in the gap between having a well-documented system and having teams actually use it. The project has moved the needle significantly on Identity Clarity, partially addressed System Usability, and identified Adoption Infrastructure as the critical next investment.

---

## E. Strategic Recommendations

### Recommendation 1: Rename All 12 Slide Layouts with Functional Labels

**Finding:** Four of Servco's 12 slide layouts have non-descriptive names (`4_Custom Layout`, `5_Custom Layout`, etc.), making them invisible to everyday users.

**Action:** Update layout names in the master PPTX and the brand JSON to functional labels:

| Current Name | Recommended Name |
|---|---|
| `Vertical Title and Text` | `Cover Slide — Light` |
| `1_Vertical Title and Text` | `Cover Slide — Dark` |
| `Basic Slide` | `Content Slide — Standard` |
| `Photo and Bullets` | `Content Slide — Image Left` |
| `Photo & Text` | `Content Slide — Image Right` |
| `Paragraphy` | `Content Slide — Text Heavy` |
| `4_Custom Layout` | `Section Divider` |
| `5_Custom Layout` | `Data & Charts` |

**Impact:** Reduces layout misuse and speeds up presentation assembly for all teams.

---

### Recommendation 2: Add Copy-to-Clipboard and Downloadable JSON to the HTML Brand Guide

**Finding:** The `servco_brand_guide.html` currently displays hex values and variable names as static text. Developers and template builders building new tools off the brand system must manually transcribe values.

**Action:** Add two features to the HTML guide:
1. A "Copy" button next to every hex value and variable name
2. A "Download JSON" button in the header that exports `servco_brand.json`

**Impact:** Reduces transcription errors and makes the brand guide a functional tool rather than just a reference document. Estimated implementation: 2–4 hours of front-end work.

---

### Recommendation 3: Produce a One-Page Brand Quick Reference Card

**Finding:** The full brand guide and specification are comprehensive but too long for everyday use. Most team members building a presentation need answers to three questions: *What colors do I use? What fonts? What goes in the footer?*

**Action:** Produce a single-page PDF quick reference card containing:
- The 3 core color swatches with hex values
- The 2 brand fonts with size scale
- The 3 slide type diagrams (cover light, cover dark, content)
- The top 5 governance rules

**Impact:** This is the highest-leverage adoption tool. A quick reference card reduces the activation energy required to follow brand standards. Distribute at team onboarding and pin to the internal wiki.

---

### Recommendation 4: Assign a Brand Template Gatekeeper and Version-Control the JSON

**Finding:** The brand system is now documented, but documentation without enforcement has limited value. The internal memo cited adoption as the primary risk — teams may revert to custom formatting without accountability.

**Action:**
1. Designate one person in Marketing Operations as the brand template gatekeeper, responsible for approving significant presentation deviations and maintaining the JSON file.
2. Move `servco_brand.json` into a version-controlled GitHub repository (already initiated with this specification).
3. Add a `changelog` block to the JSON file so every parameter update is dated and described.

**Impact:** Converts the brand system from a one-time deliverable into a living, governed asset. This is the infrastructure that makes brand consistency sustainable at scale.

---

## F. Structured AI Prompt

The following prompt is designed to allow any AI model (or future team member) to regenerate the complete Servco brand system from scratch — including the JSON parameter file and the HTML brand guide — using only this document as input.

---

```
# GOAL

You are a brand systems engineer. Using the Servco brand parameters provided below,
produce two files:

1. `servco_brand.json` — A structured JSON file containing all brand parameters
   organized by: brand metadata, canvas spec, color system, typography, slide layouts,
   visual motifs, slide anatomy, logo rules, slide number spec, and governance rules.

2. `servco_brand_guide.html` — A single-file interactive HTML brand guide with tabbed
   navigation covering: Colors, Typography, Layouts, Visual Motifs, Slide Anatomy,
   Canvas, and Governance. Apply Servco's actual brand colors and Montserrat font
   throughout the guide itself.


# BRAND IDENTITY

brand_name: SERVCO
theme_name: SERVCO_CORP_PRES_WIDE
version: 1.0
organization: Servco Pacific Inc.
industry: Diversified automotive and services
markets: Hawaii and Pacific region


# COLOR SYSTEM

primary_navy:       #274291   — Logo, headings, footer lockup, slide number
primary_blue:       #3155A6   — Diagonal line motif, decorative elements
accent_light_blue:  #1C92D1   — Footer bar, slash icon, wave tones, body accents
white:              #FFFFFF   — Text on dark backgrounds, logo on dark slides
black:              #000000   — Body text on light backgrounds

Office Theme palette (reference only — do NOT use in brand presentations):
  accent1: #4F81BD  accent2: #C0504D  accent3: #9BBB59
  accent4: #8064A2  accent5: #4BACC6  accent6: #F79646


# TYPOGRAPHY

heading_font:          Montserrat ExtraBold
body_font:             Montserrat Medium
fallback_font:         Arial (bullet lists only)
monospace_font:        Courier New

Font size scale (in points):
  size_slide_title:      54pt   (540,000 EMU)
  size_section_header:   40pt   (400,000 EMU)
  size_heading_large:    36pt   (360,000 EMU)
  size_heading_medium:   32pt   (320,000 EMU)
  size_heading_small:    30pt   (300,000 EMU)
  size_body_large:       28pt   (280,000 EMU)
  size_body_default:     18pt   (180,000 EMU)
  size_slide_number:     20pt   (200,000 EMU)
  size_caption:           8pt    (80,000 EMU)

Body text bullet hierarchy:
  Level 1: bullet •   82pt EMU   indent 879,298 EMU
  Level 2: bullet –   72pt EMU   indent 1,905,147 EMU
  Level 3: bullet •   62pt EMU   indent 2,930,995 EMU
  Level 4: bullet –   51pt EMU   indent 4,103,393 EMU
  Level 5: bullet »   51pt EMU   indent 5,275,791 EMU

Spacing:
  body_space_before_pct: 20
  kern_pt: 12


# CANVAS SPEC

canvas_width_emu:       24,387,175
canvas_height_emu:      13,716,000
canvas_width_inches:    26.67"
canvas_height_inches:   15.00"
aspect_ratio:           16:9
orientation:            landscape

slide_number_x_emu:     21,862,278
slide_number_y_emu:       619,847
bg_image_offset_x_emu:       1,587
bg_image_offset_y_emu:           0


# VISUAL MOTIFS

diagonal_line:
  color: #3155A6
  opacity: 30%
  description: Thin diagonal line running upper-right to lower-center
  applies_to: all slides

slash_accent_icon:
  colors: #274291 (primary slash) + #1C92D1 (secondary slash)
  symbol: //
  description: Two-tone double-slash at diagonal intersection
  applies_to: cover slides, section dividers

wave_illustration:
  color_light_version: #C5DCF0
  color_dark_version: #3A6DB5
  description: Organic flowing wave lines, lower-right quadrant, watermark style
  applies_to: cover slides, section dividers

footer_bar:
  left_section_color: #1C92D1
  left_section_width: ~75%
  left_section_content: diagonal hatch/stripe pattern
  right_section_color: #274291
  right_section_width: ~25%
  right_section_content: SERVCO wordmark in white
  applies_to: content slides

horizontal_rule:
  color_light_version: #1C92D1
  color_dark_version: #FFFFFF
  weight: thin (1px)
  description: Full-width rule separating content area from footer zone
  applies_to: cover slides

background_master_image:
  source_file: PP_WIDE_TEMP_BLUE_A.ai
  offset_x_emu: 1,587
  offset_y_emu: 0
  description: Full-bleed vector containing diagonal line and wave motifs


# SLIDE LAYOUTS (12 total)

Layout 1:  "Cover Slide — Light"         background: white   motifs: diagonal, slash, wave, rule
Layout 2:  "Cover Slide — Light Alt"     background: white   motifs: diagonal, slash, wave, rule
Layout 3:  "Cover Slide — Minimal"       background: white   motifs: none
Layout 4:  "Cover Slide — Dark"          background: #274291 motifs: diagonal, slash, wave, rule, bottom band (#1C92D1)
Layout 5:  "Content Slide — Standard"    background: white   motifs: footer bar, slide number
Layout 6:  "Content Slide — Image Left"  background: white   motifs: footer bar, slide number
Layout 7:  "Content Slide — Image Right" background: white   motifs: footer bar, slide number
Layout 8:  "Content Slide — Text Heavy"  background: white   motifs: footer bar, slide number
Layout 9:  "Blank Slide"                 background: white   motifs: none
Layout 10: "Section Divider"             background: white   motifs: footer bar, slide number
Layout 11: "Data & Charts"               background: white   motifs: footer bar, slide number
Layout 12: "Closing / End Card"          background: #274291 motifs: none


# SLIDE ANATOMY RULES

cover_slide_light:
  background: white
  logo: top-left, color (#274291)
  diagonal_line: yes
  slash_icon: yes
  wave_graphic: yes
  footer_bar: no
  horizontal_rule: yes (#1C92D1)

cover_slide_dark:
  background: #274291
  logo: lower-left, white
  diagonal_line: yes
  slash_icon: yes
  wave_graphic: yes (dark version #3A6DB5)
  footer_bar: no
  horizontal_rule: yes (white)
  bottom_band: #1C92D1

content_slide:
  background: white
  logo: footer-right, white on navy
  diagonal_line: no
  slash_icon: no
  wave_graphic: no
  footer_bar: yes
  slide_number: top-right, #274291, 20pt


# LOGO RULES

wordmark: SERVCO
font: Montserrat ExtraBold
color_on_light: #274291
color_on_dark: #FFFFFF
placement_cover_light: top-left (~5% from left, ~12% from top)
placement_cover_dark: lower-left (~5% from left, ~65% from top)
placement_content: footer-right lockup (~right 25% of footer bar)


# GOVERNANCE RULES

required_on_every_slide:
  - SERVCO wordmark must appear on every slide
  - Diagonal blue line motif (#3155A6) — do not remove
  - Wave illustration only on cover/section slides — never on content slides
  - Two-tone footer bar required on all content slides
  - Slide numbers top-right in navy (#274291) on content slides

color_rules:
  - Primary navy (#274291) is dominant — logo, headings, key UI elements
  - Light blue (#1C92D1) is accent — use sparingly for highlights, bars, icons
  - Do NOT use Office Theme accent colors in corporate presentations
  - White text only on navy or blue backgrounds

typography_rules:
  - Montserrat ExtraBold for all headings and the wordmark
  - Montserrat Medium for all body copy
  - Do not introduce other typefaces — Arial for bullet fallback only
  - Titles left-aligned on content slides; centered on cover slides

do_not:
  - Do not add elements competing with the diagonal line motif
  - Do not use accent colors (red, green, orange) in corporate presentations
  - Do not place the logo in the body content area
  - Do not use the wave graphic on content or data slides


# OUTPUT REQUIREMENTS

For servco_brand.json:
  - Use camelCase keys
  - Group all parameters by the section headers above
  - Include "usage" and "applies_to" notes on all color and motif entries
  - Include a "governance" section with all four rule categories
  - Include a top-level "meta" block with: brand name, version, date, source file

For servco_brand_guide.html:
  - Single self-contained file (no external CSS or JS files)
  - Load Montserrat from Google Fonts CDN
  - Apply #274291 as the primary UI color, #1C92D1 as accent
  - Tab navigation: Colors | Typography | Layouts | Visual Motifs | Slide Anatomy | Canvas | Governance
  - Colors tab: render live color swatches with hex values, names, and usage notes
  - Typography tab: font demos, size scale table with pt and EMU values, bullet hierarchy
  - Layouts tab: card grid of all 12 layouts with names, background color, and motif indicators
  - Visual Motifs tab: rendered CSS previews of each motif (diagonal line, slash icon, wave, footer bar, horizontal rule)
  - Slide Anatomy tab: side-by-side diagrams of the 3 slide types showing element placement
  - Canvas tab: key-value grid of all canvas and positioning parameters
  - Governance tab: 4 color-coded rule cards (required, colors, typography, do not)
```

---

## G. Executive Justification

**To:** CMO / Director of Marketing
**From:** Marketing Operations
**Re:** Servco Brand Presentation System — Strategic Value Summary

### Brand Health Assessment

Servco's visual identity is strong. The corporate template contains a distinctive, professional design system — a controlled color palette, consistent typography, and signature motifs that are immediately recognizable. The challenge has never been the quality of the brand; it has been accessibility. Before this project, all of that design knowledge existed only inside a binary PowerPoint file that most team members treated as a starting point rather than a standard.

This project converts that implicit knowledge into an explicit, open, and maintainable system.

### Operational Efficiency

Every hour a team member spends recreating a footer bar, selecting the wrong font, or choosing an off-brand color is an hour of unnecessary rework. At Servco's scale — multiple business lines, multiple audiences, multiple presentation authors — that rework compounds quickly. The brand JSON and HTML guide eliminate the ambiguity that causes it. A team member assembling a deck now has a single authoritative reference for every parameter, accessible without opening a PowerPoint file.

### Governance and Risk Reduction

Inconsistent presentations carry a reputational cost that is easy to underestimate. When a partner deck uses the wrong blue, when an executive presentation omits the footer bar, when a community presentation mixes fonts — each instance chips away at the credibility signal the brand is designed to send. The governance rules documented in this system create a clear, defensible standard. When deviations occur, there is now a written baseline to reference.

### Capital Structure of Brand Assets

The three deliverables produced in this project — the JSON, the HTML guide, and this specification — represent a different kind of asset than the original PPTX. The PPTX is a presentation file. These deliverables are *infrastructure*: they are version-controllable, shareable, machine-readable, and extensible. A future developer building a new template, a new AI tool, or a new sub-brand variant can build directly from the JSON without reverse-engineering the PowerPoint.

### Value Creation Track Record

The immediate deliverables of this project are:
- One machine-readable brand parameter file (`servco_brand.json`)
- One interactive HTML brand reference (`servco_brand_guide.html`)
- One technical specification and audit trail (`servco_brand_spec.md`)
- One structured AI prompt capable of regenerating the entire system

The longer-term value creation begins in Phase 2: a modular slide library built to these exact specifications, piloted with a real executive deck, and rolled out as the company-wide standard. The work done here is the foundation that makes that rollout reliable rather than arbitrary.

### Recommended Next Action

Approve Phase 2 scope: build the modular PowerPoint template (8 slide types) using `servco_brand.json` as the specification input. Assign a brand template gatekeeper. Schedule a pilot with one internal team before company-wide rollout.

---

*Servco Brand Presentation System — Stage 4 Final Analysis · v1.0 · May 2026 · Internal Use Only*
