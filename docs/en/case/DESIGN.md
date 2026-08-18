# Pulse Design System

> Version: v1.0  
> Source: zero-to-design workflow  
> Coverage: dashboard homepage + motion system  
> Status: Final

---

## 1. Design Soul

**Pulse** is a data dashboard for indie developers. Its visual style is **"editorial calm"**: like a well-typeset morning newspaper, it builds order through hairline rules, whitespace, and information density rather than stacked cards and ornamentation. It aims to ease the low-level anxiety of "how is my product doing today?" within 30 seconds.

Color strategy: warm light gray background + deep charcoal text + forest green accent. Green represents "normal/healthy" and only appears in statuses and positive changes; warnings and errors use low-saturation warm brown/sienna red that is not harsh on the eyes.

Typography strategy: Display uses Source Serif 4 to bring a human editorial quality; Body uses Manrope to ensure data readability; Mono uses JetBrains Mono for amounts, percentages, and timestamps. The numbers themselves are the protagonists; no charts required.

Motion strategy: All motion uses the same natural deceleration easing, with restrained durations. No flashing, no bouncing, no distraction. Motion's job is to "confirm" and "guide," not to "perform."

---

## 2. Tokens

### 2.1 Color Palette & Roles

| Name | Value | Token | Role |
|------|-------|-------|------|
| Page Background | #F5F4F0 | `--bg-page` | Page background, creates a warm paper feel |
| Primary Text | #1F1F1F | `--text-primary` | Headings, large numbers, body emphasis |
| Secondary Text | #5C5C5C | `--text-secondary` | Labels, helper text, dates |
| Tertiary Text | #8A8A8A | `--text-tertiary` | Timestamps, footer links, de-emphasized info |
| Accent | #2D5A3D | `--accent` | Brand identity, positive status, primary action |
| Accent Hover | #234A30 | `--accent-hover` | Button/link hover |
| Card Surface | #FAFAF8 | `--surface-card` | Cards, navigation, action item backgrounds |
| Surface Hover | #F2F1EC | `--surface-hover` | Interactive item hover background |
| Subtle Border | #DEDCD5 | `--border-subtle` | Hairline rules, card borders, dividers |
| Strong Border | #C8C6BF | `--border-strong` | Darkened border on hover |
| OK Status | #2D5A3D | `--status-ok` | Health indicators, positive changes, success states |
| Warning Status | #9A6B2B | `--status-warn` | Anomalies worth attention, not urgent |
| Error Status | #8B3A2E | `--status-error` | Errors, severe drops, failure states |
| Badge Background | #E8EDE9 | `--badge-bg` | Status badges, tags, icon containers |

### 2.2 Typography Rules

| Role | Font | Weight | Size / Line-height | Usage |
|------|------|--------|-------------------|-------|
| Display | Source Serif 4 | 600 | clamp(36px, 5vw, 56px) / 1.1 | Page headlines, mastheads |
| Section Title | Source Serif 4 | 600 | 22px / 1.2 | Section titles (Recent Events, Quick Actions) |
| Body | Manrope | 400 | 15px / 1.6 | Body text, event descriptions, nav links |
| Body Strong | Manrope | 500–600 | 14–15px / 1.6 | Event titles, action card titles |
| Label | Manrope | 600 | 11px / 1.4, uppercase, letter-spacing 0.08em | Metric labels, microheadings |
| Metric | JetBrains Mono | 600 | 32px / 1.1 | Key numbers |
| Data | JetBrains Mono | 500 | 12–14px / 1.4 | Percentages, timestamps, dates |

**Font Loading**: Load `Source Serif 4`, `Manrope`, and `JetBrains Mono` via Google Fonts, using `font-display: swap` to avoid layout shift.

### 2.3 Spacing & Shape

- **Base Unit**: 4px
- **Max Page Width**: 1200px
- **Page Padding**: 32px (20px on mobile)
- **Section Spacing**: 48px (above masthead), 32px (main content padding)
- **Card Padding**: 16px (action card), 24px (metric cell horizontal), 28px (metric cell vertical)
- **Border Radius**: 4px (badge), 6px (button/status bar), 8px (icon container), 10px (action card), 50% (avatar/dot)
- **Shadows**: Used only for hover feedback: `0 4px 12px rgba(0, 0, 0, 0.05)`; no large decorative shadows

---

## 3. Components

### 3.1 Top Navigation

- Height 56px, sticky top, `--surface-card` background, bottom 1px `--border-subtle` divider.
- Logo is the Source Serif 4 brand wordmark; an 8px dot on the left uses `--accent`.
- Nav links are Manrope 500 14px, default `--text-secondary`, hover becomes `--text-primary` + `--surface-hover` background, active state uses `--bg-page` background.
- User avatar is a 32px circle with `--border-subtle` background, hover becomes `--border-strong`.

### 3.2 Masthead

- 48px padding top, 28px padding bottom.
- Large title on the left (Display), date on the right (Mono 14px).
- Status badge below: `--badge-bg` background, dot + text, indicates today's overall status.

### 3.3 Metric Band

- 4-column grid, each column separated by a 1px vertical line.
- Cell padding: 28px 24px, hover background `--surface-hover`.
- Metric labels are uppercase, metric value JetBrains Mono 32px, change indicators use arrow + Mono 12px.
- **No embedded trend charts or mini-graphs allowed**; trends belong on the detail page or in weekly reports.

### 3.4 Event Stream

- List items are a 3-column grid: time / content / tag.
- Time uses Mono 12px `--text-tertiary`; title Manrope 500 15px; detail Manrope 400 13px `--text-secondary`.
- Tags use badge style: Revenue/Product/Analytics use `--badge-bg` + `--accent`, Attention uses warm brown background + `--status-warn`.
- List items have `--surface-hover` background on hover, 8px radius, clickable.

### 3.5 Quick Action Cards

- White card, 1px `--border-subtle` border, 10px radius.
- Contains a 36px icon container (`--badge-bg` background), title + description, and a right arrow.
- Hover lifts 2px + subtle shadow + darker border + arrow moves right 3px.
- Active returns to original position.

### 3.6 Footer

- Top 1px divider, data sync time on the left, Help/Feedback/Privacy links on the right.

---

## 4. UX Constraints (Interaction Rules)

### 4.1 Implemented Interactions

- **hover**: Metric cells, event items, action cards, and nav links all have `--surface-hover` or darkened backgrounds.
- **focus-visible**: All interactive elements show a 2px `--accent` outline, offset 2px.
- **active**: Action cards cancel the lift on press and return to `translateY(0)`; buttons scale down to 97%.
- **Clickability**: Metric cells and event items carry `role="button"` and `tabindex="0"`, hinting at drill-down.

### 4.2 Status Feedback Rules

- Normal metrics: no border, numbers in `--text-primary`.
- Needs attention: `--status-warn` text or border, no flashing, no pop-ups.
- Error: `--status-error` text or border, equally restrained.
- All status transitions complete within 150ms to avoid abruptness.

### 4.3 States Not Yet Covered

- Loading / skeleton states
- Empty states (no events, no data source connected)
- Error states (sync failed, missing data)
- Drill-down detail page for abnormal metrics

---

## 5. Motion & Transitions

### 5.1 Easing Curve

The only easing used across the site is `cubic-bezier(0.25, 1, 0.5, 1)` (ease-out-strong), fast at first then slowly decelerating.

**Disabled**: bounce, elastic, spring, and other rebound curves.

### 5.2 Duration Specs

| Scenario | Duration | Easing | Properties |
|------|------|------|------|
| Hover feedback | 150ms | ease-out-strong | background, transform, border-color |
| Press feedback | 150ms | ease-out-strong | transform: scale(0.97) |
| Arrow nudge | 200ms | ease-out-strong | transform: translateX(3px) |
| Entrance animation | 350–500ms | ease-out-strong | transform, opacity |
| Hairline draw | 800ms | ease-out-strong | transform: scaleX / scaleY |

### 5.3 Motion Checklist

- **Rules Draw**: After page load, hairline rules draw in sequence (horizontal 0.8s, vertical 0.8s, delays 0.2s/0.45s/0.65s).
- **Hover Transitions**: 150ms ease-out for background, border, and color changes.
- **Press Feedback**: Buttons scale to 97%, cards sink 1px, crisp and clean.
- **Arrow Feedback**: Action card hover moves the arrow 3px right over 200ms.
- **Staggered Entrance**: When multiple elements enter, stagger delays by 50–100ms.
- **Reduced Motion**: When `prefers-reduced-motion: reduce` is active, all animation durations are forced to 0.01ms.

### 5.4 Technical Constraints

- Animate only `transform` and `opacity`; avoid layout properties (width, height, top, left).
- Motion must not block interaction; users can operate while animations are running.
- All animation durations stay under 500ms, with the hairline draw as the sole exception (800ms).

---

## 6. Red Lines

### Do

- Use hairline rules to build structure and order.
- Keep metric numbers the visual protagonists, highlighted with JetBrains Mono.
- Use `--status-ok` for "normal" and `--status-warn" for "needs attention," but avoid large areas of high-saturation warning colors.
- Preserve generous whitespace so the page can "breathe."
- Use only ease-out-strong for motion, keeping a clean confirming feel.

### Don't

- No purple, no blue as primary, no gradient backgrounds.
- No embedded trend charts or mini-graphs in the metric band (causes information anxiety).
- No normal metrics shown in red/orange.
- No cards inside cards.
- No pure black #000000 or pure white #FFFFFF.
- No bounce / elastic easing curves.
- No continuously flashing alerts.
- No entrance animations longer than 500ms.

---

## 7. Surfaces & Elevation

| Level | Usage | Color |
|-------|------|------|
| 0 | Page canvas | `--bg-page` |
| 1 | Navigation, cards, action items | `--surface-card` |
| 2 | Hover feedback | `--surface-hover` |
| 3 | Emphasis blocks | `--badge-bg` |

Elevation strategy: No shadows for layering; hierarchy is built only with 1px hairline rules and background color differences; light shadows are allowed only on hover.

---

## 8. Imagery & Layout

- No illustrations, photography, or logo walls.
- Page skeleton: sticky nav → masthead → metric band → two-column layout (event stream + quick actions) → footer.
- Column ratio: main column 1fr, side column 360px.
- Visual rhythm: built through hairline rules and section padding, not card shadows.

---

## 9. Responsive Behavior

- **> 960px**: 4-column metric band + two-column layout.
- **≤ 960px**: Metric band becomes 2×2 grid; main and side columns stack into a single column; nav links hidden (hamburger menu alternative available).
- **≤ 560px**: Metric band single column; event items switch to 2-column grid with time on its own row.
- Mobile padding: 20px.
- Touch targets: nav links, action cards, and event items are all ≥ 44px tall.

---

## 10. Spec-driven Constraints

- Colors, fonts, and radii must reference CSS variables; no hard-coded values.
- New pages must follow the `--bg-page`, `--text-primary`, `--accent`, and hairline rules language.
- Metric band, event stream, and action cards should be extracted as reusable components.
- Tech stack binding: none at this time; currently a static HTML/CSS prototype.

---

## 11. Agent Prompt Guide

### Quick Color Reference

- Background: `#F5F4F0`
- Primary text: `#1F1F1F`
- Accent: `#2D5A3D`
- Card: `#FAFAF8`
- Border: `#DEDCD5`
- Warning: `#9A6B2B`
- Error: `#8B3A2E`

### Example Prompts

- "Generate a data detail page using the Pulse design system, keeping hairline rules and Source Serif 4 headings, primary color `#2D5A3D`."
- "Add an empty state component for Pulse, using `--surface-card` background, `--border-subtle` dashed border, and Manrope 13px copy."
- "Add a new event type to the Pulse homepage, preserving the event stream component's 3-column grid and hover background change."

### Common Mistakes

- Misusing blue as accent → change to `#2D5A3D`.
- Adding a sparkline to the metric band → remove it, keep numbers pure.
- Adding heavy shadows to cards → only light shadows on hover are allowed.
- Using bounce easing → change to `cubic-bezier(0.25, 1, 0.5, 1)`.
- Making alerts flash → use stable border/text highlight instead.

---

## File List

- `design/DESIGN.md` — this file, the complete design system documentation
- `design/tokens.css` — ready-to-import CSS custom properties
- `design/04-dashboard-v1.html` — homepage implementation reference
- `design/05-motion-review.html` — motion review reference
