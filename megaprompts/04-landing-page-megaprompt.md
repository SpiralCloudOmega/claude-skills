# Mega Prompt: Landing Page Generator Skill

## Role

You are a **Skill Architect** specializing in frontend generation workflows. Generate a production-grade, distributable Claude skill that produces premium single-file HTML landing pages with 3D CSS animations, scroll-triggered effects, and mouse-parallax depth.

## Output Target

Single file: `${SKILLS_DIR}/landing-page/SKILL.md`

Word budget: 2,000–2,400 words. Hard ceiling: 2,500.

## Skill Purpose

Generate a polished, self-contained `.html` landing page from a text prompt or brief. The output is one HTML file: all CSS inline in `<style>`, all JS inline in `<script>`, only external dependencies being Google Fonts + GSAP via CDN. The page is visually distinctive, animated, and production-quality.

## Required Capabilities

The skill must specify how to:

1. **Extract content from input** — Product name, hero headline, subtext, features, CTA text, closing copy.
1. **Apply a configurable brand system** — Default to a polished dark theme, but accept brand overrides (colors, fonts, accent).
1. **Build three required sections** — Hero, Features, Closing CTA.
1. **Apply animations** — GSAP entrance, ScrollTrigger reveals, mouse parallax, CSS floating shapes.
1. **Output a single self-contained HTML file** — Configurable path, kebab-case filename.

## Workflow Structure

The generated skill must follow this structure:

```
1. Content extraction (with fallback strategy)
2. Brand system selection (default + override path)
3. Section 1: Hero (structure + depth layers + animations)
4. Section 2: Features (structure + card spec + reveal animation)
5. Section 3: Closing CTA (structure + ambient glow)
6. Brand system reference (colors, typography, components)
7. Required CDN dependencies
8. Animation patterns (entrance, parallax, scroll-triggered, floating)
9. Layout rules (responsive grid, viewport behavior)
10. Output spec (path, naming, file format)
```

## Critical Improvements Over Naive Implementation

The skill MUST address these production concerns:

1. **Configurable color system** — Don’t hardcode one brand palette. Provide a default (dark navy + teal accent) AND document override syntax for users to swap in their brand colors via CSS custom properties.
1. **Configurable output path** — Use `${OUTPUT_DIR}` variable, default to `./landing-pages/`. No hardcoded absolute paths.
1. **Content fallback strategy** — When input is sparse, document how to invent compelling content from context rather than stalling.
1. **Responsive by default** — Document breakpoints: 900px (tablet → 2-col), 580px (mobile → 1-col).
1. **Accessibility minimum** — Document: alt text on icons via aria-label, semantic HTML5 (header, section, footer), keyboard-navigable CTA buttons.
1. **No FOUC** — Mandate `gsap.set()` to hide elements BEFORE entrance animations.

## Brand System Specification (Must Be Fully Documented)

### Default Color Palette (Dark Navy + Teal)

```css
--navy:       #0A1628;
--navy-mid:   #0D1F38;
--teal:       #00D4AA;
--teal-glow:  rgba(0, 212, 170, 0.12);
--amber:      #F5A623;
--off-white:  #F7F7F2;
--text-muted: rgba(247, 247, 242, 0.68);
--card-bg:    rgba(0, 212, 170, 0.06);
--card-border:rgba(0, 212, 170, 0.15);
```

### Override Pattern (Must Document)

The skill must explain: users can override by passing a custom palette object. Example:

```
Brand override:
- primary: #FF6B35
- accent:  #2EC4B6
- bg:      #011627
- text:    #FDFFFC
```

### Typography

- Font family: Inter (via Google Fonts)
- Weight scale: 400, 500, 600, 700, 800
- Size scale documented per use (Hero H1, Section H2, card titles, body, eyebrow, CTA)

### Components (Must Specify CSS)

- `.btn-primary` — CTA button with hover state
- `.feature-card` — Card with hover lift
- `.eyebrow` — Letter-spaced category label

## Section Specifications

### Section 1: Hero

- `100vh`, centered content
- Optional eyebrow label
- H1 (68–82px, 800 weight)
- Subtitle (1–2 sentences)
- CTA button
- Scroll-down indicator (animated chevron)
- **Depth layers**: `.hero-shapes-back` and `.hero-shapes-mid` with absolute-positioned decorative shapes

### Section 2: Features

- 3 columns default (2-col if exactly 4 features, 1-col on mobile)
- Each card: SVG icon (28px, accent stroke) → title → description
- Hover state: lift + border brighten

### Section 3: Closing CTA

- Full-width, dark background
- Large closing headline (52–62px, 800 weight)
- Short subtext
- CTA button with ambient radial-gradient glow behind it

## Animation Patterns (Must Be Fully Specified)

The skill must include these patterns as concrete code blocks:

### 1. Hero Entrance (GSAP timeline)

- `gsap.set()` to hide everything first (prevents FOUC)
- Staggered timeline with overlap timings

### 2. Mouse Parallax

- Mousemove listener on hero
- Two depth layers move at different speeds (back: ±45/22, mid: ±22/11)
- Content layer moves subtly in same direction (±8/5)

### 3. Scroll-Triggered Feature Cards

- Initial state: `opacity: 0, y: 55, rotateX: 18`
- ScrollTrigger reveal with `power2.out` ease
- Stagger 0.11s

### 4. Floating Decorative Shapes (CSS keyframes, not GSAP)

- `floatA`, `floatB`, `floatC` with varied durations and rotation
- Use CSS for ambient motion (smoother, cheaper than GSAP)

### 5. Scroll Indicator (CSS bounce)

## Required CDN Dependencies

Skill must specify exactly these (no exceptions):

```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollTrigger.min.js"></script>
```

## Output Spec

- Path: `${OUTPUT_DIR}/<product-name-kebab>-landing.html`
- Default `${OUTPUT_DIR}`: `./landing-pages/`
- Filename: lowercase kebab-case from product name (“Quill AI” → `quill-ai-landing.html`)
- Self-contained: all CSS in `<style>`, all JS in `<script>`, only Google Fonts + GSAP CDN external

## Trigger Phrases (for frontmatter description)

- “create a landing page”
- “build a landing page”
- “make a landing page for X”
- “I need a web page for Y”
- “promotional page”
- “product page”
- “one-pager”
- “web presence”
- “sales page”

## Error Handling Requirements

|Situation                                      |Behavior                                                                     |
|-----------------------------------------------|-----------------------------------------------------------------------------|
|Input is just a name with no context           |Invent compelling content from name semantics; flag as inferred              |
|Input file is large or PDF                     |Read fully before generating; don’t truncate                                 |
|Brand colors are insufficient (only 1 provided)|Use that as primary; derive secondary/accent algorithmically (lighten/darken)|
|Features count not specified                   |Default to 4                                                                 |
|Output dir doesn’t exist                       |Create it                                                                    |
|Existing file at output path                   |Append timestamp suffix or ask user                                          |

## Portability Requirements

- **Claude Code CLI**: Native — writes HTML file directly to filesystem.
- **Claude.ai web**: Native — produces HTML as an artifact instead of file.

The skill must document both delivery modes:

> **Delivery mode**: In Claude Code CLI, write the file to disk at the specified path. In Claude.ai web, create an HTML artifact with the same content.

## Frontmatter Spec

```yaml
---
name: landing-page
description: "Generates a premium single-page HTML landing page with 3D CSS animations, GSAP scroll effects, and mouse-parallax depth. Use whenever the user says 'create a landing page', 'build a landing page', 'make a landing page for X', 'I need a web page for Y', or provides product/service details and wants a polished website. Also triggers on 'promotional page', 'product page', 'one-pager', 'web presence', 'sales page'. Outputs a single self-contained HTML file (Claude Code) or HTML artifact (Claude.ai). Supports configurable brand colors via CSS custom property overrides."
---
```

## Anti-Patterns To Reject

- Hardcoded absolute paths in output directory
- Single brand palette without override documentation
- Outlining before writing — write in one pass
- External CSS or JS files (must be inline)
- Skipping `gsap.set()` initial states (causes FOUC)
- More than 6 features in default grid (becomes unscannable)
- Brand-specific content references in the skill itself

## Validation Checklist (Run Before Delivery)

- [ ] Frontmatter parses as YAML
- [ ] Word count 2,000–2,500
- [ ] Default color palette documented as CSS custom properties
- [ ] Override pattern documented
- [ ] All 3 sections fully specified
- [ ] All 5 animation patterns included with code
- [ ] CDN dependencies listed
- [ ] Output path uses variable, not hardcoded absolute path
- [ ] Responsive breakpoints documented
- [ ] Both CLI and web delivery modes documented
- [ ] No FOUC instruction explicit
