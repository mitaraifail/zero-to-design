# [Product Name] Design System

> This document is the single source of visual and interaction truth for AI agents generating UI. All pages, components, styles, and interactions must strictly follow the tokens and rules in this document.
> Produced by the zero-to-design workflow: Phase 4 first screen(s) → DESIGN.draft.md → Phase 5 motion review / Phase 6 multi-screen iteration → Phase 7 finalization.

## 1. Design Soul (Visual Theme & Atmosphere)

**Brand in one sentence**: [e.g.: a warm, trustworthy indie-creator marketplace]

**Overall temperament**: [e.g.: like an indie bookstore tucked inside a market — handmade warmth with professional quality]

**Keywords**: [3-5 adjectives, e.g.: warm, handmade, trustworthy, clean, breathing room]

**Color strategy**: [one paragraph on the color philosophy, e.g.: backgrounds always lean warm; the accent is a garnish only, never more than 10% of any area]

**Typography-role philosophy**: [one paragraph, e.g.: headlines use a serif to convey warmth; body uses a sans-serif for readability]

**Reference brands**: [2-3 brands with a similar temperament]

---

## 2. Tokens (Base Rules)

### Color Palette & Roles

| Token | Hex | Role | Used for | Forbidden for |
|-------|-----|------|----------|----------------|
| `--color-bg` | `#...` | Page background | Main background | Large high-saturation fills |
| `--color-surface` | `#...` | Card/panel background | Product cards, info panels | - |
| `--color-text-primary` | `#...` | Primary text | Headlines, body | Background color |
| `--color-text-secondary` | `#...` | Secondary text | Captions, labels | Headlines |
| `--color-accent` | `#...` | Accent | CTA buttons, links, highlights | Large background fills |
| `--color-border` | `#...` | Border | Card borders, dividers | Text color |
| `--color-success` | `#...` | Success state | Success messages | Large backgrounds |
| `--color-error` | `#...` | Error state | Error messages | Large backgrounds |

**Color principles**:
- [e.g.: never use pure white #FFFFFF as a background]
- [e.g.: the accent is a garnish only, never more than 10% of any area]

### Typography Rules

| Tier | Font | Substitute | Weight | Size | Line-height | Letter-spacing | Used for |
|------|------|-----------|--------|------|-------------|----------------|----------|
| Display | [font name] | [fallback] | [weight] | [px] | [line-height] | [spacing] | Homepage Hero headline |
| H1 | [font name] | [fallback] | [weight] | [px] | [line-height] | [spacing] | Page main title |
| H2 | [font name] | [fallback] | [weight] | [px] | [line-height] | [spacing] | Section title |
| Body | [font name] | [fallback] | [weight] | [px] | [line-height] | [spacing] | Body text |
| Mono | [font name] | [fallback] | [weight] | [px] | [line-height] | [spacing] | Prices, code, labels |

**Typography principles**:
- [e.g.: never use Inter, Roboto, Arial, or other training-data default fonts]

### Spacing & Shapes

**Base unit**: [e.g. 4px] · **Density**: [compact / comfortable / spacious]

| Spacing Token | Value | Used for |
|---------------|-------|----------|
| `--space-section` | [px] | Between major sections |
| `--space-card-gap` | [px] | Between cards |
| `--space-content` | [px] | Inside cards/panels |

| Radius Token | Value | Applied to |
|--------------|-------|------------|
| `--radius-card` | [px] | Cards |
| `--radius-button` | [px] | Buttons |
| `--radius-input` | [px] | Inputs |

---

## 3. Components (Component Specs)

### Buttons

| Type | Background | Text color | Border | Radius | Padding | Weight | Hover effect | Disabled state |
|------|-----------|------------|--------|--------|---------|--------|--------------|----------------|
| Primary | `--color-accent` | [value] | none | [px] | [px] | [weight] | [description] | [description] |
| Secondary | transparent | `--color-text-primary` | 1px `--color-border` | [px] | [px] | [weight] | [description] | [description] |

**Button rules**:
- [e.g.: at most 2 Primary buttons per page]
- [e.g.: buttons give scale(0.97) feedback on press, lasting 100ms]

### Cards

| Property | Value |
|----------|-------|
| Background | `--color-surface` |
| Border | [value] |
| Radius | `--radius-card` |
| Shadow | [yes/no, specific value] |
| Padding | [px] |

### Inputs / Nav Bar / Tags / Price Display / Empty-State Component

[Fill in one by one as needed, same format as above: Role + full visual spec + hover state + transition animation]

---

## 4. UX Constraints (Interaction Rules · Required Chapter)

> Source: all interaction decisions approved by the user during Phase 4 first-screen(s) iteration and Phase 6 multi-screen design. If this chapter is missing, the DESIGN.md is considered incomplete.

### Interaction Patterns
- Filter/search/sort: [description, e.g.: filter chips filter instantly, no "apply" button]
- Navigation logic: [description]
- Form validation: [e.g.: validate on blur; error message in small red text below the input]

### State Feedback
| State | Rule |
|-------|------|
| hover | [description] |
| active | [e.g.: scale(0.97), 100ms] |
| focus | [e.g.: 2px accent-color outline] |
| disabled | [e.g.: opacity 0.5, no interaction] |
| loading | [e.g.: skeleton screens, no spinners] |

### Empty / Loading / Error States
- Empty state: [description, including illustration/copy/guiding action]
- Loading state: [description]
- Error state: [description, including retry mechanism]

### Accessibility Baseline
- Body text contrast ≥ 4.5:1
- Focus visibility: [description]
- Keyboard navigation: [description]

---

## 5. Do's and Don'ts (Red-Line Rules)

### Do
- [Specific, actionable rules]

### Don't
**AI-slop bans**:
- No Inter / DM Sans / Roboto or other default fonts
- No purple-to-blue gradient backgrounds
- No gradient text, no glassmorphism
- No identical 3-card feature rows, no numbered section markers (01/02/03)
- No Lorem Ipsum
- No pure black #000000 or pure white #FFFFFF

**Brand-specific bans**:
- [e.g.: the accent color must not be used for large-area fills]
- [e.g.: don't bold headlines]

---

## 6. Surfaces & Elevation

| Level | Background | Border | Shadow | Used for |
|-------|-----------|--------|--------|----------|
| Level 0 | `--color-bg` | none | none | Page base canvas |
| Level 1 | `--color-surface` | 1px `--color-border` | none | Cards, panels |
| Level 2 | [value] | [value] | [value] | Modals, drawers |

**Shadow strategy**: [e.g.: no shadows — layer by tone instead]

---

## 7. Imagery & Layout

**Imagery style**: [photography / illustration / banned items]

**Page skeleton**:
- Nav height: [px]
- Max width: [px]
- Hero layout: [description]
- Column ratios: [description]
- Vertical rhythm: [description]

---

## 8. Responsive Behavior

| Breakpoint | Width | Layout changes |
|-----------|-------|----------------|
| Mobile | < 640px | [description] |
| Tablet | 640-1024px | [description] |
| Desktop | > 1024px | [description] |

**Touch optimization**: minimum button height 44px; at least 8px between links

---

## 9. Spec-driven Constraints (Engineering Constraints · Recommended)

- **Cross-page consistency**: [e.g.: card radius is uniformly `--radius-card` on all pages]
- **Component reuse**: [e.g.: product cards must use the shared component; no re-implementation]
- **Tech-stack bindings**: [e.g.: colors must be referenced through CSS variables; hard-coded hex is forbidden]
- **Acceptance criteria**: [e.g.: any new page must pass the DESIGN.md Do's and Don'ts check]

---

## 10. Agent Prompt Guide (Usage Guide for Agents)

### Quick Color Reference

| Scenario | Token |
|----------|-------|
| Page background | `--color-bg` |
| Card background | `--color-surface` |
| CTA button | `--color-accent` |

### Example Component Prompts

```
Generate a product card component following DESIGN.md:
- Background: --color-surface, border: 1px solid --color-border
- Radius: --radius-card, padding: --space-content
- Title: H3, --color-text-primary
- Price: Mono font, --color-accent
- Button: Primary type, "Buy Now"
```

### Common Mistakes and Fixes

| Mistake | Fix |
|---------|-----|
| [e.g.: used a pure white background] | [use `--color-bg` instead] |

---

## Optional Extensions

### Motion & Transitions (must be expanded in detail if Phase 5 ran)

**Easing tokens** — values must be derived from the Phase 5 motion review (or the Phase 4 first screen(s) if Phase 5 was skipped), not copied from this template:
| Token | Value | Used for |
|-------|-------|----------|
| `--ease-out-strong` | [easing curve] | Elements entering/exiting |
| `--ease-in-out-strong` | [easing curve] | Elements moving |
| `--ease-drawer` | [easing curve] | Drawers/panels |

**Duration scale** — values must be derived from the Phase 5 motion review (or the Phase 4 first screen(s) if Phase 5 was skipped):
| Token | Value | Used for |
|-------|-------|----------|
| `--duration-fast` | [duration] | hover, micro-feedback |
| `--duration-normal` | [duration] | dropdowns, tooltips |
| `--duration-slow` | [duration] | modals, drawers |

**Component animation rules**: [explain one by one: buttons, modals, toasts, etc.]

**Signature move spec**: [full definition of the signature move chosen in Phase 3]

**Hard rules**:
- UI animations < 300ms
- Only animate transform and opacity
- Respect prefers-reduced-motion
- Buttons :active [press effect, e.g. scale down slightly]

---

## Appendix: Generated Assets

| File | Description | Generated in Phase |
|------|-------------|--------------------|
| [filename] | [description] | [Phase N] |

---

> **Version**: v1.0 · Generated: [date] · Final output of the full zero-to-design workflow
