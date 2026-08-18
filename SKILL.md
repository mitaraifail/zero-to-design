---
name: zero-to-design
description: |
  Interactive design workflow skill that supports both new products and existing systems: product definition → reference collection → design direction selection → first-screen(s) iteration → core screen expansion → cross-screen polish → a continuously evolving DESIGN.md. For existing systems, it can reuse and validate existing design assets, or explore the codebase and running UI to extract an observed design baseline before entering core screen expansion or a targeted polish pass.
  Suitable for: brand/page design for new projects, redesigns, building a design system from scratch, adding pages/components to an existing application, auditing an existing UI system, and extracting DESIGN.md from an established codebase.
  Trigger words: "zero to design", "design from scratch", "existing system design", "design an additional page", "add a component to my app", "audit existing UI", "extract DESIGN.md", "brand design flow", "design direction", "generate DESIGN.md", "从 0 设计", "已有系统接入", "设计新页面", "设计新组件", "提取 DESIGN.md", "品牌设计流程", "设计方向选择", "生成 DESIGN.md".
triggers:
  - "zero to design"
  - "zero-to-design"
  - "design from scratch"
  - "existing system design"
  - "design an additional page"
  - "add a component to my app"
  - "audit existing UI"
  - "extract DESIGN.md"
  - "brand design flow"
  - "design direction"
  - "generate DESIGN.md"
  - "从 0 设计"
  - "从 0 到 1 设计"
  - "已有系统接入"
  - "设计新页面"
  - "设计新组件"
  - "提取 DESIGN.md"
  - "品牌设计流程"
  - "设计方向选择"
  - "生成 DESIGN.md"
---

# zero-to-design · An Interactive 0-to-1 Design Workflow

An interactive design-guidance skill built for backend engineers and non-designers. Through 7 Phases (2 of them optional) of multi-turn conversation, it turns a vague product idea into an actionable DESIGN.md, page design mockups, and motion constraints.

**Core principle**: never assume the user has design experience. Every step explains the "why" and offers concrete options to choose from.

**Global rule: Language Matching (mandatory)**

- Detect the user's language from their first message and use it consistently for EVERYTHING: all conversation, every question you ask, and every generated artifact — including visible copy inside HTML pages (section titles, tooltips, button labels, demo-area names), and the content of `01-product.md`, `02-references.md`, `DESIGN.md`, and `design/state.md`.
- If the user writes in Chinese, the entire experience is in Chinese. If in English, entirely in English. If in Japanese, entirely in Japanese. And so on for any other language.
- Markdown artifacts (`01-product.md`, `02-references.md`, `DESIGN.md`) must use the user's language for ALL visible text, including chapter titles, section headings, table headers, field labels, and explanatory paragraphs. Do not keep English headings like `Product Definition` or `Core Palette` when the user is Chinese — translate them.
- The ONLY things that always stay in English: file names, directory names, CSS custom property names, token names, code identifiers, and font family names.
- Feedback phrases shown as examples (like "looks good" / "change X" / "none of them") must also be presented in the user's language, so the user knows how to reply in their own words.
- Never mix languages within a single artifact.

## Design-constraint skills (discover, don't require)

This skill has **no hard dependencies**. At Phase 3 it scans the user's environment for design-related skills they already installed, verifies which ones load, and lets the user decide which to use; Phases 4 / 5 / 6 / 7 carry that choice forward.

The lists below are **recommendation priorities for well-known skills when they are discovered** — not installation requirements. If none are found, the built-in fallback rules apply and the flow continues uninterrupted.

### Priority 1: `impeccable` (primary constraint layer, strongly recommended)

- [`impeccable`](https://github.com/pbakaus/impeccable) is a toolbox of focused design sub-skills by pbakaus, built to remove AI slop and enforce taste.
- Across the Phases of zero-to-design, load only the sub-skills most relevant to the current task; do NOT load all 23 at once.

| Phase | Recommended impeccable sub-skills | Purpose |
|-------|-----------------------------------|---------|
| Phase 3 Direction Round | `bolder`, `shape`, `critique` | Make directions bolder and more differentiated; evaluate whether a direction serves the product |
| Phase 4 First Screen(s) | `typeset`, `layout`, `delight` | Fine-tune the chosen first-screen(s) direction without changing its identity |
| Phase 5 Core Screen Expansion | `layout`, `clarify` | Extend the approved system to core screens, states, and reusable components |
| Phase 6 Cross-Screen Polish | `clarify`, `typeset`, `layout`, `animate`, `audit` | Run dimension-by-dimension passes across all core screens and resolve drift |
| Phase 7 Design System | `audit`, `clarify` | Extract components, check accessibility, unify copy tone |

### Priority 2: `frontend-design` (fallback constraint layer)

- Anthropic's official frontend design skill, focused on page-level HTML/CSS implementation.
- Directly provides anti-AI-slop rules, font/color/layout bans, and component specs.
- Use when `impeccable` is unavailable or when the user explicitly prefers it.

### Priority 3: Built-in fallback rules

If `impeccable` and `frontend-design` are both unavailable, do **not** interrupt the flow — automatically activate the following built-in simplified rules.

**Discovery strategy**:

1. **At the start of Phase 3, run the "dynamic discovery" flow to let the user confirm the constraint skill**; Phases 4 / 5 / 6 / 7 carry that choice forward without asking again (unless the user explicitly requests a change).
2. **Selectively load impeccable sub-skills based on the current Phase** (see the table above). If a sub-skill doesn't exist, just skip it.
3. **If `impeccable` is not installed, try `frontend-design`**; if that also fails, activate the built-in fallback rules.
4. **Tell the user in conversation which constraint source is currently in use**: "impeccable sub-skills loaded" / "frontend-design rules loaded" / "Currently using built-in simplified rules; install the impeccable skill if you want stronger constraints."

**Built-in fallback rules** (the agent must strictly follow these when no external skill is available). These are **negative constraints only** — they tell the agent what NOT to do. They are not design directions, and they must not be used to derive positive design decisions (e.g. "the fallback bans Inter, so I'll use Helvetica" is wrong; the font must be derived from the product definition and references):

- **Font bans**: no Inter, Roboto, Arial, DM Sans, DM Serif, Plus Jakarta Sans, Outfit, Space Grotesk, Space Mono, IBM Plex (all), Fraunces, Instrument Serif, Playfair Display, Cormorant, Lora, Crimson, Newsreader, Syne
- **Color bans**: no purple-to-blue gradient backgrounds; no cream/bone/beige backgrounds paired with brass/clay/oxblood accents (the premium-consumer reflex); no neon glows
- **Layout bans**: no eyebrow above every section; no numbered section markers (01/02/03); no identical 3-card feature rows; no hero metric template; no gradient text; no glassmorphism as default decoration
- **Copy bans**: no em dashes; no "seamless", "elevate", "unleash", "empower", "next-gen"; no aphoristic three-line cadence
- **General rules**: no Lorem Ipsum; no pure black #000000 or pure white #FFFFFF; no large decorative shadows that serve no purpose

## Workflow Overview

```
Entry A: New Product             → Phase 1
Entry B: Existing System         → Existing-system intake → Phase 5 / Phase 6
  ├─ Reusable design assets      → read and validate existing source
  └─ No design assets            → explore system → create baseline DESIGN.md

Phase 1: Product Discovery      → outputs 01-product.md
Phase 2: Inspiration Gathering  → outputs 02-references.md
Phase 3: Direction Round        → outputs 03-directions.html + user selection
Phase 4: First Screen(s) Preview Loop → outputs 04-<screen>-v1.html (or 04-<screen1>-<screen2>-v1.html) → v2 → v3... + DESIGN.draft.md
Phase 5: Core Screen Expansion → outputs 05-<screen>-v1.html + screen map + component inventory
Phase 6: Cross-Screen Polish → outputs polish logs/reviews + updated screen previews + DESIGN.draft.md
Phase 7: Design System          → outputs DESIGN.md + tokens.css + assets/
```

> File numbering aligns with Phase numbers: the output files of Phase N carry the `0N-` prefix (except Phase 7's final outputs DESIGN.md / tokens.css, which take no numeric prefix).

## Entry Resolution and Project Scope

Resolve the user's intent and project scope before reading `design/state.md`, inspecting source files, or creating any artifact. The project scope is the repository or application whose design files this skill may read or write.

1. **Use explicit intent first.** If the user's request clearly says to create a new product, redesign an existing product, add a page/component to an existing application, continue an existing workflow, or start over, use that intent directly. Explicit "from scratch", "start over", or "complete redesign" intent takes precedence over automatic state recovery. Do not ask the user to choose a mode they have already specified.
2. **Use the current directory when it is clear.** If the request refers to the current project and the working directory is an identifiable project directory, use it and tell the user which project is in scope. Do not ask for the same path again.
3. **Ask only when the mode is ambiguous.** For a generic invocation such as "help me design this", ask one focused question in the user's language:

   > 你这次是要从零创建一个新产品，还是在已有项目中设计页面或组件？如果要继续上次的设计流程，也可以直接告诉我。

4. **Separate local scope from runtime evidence.** An explicit local project path determines what the skill may read and where it may write. A running URL is only a runtime inspection target; it does not change the local read/write scope. If the user provides both and they refer to different applications, inspect the URL only as runtime evidence and keep all artifacts in the explicit local project. If the user provides only a URL and the current directory is not clearly the corresponding local project, ask for the local project directory before reading source files or creating artifacts. Never read one application and write artifacts into an unrelated current directory.
5. **Confirm the project directory only when it is unclear.** For either entry mode, ask for the project directory only if the current directory is not an obvious target. Prefer the local project directory; request a running URL only when runtime UI inspection would add useful evidence.
6. **Resolve restart safety before state recovery.** Briefly state the selected entry mode, local project directory, and optional runtime URL. If the user explicitly requested a restart or complete redesign and `design/state.md` already exists, do not resume it or overwrite it. By default, create a new workspace at `<project>/design-restarts/<YYYYMMDD-HHmmss>/`; if the user provides another workspace path, use that path instead. In a restart workspace, all relative artifact paths in this skill resolve from the workspace root, so the new state file is `<workspace>/design/state.md` and new outputs are under `<workspace>/design/`. The original project may be inspected as the implementation source, but writes must be limited to the resolved workspace. If the user chooses to continue in the original project, first make a non-destructive copy of the existing `design/` directory to an approved backup/archive path, verify the backup exists, and only then write new artifacts in the original location. Otherwise, check `design/state.md` in the resolved project and resume it when applicable. An explicit local project path takes precedence over the current directory; a URL never becomes the write scope.

Do not make the user answer separate mode and location questions when both are already clear from the request. Do not inspect or create design artifacts in an unresolved directory.

## Entry Modes

Choose the entry mode before starting Phase 1. Do not force an existing product through the 0-to-1 questions when the user asks to design a new page or component inside an already-running system.

### Entry A: New Product

Use the normal flow when the product is new or no existing application is in scope. A complete redesign of an existing product is also a restart request: use Phase 1 only after the restart-safety rule has preserved the existing design state and established the new design workspace.

### Entry B: Existing System

Use this mode when the user has an existing repository, running application, or established UI and wants to design additional pages or components. Resolve the project directory through Entry Resolution, then inspect the system before making visual decisions. The target page/component comes from the user's request; ask for it only when it is not already clear. A running URL is optional runtime evidence, not a prerequisite for local inspection.

First determine which of these two cases applies:

1. **Existing design assets are available.** Search for `DESIGN.md`, `design-system.md`, token files, theme files, component documentation, and project-level agent instructions. Treat the user's identified source of truth as authoritative after checking that it matches the running implementation. Read the relevant routes, global styles, tokens, and reusable components. Do not generate a second design system merely because the files are not under `design/`.
2. **No usable design assets are available.** Explore the repository and, when possible, the running application. Inspect routes, layouts, representative pages, global CSS, theme variables, typography imports, component primitives, responsive breakpoints, interaction states, and loading/empty/error states. Use observed implementation as evidence; do not invent a new visual direction. Produce a baseline design-system document that records observed rules, source paths, confidence, unresolved inconsistencies, and safe extension rules.

The existing-system intake must produce or identify these artifacts before Phase 5. Unless the user has explicitly chosen another location, generated intake artifacts live under `design/`:

- `design/existing-system.md` — system scope, technology, routes, visual language, responsive behavior, accessibility baseline, and source-of-truth paths.
- `design/component-inventory.md` — reusable components and primitives, with each target marked `reuse`, `extend`, or `new`.
- `DESIGN.md` or the existing equivalent — the canonical design-system source. If generated from exploration, mark it as an observed baseline and preserve evidence links to source files.
- `design/state.md` — record `Entry Mode: existing-system`, the canonical source path, the exploration status, and the target screens.

After intake, enter Phase 5 directly when the request involves new core screens or a multi-screen extension. If the request is a narrow refinement of one existing screen, enter Phase 6 directly and run only the relevant polish passes. Phase 1–4 are not required unless the user requests a new visual direction or a complete redesign.

### Existing-System Source Rules

- Prefer the repository's real source of truth over generated copies: existing tokens over retyped tokens, existing components over HTML-only substitutes, and existing routes over invented navigation.
- Preserve the existing technology and rendering model. A Nuxt/Vue system should receive Vue/Nuxt implementation guidance; a React system should receive React guidance, and so on.
- Separate observed facts, inferred rules, and proposed changes in `design/existing-system.md` and the active canonical design source.
- If the existing system is inconsistent, record the inconsistency and choose a local extension rule for the target page. Do not silently normalize the whole product.
- A new page may introduce a token or component only when the inventory explains why reuse or extension is insufficient.
- Do not overwrite or relocate existing design assets without explicit user approval. If a canonical source is outside `design/`, reference it from `design/state.md` and the generated artifacts.
- If the application cannot be run, continue with static inspection and mark runtime observations as unavailable; do not claim that behavior was verified.

After each Phase completes, **if the agent has high confidence in the current Phase's output (no ambiguity, nothing missing, user feedback was clear), it may proceed directly to the next Phase** — no need to ask "Shall we move on to Phase X?".

**Cases where you must ask the user for confirmation**:
- The user's answer was vague or the agent made an uncertain inference
- The current Phase has unresolved open questions
- An irreversible decision is involved (such as final approval of DESIGN.md)

**Cases where you do NOT need to ask**:
- Phase 1: all 8 required questions have clear answers, and the key screen(s) have been explicitly confirmed; the agent is just organizing them into documents
- Phase 2: the user has provided enough references or explicitly took the shortcut path
- Phase 3: the directions file has been generated and is awaiting the user's selection (this is necessary user input, not a confirmation)
- Phase 4: during first-screen(s) iteration, every revision needs user feedback; but once the user says "looks good", go straight to the fork decision

**How to present transitions**: when entering the next Phase with high confidence, a single sentence is enough, e.g. "Phase 1 complete — moving to Phase 2 to recommend reference sites." Do not list lengthy confirmation questions.

**Global rule: never backfill questions across Phases**

- Each Phase asks only its own questions; never go back to re-ask questions from earlier Phases.
- If the user skipped a question in an earlier Phase, the agent must infer the answer from available information and mark it as "agent-inferred" in the corresponding document.
- Later Phases may only read the output documents of earlier Phases; they must not ask the user again for information that an earlier Phase should have collected.

**Global rule: cross-session resume**

- After Entry Resolution has selected the project scope, and unless an explicit restart was requested, **the first file action is to check for and read `design/state.md`** (if it exists). Do not read a state file from the unresolved current directory or from a different project.
- If it exists and no restart was requested: resume from `Current Phase`, briefly tell the user what has been done and what's next, then continue. You must **not** re-run completed Phases, must **not** re-propose anything from `Rejected Directions`, and must **not** violate `Decisions Locked`.
- If an explicit restart or complete redesign was requested and it exists: preserve the existing state, do not auto-resume or overwrite it, and establish the restart workspace or verified backup/archive defined in Entry Resolution before starting Phase 1. When a separate workspace is used, write its `design/state.md` and all phase artifacts relative to that workspace; do not silently fall back to the original project's `design/` directory.
- If it doesn't exist, first determine whether the user is working inside an existing system. For an existing system, start with the Existing-System intake above and create `design/state.md`; otherwise start from Phase 1.

**Global rule: post-completion extension mode (designing new pages after Phase 7 is done)**

- If `design/state.md` has status `complete` and the user comes back asking for a new page (e.g. "design the search results page for me"), **enter extension mode** instead of restarting the whole flow:
  1. Read the active canonical design source recorded in `design/state.md` as the sole source of constraints. Do not assume it is `design/DESIGN.md`; it may be an existing project-level `DESIGN.md` or another documented equivalent.
  2. Follow Phase 5's screen contract and Phase 6's relevant polish passes: create the appropriate screen or component preview as `design/06-<target>-v*.html`, going one target at a time. Pages include default / loading / empty / error states; components include the relevant state and variant matrix.
  3. If user feedback touches the design-system level (e.g. "card corners should be rounder on all pages"), **update the active canonical design source recorded in `design/state.md`** and record the reason plus the user's exact words. If that source is a generated `DESIGN.md`, bump its version number (e.g. v1.0 → v1.1); otherwise preserve the source's existing versioning and update convention.
  4. Once the new page or component is approved, append it to the `File Checklist` in `design/state.md`.
- Extension mode does **not** require re-running Phases 1-4: the product definition, direction, and first screen(s) are already locked.
- Only if the user asks for a **complete redesign** (new direction / new style) should you enter the restart-safety flow, preserve the existing `design/state.md`, and establish the restart workspace or verified backup/archive defined in Entry Resolution before running the flow again. Never reset or overwrite the existing state in place.

---

## Phase 1: Product Discovery

**Goal**: through 8 key questions, make "what to build and what it should feel like" explicit.

**How to run**: ask questions step by step in conversation. You may ask one at a time (recommended — more conversational) or list 3-4 at once (more efficient for the user to answer). Adapt flexibly to how detailed the user's answers are.

**Open-input rules (must follow)**:

- The option lists the agent offers in each question are **only prompts to lower the cost of answering**, not closed multiple-choice questions.
- Every question must explicitly support the user **freely entering** their own answer. When asking, include a hint like "or just describe it in your own words".
- Example: after offering Trust/Speed/Calm options for the mood question, you must add "— or supply your own words". Same for the platform options "Web / iOS (iPhone or iPad) / Android (phone or tablet) / Desktop" in the design-constraints question.
- A freely entered answer is **equally valid** as a listed option — adopt it directly and write it into `01-product.md`; do not force-map it back onto an existing option.
- **No reverse mapping**: if the user has already described the answer in their own words (e.g. "clean, fresh, focused, with a slight creative touch"), do **not** follow up with "is that Professionalism or Creativity?". The user's own words are the most accurate answer — just record them.
- Bad example: user says "clean, fresh, focused", agent replies "I'll map that to Professionalism + Creativity, does that sound right?"
- Good example: user says "clean, fresh, focused", agent replies "Got it — the mood is clean, fresh, focused, with a slight creative touch. I'll write that into 01-product.md."

**Smart-skip rule**: if the user's initial input or subsequent answers already clearly contain the answer to a question, **do not ask it again** — just confirm it.

**Question presentation rules (must follow)**:

- The 0-7 numbering of the required questions is an **internal index — never expose it to the user**. When presenting questions to the user, **renumber the ones you're actually asking sequentially from 1** (Q1, Q2, Q3...), keeping them consecutive with no gaps.
- Present smart-skipped information in an **unnumbered confirmation block**, separate from the question list, e.g.:

  > Your initial request already contains some information — let me confirm first:
  > - This is a platform for selling digital goods, right?
  > - Homepage = brand intro + product listing, right?
  >
  > I still need to ask a few questions:
  > Q1. Product name: ...
  > Q2. Target user profile: ...
  > Q3. Mood/atmosphere: ...

- Bad example: the confirmation block uses "1. 2." numbering and the question list shows "0. 2. 4. 5." with gaps — two numbering systems mixed together, and the user can't map answers to questions.

**Common mapping examples**:

| User input | Implied answer | Agent action |
|-----------|----------------|--------------|
| "I want to design a website for selling digital goods" | Product definition (digital goods marketplace) | Just confirm: "This is a digital goods marketplace, right?" |
| "The homepage needs promotion and a product list" | Conversion goal (browse/buy products) | Just confirm: "The goal is to get users to browse and buy, right?" |
| "It's for creators" | Target users (creators) | Ask for details: "Age, occupation, how do they currently sell things?" |
| "Like Gumroad" | Key differentiator (to be confirmed) | Ask: "Compared with Gumroad, what's your differentiator?" |
| "Make it more professional" | Mood/atmosphere (professionalism) | Just confirm: "The core feel is professional and trustworthy, right?" |

**Judgment standard**: skip only when the user's answer is **clear and unambiguous**. If the answer is vague (e.g. "make it look nice"), you still need to follow up.

**Missing-information rules**:

- If the user **explicitly skips or doesn't answer** a required question (e.g. they answered product name and conversion goal but not mood/atmosphere), do **not** move on to later Phases and then circle back to ask.
- Correct approach: **infer it yourself within Phase 1** based on existing answers, write the inference into `01-product.md`, and clearly mark it as "agent-inferred".
- Inference examples:
  - User says "digital goods marketplace for creators" but never mentions mood → infer `warmth + professionalism` (creators need approachability; transactions need trustworthiness)
  - User says "B2B API marketplace" but never mentions mood → infer `trust + speed` (enterprise purchasing needs trust and efficiency)
- If you're not confident in an inference, **ask for confirmation once before ending Phase 1**: "I didn't quite catch the mood you want — based on what you've described, my inference is 'warmth + professionalism'. Does that work?" — close the loop inside Phase 1; don't drag it into Phase 3.

**Required questions** (in order; numbers are internal indexes — when presenting to the user, renumber per the "question presentation rules"):

0. **Product name**: What is this product called? (Used in all subsequent design files.)
1. **One-sentence product definition**: In your own words, not an official slogan — what is this?
2. **Target user profile**: Who is the single most typical user? (Age, occupation, how they currently make money / sell things)
3. **User mental state**: Before opening this page, what expectations or emotions does the user carry? (Curious? Skeptical? Looking for a tool? Recommended by someone?)
4. **Mood/atmosphere**: What core feeling should the interface convey? Pick 1-2 from below, or supply your own:
   - **Trust** (trustworthy / professional / reliable)
   - **Speed** (efficient / agile / no time wasted)
   - **Calm** (peaceful / focused / not anxious)
   - **Excitement** (exciting / sense of discovery / want to explore)
   - **Professionalism** (professional / rigorous / enterprise-grade)
   - **Warmth** (warm / friendly / human)
   - **Playfulness** (fun / lighthearted / not serious)
   - **Creativity** (creative / inspiring / unique)
5. **Key differentiator**: Compared with the main competitors, what is the single most important difference? (Pick only the most important one.)
6. **Conversion goal**: What action do you most want users to take on this page? (Sign up? Download? Purchase?)
7. **Design constraints**:
   - Platform: Web / iOS / Android / Desktop? For iOS / Android, always also record the device form factor — phone (iPhone / Android phone) or tablet (iPad / Android tablet). If the user only says "iOS", "Android", or "mobile", ask once: "Is the primary device a phone or a tablet?" Never end Phase 1 without a recorded form factor, and never silently assume tablet.
   - Audience age range: <range>
   - Accessibility needs: any special requirements (colorblind-friendly, screen readers, large-text mode)?
   - Existing brand assets: existing logo / colors / fonts? (If any, please provide.)

**Optional follow-ups** (decide based on answer quality):

- If the user says "pretty much the same as competitors" → ask: then why would users choose you over them?
- If the user says "the target audience is very broad" → ask: if you could only serve one type of person, which type?
- If the user says "I want it to look good" → ask: good-looking so that users feel it's professional / trustworthy / fun / premium, or something else?
- If the user's answer to "mental state" is vague → ask: when a user first hears about this product, is their most likely reaction "I need this" or "what's this for?"

**Output**: create `design/01-product.md` in the project root, containing the fields below. **All section headings and field labels must be written in the user's language** (e.g. if the user is Chinese, use `产品定义` / `产品名称` / `一句话定义` / `目标用户` / `用户心理预期` / `氛围关键词` / `核心差异点` / `转化目标` / `设计约束`).

```markdown
# Product Definition · <Product Name>

## Product Name
<Product name>

## One-Sentence Definition
<User's answer>

## Target Users
<Profile description>

## User Mental State
<Expectations/emotions before opening the page>

## Mood/Atmosphere
<Core feeling the interface should convey: trust / speed / calm / excitement / professionalism / warmth / playfulness / creativity>

## Key Differentiator
<Differentiator>

## Conversion Goal
<Target action>

## Design Constraints
- Platform: Web / iOS (iPhone or iPad) / Android (phone or tablet) / Desktop
- Audience age range: <range>
- Accessibility needs: <any special requirements>
- Existing brand assets: <logo/colors/fonts, if any>

## Key Screens for Phase 3/4 (1–2 screens, confirmed at end of Phase 1)
- <screen A>
- <screen B> (optional — only when two tightly-coupled screens were confirmed)
```

**Approval gate**: all 8 required questions have clear answers (answered by the user, or inferred by the agent and marked as such), and the user has explicitly confirmed 1 or 2 Key Screens. Only after both conditions are met, **record the confirmed screens in `design/state.md` and `01-product.md`, generate `01-product.md` if it does not exist, and proceed to Phase 2** — no need to ask "Shall we move to Phase 2?".

**Phase 1 → Phase 2 handoff: confirm the key screen(s) for Phase 3/4**

After the 8 product-definition questions are complete and before the Phase 1 approval gate is satisfied, propose which 1–2 screens should be designed together in the next phases. Most products start with **1 key screen**; choose **2 screens only when they are tightly coupled and must be seen together** to judge the design language (e.g. chat list + chat detail, storefront + product detail, card feed + profile).

Ask the user like this:

> In Phase 3 and Phase 4 I'll generate design directions and a first mockup for the most critical screen(s). Based on what you've described, I propose we start with **<screen A>**{** and <screen B>**}. Does this match what you had in mind, or would you prefer a different screen? You can pick **one screen** or **two screens at most**.

Record the confirmed screen(s) in `design/state.md` under **Key Screens** and in `01-product.md` under **Key Screens**. If the user only wants one screen, omit the optional second entry; do not silently add a second.

---

## Phase 2: Inspiration Gathering

**Goal**: move the user from "I don't know what I want" to "I know what I like and what I don't like".

**How to run**:

1. **Agent proactively recommends**: based on the Phase 1 product definition, recommend 5-10 references. **Match the reference type to the target platform from Phase 1**:
   - **Mobile / native app products**: recommend real mobile apps (App Store / Play Store / official landing pages) and mobile-app screenshot galleries. Do not default to desktop websites.
   - **Web / desktop products**: recommend websites and web-focused galleries.
   - **All platforms** must cover the four categories below — font inspiration libraries are not optional. Every recommendation must include a directly accessible domain, store link, or specific page URL; don't make the user search for it:
     - 2-3 similar products (direct competitors)
     - 2-3 cross-category products or experiences with a matching vibe
     - 2-3 design inspiration galleries appropriate to the platform
     - **1-2 font inspiration libraries (mandatory, listed separately)**: Typewolf, Font Pair, Fontshare, Coolors, etc. Explain what each is for, e.g. "Typewolf for real-world font pairings, Fontshare for free commercially-usable fonts, Coolors for trying color palettes"

   Example recommendation output for a **web product** (must include a "Font inspiration libraries" section; every reference with its domain):

   > Similar competitors (see how they do the "shelf"): Gumroad (gumroad.com) / Lemon Squeezy (lemonsqueezy.com) / Patreon (patreon.com)
   > Cross-category vibe references (see how "simple but human" is done): Etsy (etsy.com) / Monocle (monocle.com) / indie bookstore sites like Strand Bookstore (strandbooks.com)
   > Design inspiration galleries (see how details are handled): Mobbin (mobbin.com) / Godly (godly.website) / Awwwards (awwwards.com)
   > **Font inspiration libraries (pick font pairings)**: Typewolf (typewolf.com) / Fontshare (fontshare.com)

   Example recommendation output for a **mobile app product**:

   > Similar competitors (study their mobile flows: onboarding, matching, chat, profile): Hinge (hinge.co / App Store) / Bumble (bumble.com / App Store) / Soul (soulapp.cn / App Store)
   > Cross-category vibe references (see how "trust + warmth" feels on mobile): Headspace (headspace.com / App Store) / Aesop (aesop.com) / Monocle (monocle.com)
   > Mobile design inspiration galleries (search dating / chat / onboarding): Mobbin mobile (mobbin.com/browse/ios/apps) / Screenlane (screenlane.com) / UI8 mobile (ui8.net/category/ios)
   > **Font inspiration libraries (pick font pairings)**: Typewolf (typewolf.com) / Fontshare (fontshare.com)

   **Forbidden**: writing just "Gumroad" or "some indie bookstore" without a domain/store link, forcing the user to search. For mobile apps, pointing only at a desktop marketing site without mentioning the app store or mobile screenshots is also forbidden.

2. **Ask the user for screenshots + overall impressions**: have the user open the recommended references and answer two layers of questions for each:

   **Overall level (scan the whole reference first, answer by intuition):**
   - How does this app / website / experience feel overall? (Professional / warm / bold / calm / lively / premium / approachable / other)
   - Would you want your product to have a bit of this vibe? If so, which bit?
   - Are there any overall vibes you definitely do NOT want?

   **Specific screenshot level:**
   - Screenshot 1-2 screens or spots where you think "this part is nice" or "I don't like this part"
   - What specifically do you like/dislike? (Color / typography / layout / motion / copy / spacing / image style)

3. **Offer a shortcut path (when there's no time to look at sites one by one)**: explicitly give the user two shortcut options — do **not** add extra A/B/C letter choices:

   > If you don't have time to look at them one by one, just reply in natural language:
   > - "Just go ahead" — I'll infer the aesthetic boundaries from the common vibes of similar products and continue into Phase 3 direction generation.
   > - Or state your explicit preferences first, then say "just go ahead". For example: "No red, blue, purple, or gradients; use serif fonts. Just go ahead." or "Clean black-on-white with a few bright accents. Just go ahead."

   **Forbidden**: appending letter options like "A. Go look at the sites / B. Take the shortcut / C. Let me infer" after the shortcut instructions. The user just replies in natural language.

   When the user takes the shortcut with preferences, record their explicit statement verbatim in the "Explicit Preferences" section of `02-references.md` — these are **hard constraints** in Phase 3.

4. **Organize into a document**: compile the user's screenshots, overall impressions, local annotations (and explicit preferences if the shortcut was taken) into `02-references.md`.

**Recommended reference list by product type and platform**:

| Product type | Similar references | Cross-category vibe references | Design inspiration galleries |
|--------------|-------------------|-------------------------------|------------------------------|
| Digital goods / creator platforms (web) | Gumroad (gumroad.com), Lemon Squeezy (lemonsqueezy.com), Patreon (patreon.com) | Indie bookstores like Strand (strandbooks.com), magazines like Monocle (monocle.com), handmade-craft platforms like Etsy (etsy.com) | Mobbin (mobbin.com), Awwwards (awwwards.com), Godly (godly.website) |
| SaaS tools (web) | Linear (linear.app), Notion (notion.so), Figma (figma.com) | Architecture studios, consulting firms, premium e-commerce | SaaS Landing Page (saaslandingpage.com), Lapa (lapa.ninja) |
| Community / content (web) | Discord (discord.com), Reddit (reddit.com), Substack (substack.com) | Cafés, libraries, galleries | Cosmos (cosmos.so), Savee (savee.it) |
| Finance / enterprise (web) | Stripe (stripe.com), Mercury (mercury.com), Ramp (ramp.com) | Banks, law firms, consulting firms | Webflow (webflow.com), 21st.dev (21st.dev) |
| Mobile social / dating / messaging | Hinge (hinge.co), Bumble (bumble.com), Soul (soulapp.cn), Patook (patook.com), Lex (lex.app), Grindr (grindr.com) | Headspace (headspace.com) for calm trust, Aesop (aesop.com) for quiet premium texture, Monocle (monocle.com) for editorial warmth | Mobbin mobile (mobbin.com/browse/ios/apps), Screenlane (screenlane.com), UI8 mobile (ui8.net/category/ios), Dribbble "mobile" search (dribbble.com/search/mobile) |
| Mobile utility / productivity | Things 3 (culturedcode.com/things), Streaks (streaksapp.com), Notion mobile (notion.so/product) | Headspace (headspace.com), Bear (bear.app), Clear (clearapp.me) | Mobbin mobile (mobbin.com/browse/ios/apps), Screenlane (screenlane.com), Behance mobile UI (behance.net) |

**Output**: `design/02-references.md`, structured as below. **All section headings and field labels must be written in the user's language** (e.g. if the user is Chinese, use `参考收集` / `Agent 推荐` / `明确偏好` / `用户标注` / `提取的设计线索`).

```markdown
# Reference Collection · <Product Name>

## Agent Recommendations
<Recommended reference list + reasons; must include font inspiration libraries>

## Explicit Preferences (only filled when the shortcut path was taken; leave empty on the normal path — preferences are synthesized from user annotations)
- **User's exact words**: <e.g. "No red, blue, purple, or gradients; use serif fonts", or "none">

## User Annotations

### Reference 1: <Reference Name>
- **Platform / URL**: <mobile app / website / store link>
- **Overall impression**: <the reference's overall vibe/mood, and which parts you would/wouldn't borrow>
- **Screenshot 1**: <filename>
  - Like: <user's description>
  - Dislike: <user's description>
  - Extractable elements: <color/typography/layout/motion/copy>
- **Screenshot 2**: <filename>
  - Like: <user's description>
  - Dislike: <user's description>
  - Extractable elements: <color/typography/layout/motion/copy>

### Reference 2: <Reference Name>
...

## Extracted Design Clues
- **Overall vibe tendency**: <summarized from the user's overall impressions: warm / professional / bold / calm / lively / premium / approachable, etc.>
- **Color tendency**: <explicit preferences (if any) + synthesized user annotations>
- **Typography tendency**: <explicit preferences (if any) + synthesized user annotations>
- **Layout tendency**: <summarized from user annotations>
- **Definitely NOT**: <explicit preferences (if any) + synthesized user annotations>
```

**Approval gate**: either of the following:
- The user provided overall impressions + screenshot annotations for at least 3 references
- The user took the shortcut path ("just go ahead", or "explicit preferences + just go ahead"), and the explicit preferences have been recorded verbatim

---

## Phase 3: Direction Round

**Goal**: based on the product definition, references, and the 1–2 key screens confirmed at the end of Phase 1, output 3-4 **genuinely different** design directions for the user to choose from.

**Preconditions**: before entering Phase 3, `01-product.md` and `02-references.md` must already exist, and `design/state.md` must record the confirmed **Key Screens** (1 or 2). Phase 3 **no longer asks the user** product-definition questions (mood/atmosphere, target users, key differentiator, etc.). If some fields in `01-product.md` are empty or marked as "agent-inferred", Phase 3 must derive directions directly from those inferences and must **not** ask the user to fill them in.

**Key requirements**:
- **Load `impeccable` sub-skills first as the primary constraint layer**; if unavailable, try `frontend-design`; if both fail, activate the built-in fallback rules
- Optionally load `bolder`, `shape`, `critique` to strengthen direction differentiation
- The 3-4 directions must span different axes **relevant to the product**. These axes are dynamically derived by the agent from Phases 1/2 — not a fixed list:
  - Example axes: warm vs cool colors, serif vs sans-serif, minimal vs rich, light vs dark, editorial vs utilitarian, card grid vs list feed
  - Judgment principle: which axes best express the temperament divide of this product? What is the core choice the user is torn over?
- Each direction must be a complete design language, not "the same layout in different colors"
- **Colors must be layered**: Core Palette (3-4: background/text/accent) + UI Semantic Tokens (3-6: card/border/secondary text/status colors), with explicit role labels
- **Fonts must be named**: write out real font-family, weight, size/line-height — never just "Display/Body/Mono" with sample text
- **Platform-aware interaction vocabulary**: the target platform from Phase 1 must drive all interaction descriptions, state names, and motion triggers. Mobile/touch products use tap, press, active, long-press, swipe, and touch targets; web/desktop products use hover, click, focus, and active. In HTML previews, hover may appear as a desktop-preview convenience, but written specs must name the platform's real input modality.

**How to run**:

1. **Dynamically discover available design skills and let the user choose**:

   Before generating directions, discover as much as possible which design-related skills are available in the current environment. Execute in this order:

   **(a) Scan the skills directory**
   - Use `Glob` to scan `~/.agents/skills/` (or the current environment's skills directory) and list all skill names.
   - Filter for candidates related to visual/frontend/design. Common keywords include:
     - `impeccable`, `frontend-design`, `bolder`, `delight`, `shape`, `critique`, `typeset`, `layout`, `animate`, `polish`, `clarify`, `audit`, `taste-skill`, `emil-design-eng`, `gsap-*`
   - Don't rely only on the fixed list: if the scan finds other skills whose names are clearly design-related (e.g. `visual-design`, `ui-craft`), add them as candidates too.

   **(b) Verify by actually loading**
   - For each candidate skill found, try calling `Skill(<name>)`.
   - Record which skills loaded successfully (✓) and which failed (✗).
   - Note: a load failure only means the skill is unavailable in the current environment — not that it's absent from the directory.

   **(c) Present the discovery results and let the user confirm/supplement**
   - Present the successfully loaded skills grouped by category — **do not decide for the user**:
     - **Primary constraint skills**: `impeccable`, `frontend-design`, and other complete design rule packages
     - **Enhancement skills**: `bolder`, `shape`, `critique`, `typeset`, `layout`, `delight`, and other sub-skills
     - **Other design skills**: any other successfully loaded design-related skills found in the scan
   - Also list the skills that were **found but failed to load**, so the user knows what might be missing from the environment.
   - **Important**: Phase 3 only confirms the skill selection — it does not re-ask product-definition questions (mood/atmosphere, target users, etc.). That information is already locked in Phase 1's `01-product.md`.
   - Ask the user (the following is a template — replace it with the actual detection results when outputting):

     > I scanned for design-related skills; some loaded successfully:
     >
     > ✅ Available:
     > - Primary constraint: `impeccable`
     > - Enhancement: `bolder`, `shape`, `typeset`
     > - Other: `layout`
     >
     > ❌ Found but failed to load:
     > - `frontend-design`, `critique`, `delight`
     >
     > Please choose which skills to use for this Phase 3:
     > - **A. Recommended**: `impeccable` sub-skills (`bolder` + `shape` + any others that loaded)
     > - **B. Only `frontend-design`** (if available)
     > - **C. Only the built-in fallback rules**
     > - **D. Custom combination** (just reply with skill names, e.g. "impeccable + layout", or "frontend-design + typeset")
     > - **E. Add another skill** (if the one you want isn't listed, tell me its name)

   **(d) Load the skills the user confirmed**
   - Only call `Skill(<name>)` after the user explicitly confirms.
   - If a skill the user mentions previously failed the probe, try loading it again; if it still fails, tell the user and suggest alternatives.
   - If the user chooses the built-in fallback rules, load no external skills.

   **(e) Record the choice**
   - Record the final confirmed skill list in the **Design Constraints** section of `design/state.md`.
   - Phases 4 / 6 carry the same constraints forward unless the user explicitly asks to change.
   - If dynamic scanning fails (permissions / directory doesn't exist), fall back to fixed-list probing + user confirmation: `impeccable` → `frontend-design` → built-in fallback.

2. **Load the selected constraint skill(s)**: load skills per the user's choice. By default, recommend `impeccable` sub-skills first, then load `bolder`, `shape`, `critique` on demand if available.

3. **Generate the directions file**: create `design/03-directions.html`. You may use `templates/directions-template.html` **only** as a page-structure scaffold (top product-analysis card + direction list layout framework). The template's colors, typography, spacing, and visual treatments are placeholder examples — they must be completely replaced by values derived from `01-product.md` and `02-references.md`. Never treat the template's default dark appearance as a design direction or starting point. All visible copy in the template (section titles, tooltips, footer hints, button labels) must also be translated into the user's language — never leave English labels in a Chinese deliverable, or vice versa. The concrete design content of each direction must be freshly generated from this round's derivation. It contains:
   - Top: product-analysis card (one-sentence product definition + target users + core scenario)
   - 3-4 directions in a **2-column grid on desktop (at most 2 per row; 4 directions = 2 rows × 2 columns)**, single column on mobile. Never lay all directions out in a single row — that squeezes each direction's mini-mockup down to phone width, so the user can't judge whether a desktop/web layout works
   - **The mini-mockup's aspect ratio must match the target platform and device form factor recorded in Phase 1's Design Constraints**: web/desktop products render at a landscape, desktop-like proportion; phone products (iPhone / Android phone) render at a portrait phone-like proportion; tablet products (iPad / Android tablet) render at a tablet proportion. Never render a phone interface inside a tablet or landscape frame — that misrepresents the product even if it fills the card nicely. If the recorded form factor is ambiguous, confirm with the user before generating. If the preview area is too narrow to show a desktop layout honestly, reduce directions per row — never shrink a desktop interface into a phone-shaped frame
   - Each direction contains:
     - Direction name (two words, evocative, e.g. "Workbench White", "Clay Shelf")
     - One-sentence pitch (conveys how the direction feels, not a feature list)
     - **Rationale**: why does this direction suit the product? (Cite Phase 1's mood/atmosphere and key differentiator, or Phase 2's reference vibes)
     - **Color system**: must be shown in two layers, not just a stack of colors:
       - **Core Palette (3-4)**: background, text, accent. This is the vibe the user perceives at first glance.
       - **UI Semantic Tokens (3-6)**: card background, border, secondary text, success/warning/error states, badge background, etc. Each must carry a role label such as `surface-card`, `border-subtle`, `text-secondary`.
     - **Typography system**: must explicitly write out font names, weights, and sizes — never just "Display/Body/Mono" with sample text.
       - Format: `Display: <font name> <weight> <size>/<line-height>`, e.g. `Display: "ZCOOL XiaoWei" 600 48px/1.2`
       - Include at least Display, Body, and Mono/Accent tiers, and explain what each is for.
     - **Layout Pattern**: must explicitly describe how the target interface's key regions are organized — don't rely on the mini-mockup alone and make the user guess. **Key regions are determined by the agent based on the interface type** (a homepage might be Hero + listing area; a dashboard might be sidebar + data area; a landing page might be Hero + selling points). Describe for each region:
       - Position and proportion (e.g. "left 40%: big headline + search; right 60%: preview grid")
       - Internal information hierarchy (e.g. grid column count in the listing area, card information hierarchy, presence of filter chips)
       - The visual-weight relationship between regions
       - One sentence summarizing the overall layout strategy
     - **Animated signature move demo**: a signature move must have **both a written explanation and an actual animation** — never just a four-word title. The explanation is a full paragraph (2-4 sentences) covering:
       - What exactly is the move? (e.g.: product cards lift slightly on hover/press + shadow expands)
       - Why does this move belong to this direction? (e.g.: the "Workbench White" direction pursues "lightness with breathing room"; lifting cards makes the shelf feel gently held up)
       - Where is it used? (e.g.: only on product-card hover/press; the 3 featured cards in the mini-mockup demo it simultaneously)

       Example:
       > **Card Breathing**: on hover (web) or press (mobile), a product card rises 4px while its shadow spreads from 1px to 12px, simulating the lightness of being picked up. This move gives the "Workbench White" shelf order without losing warmth, avoiding a rigid flat grid.

     - **Mini Interface Mockup**: must **genuinely embody** the Layout Pattern, colors, typography, and signature move described above, and include enough **essential elements** for the user to judge whether the layout works.

       **Number of screens in the mockup**: if `design/state.md` records **2 Key Screens**, each direction's Interface Mockup must show **both screens together, stacked vertically** — one screen below the other, each mockup using the full width of the direction card, with a short screen-name caption above each so the user knows which is which. Never place the two mockups side by side: inside a direction card they would each shrink to half width and become too small to judge (especially desktop-shaped mockups). The goal is to let the user judge how the design language holds across the coupled interface pair. If only **1 Key Screen** is recorded, show that single screen. Never show a second screen that the user did not confirm in Phase 1.

       **Essential elements are determined by the agent from the Phase 1 product definition and interface type** — not a fixed checklist. Judgment principles:
       - When the user opens this interface, **which entries/information must be visible to complete the core action**? (Browse / search / filter / buy / log in / view data)
       - Along this interface's core conversion path, **which UI elements are indispensable**?
       - Without these elements, can the user still judge whether the layout works?

       Take a digital-goods platform homepage: essential elements usually include a nav bar (logo + main nav + login entry), a Hero area (headline + CTA), a search box, category filters, and a product grid (at least 4 cards). But for a dashboard, it might be sidebar nav + data cards + chart area; for a single-page portfolio, maybe just nav + Hero + work grid.

       **The signature move must actually trigger inside the mini-mockup**: it cannot live only in a standalone demo area. The corresponding elements in the mini-mockup must be interactive (e.g. product cards really respond to hover/press, the headline really has a highlight animation, buttons really have a pressed effect).

       Common mistakes and fixes:
       - ❌ Wrong: the mini-mockup has only 1-2 cards, so multi-card arrangement is invisible.
       - ✅ Right: the product area has at least 4 cards, showing grid density and card spacing.
       - ❌ Wrong: no search box / category filters, so the user doesn't know what those entries look like.
       - ✅ Right: search box, category chips, and login button all appear in the nav or Hero area.
       - ❌ Wrong: forcibly inserting a search box / category filters regardless of product type (e.g. bolting a search box onto a portfolio site).
       - ✅ Right: the agent first determines the core conversion path from the product definition and includes only essential elements.
       - ❌ Wrong: cards in the standalone demo area animate, but product cards in the mini-mockup don't respond to hover/press at all.
       - ✅ Right: product cards in the mini-mockup reuse the same CSS class and rise on hover/press just the same.
       - ❌ Wrong: the signature-move title just says "Highlighter Mark" with no explanatory paragraph.
       - ✅ Right: the title is immediately followed by 2-4 sentences explaining what the move means and how it relates to the direction.

4. **Open the preview**: use the `open` command to open `03-directions.html` in the browser.

5. **User selection**: after showing the user the four directions, guide the selection with a **two-layer structure**.

   **Layer 1: already happy with a direction?**

   If the user is basically happy with one direction, offer two ways to choose:

   - **Direct pick**: reply with a letter (A / B / C / D)
   - **Fine-grained combination**: pull specific elements from multiple directions. Combination granularity can go down to the element level:
     - Color element level: "buttons use A's accent red + background uses B's bg-page beige + cards use C's surface-card"
     - Font element level: "Display uses A's 'Bricolage Grotesque' + Body uses C's 'Noto Sans SC' + Mono uses B's 'Kode Mono'"
     - Layout element level: "Hero uses A's left-aligned big headline + product area uses B's 3-column grid + CTA uses C's dark inverted block"
     - Motion element level: "signature move uses A's hand-drawn underline + hover/press uses B's hard shadow + loading uses C's film grain"
     - Combined: "A's colors + B's typography + C's layout + D's motion"

   **Layer 2: not happy yet?**

   If no direction satisfies the user, offer two feedback modes:
   - **Reject wholesale**: "none of them, try something more ××" (e.g. "warmer", "more professional", "bolder")
   - **Partial refinement**: "A's colors are nice, but the type feels too cold — swap in a warmer font and regenerate" or "B's layout works, but the signature move is too flashy — simplify it and try again"

   **Example prompt**:

   > Open the browser to see the four directions. These are **direction drafts** for quickly experiencing the four dimensions of color, typography, layout, and motion. Once you pick one, Phase 4 will generate a more complete and realistic full-page design.
   >
   > **If you're already happy with a direction:**
   > - Just reply with a letter (A / B / C / D)
   > - Or combine elements, e.g.:
   >   - "Buttons use A's red + background uses B's beige + Display font uses C's"
   >   - "A's Hero layout + B's product grid + C's signature move"
   >
   > **If not happy yet:**
   > - Say "none of them, try something more ××"
   > - Or say "A's colors are nice, but the type is too cold — swap it and regenerate"

**Direction generation rules (must be dynamically derived — templating is forbidden)**:

- **The signature move must be perceptible**: each direction's signature move cannot be just a written label (like "highlighter mark") — it must be demonstrated with a real animation in `03-directions.html` (CSS animation, hover/press transition, scroll reveal, etc.) so the user instantly sees the direction's "memory hook".
- Signature move examples:
  - Highlighter emphasis: a hand-drawn highlight line draws itself left-to-right under the headline over 1.5s
  - Sticker aesthetic: buttons rotate slightly on hover/press and gain a hard drop shadow
  - Editorial magazine feel: images fade in with film grain on load
  - Indie bookstore: cards lift slightly on hover/press like a page corner curling up

- **Colors must be layered**: never lay all colors out flat. Must be split into:
  - **Core Palette (3-4)**: background, text, accent. This is the vibe the user perceives at first glance.
  - **UI Semantic Tokens (3-6)**: card background, border, secondary text, status colors, etc. Each must carry a role label such as `surface-card`, `border-subtle`, `text-secondary`.
  - Bad example: 7 color swatches side by side with no distinction between core and semantic.
  - Good example: first show "Background [bg-page] / Text [text-primary] / Accent [accent]", then "Card [surface-card] / Border [border-subtle] / Badge background [badge-bg]".

- **Fonts must be named**: never use sample text alone to represent a font. Real font-family, weight, and size/line-height must be written out.
  - Bad example: `Display: Find your next tool`
  - Good example: `Display: "ZCOOL XiaoWei" 600 48px/1.2`, `Body: "Noto Sans SC" 400 16px/1.6`, `Mono: "JetBrains Mono" 500 14px/1.5`

- **Mockup elements must not introduce extra hues**: placeholder elements in the Interface Mockup — product cards, images, icons — must use colors from the design system or neutrals, not highly saturated random colors (e.g. green/blue/orange cards) that steal the show.
  - Bad example: the design system's accent is red, but the mockup shows large green product cards, making the user think the direction is green-toned.
  - Good example: product cards use the `surface-card` background; image areas use low-saturation neutrals or real product images; the accent appears only on tags, prices, buttons, and other accent spots.

- **Hierarchy inside the HTML must be clearly legible**: in `03-directions.html`, each direction's section titles (Rationale / Color System — with Core Palette and UI Semantic Tokens as its sub-sections — / Typography System / Layout Pattern / Signature Move / Interface Mockup) and their content must have obvious visual hierarchy — they must not look like same-level text.
  - Bad example: titles and body text both 14-15px, same color, no spacing, no indentation — the user can't tell titles from content.
  - Good example:
    - Section titles use a larger size (≥13px and clearly bigger than body), bold weight, and the direction's accent color or a dark gray, creating contrast with body text
    - Section titles keep ≥24px spacing from the content above and 12-16px from the content below
    - Content blocks under a title use slight indentation (16-24px) or a light background for distinction
    - The Core Palette and UI Semantic Tokens sub-sections must visually read as belonging under the "Color System" parent heading

- **Every section title must carry an `i` explanation badge**: in `03-directions.html`, add an info icon (ⓘ or a lowercase i) to the right of each technical section title; hovering shows a short explanation of that section. The target users are backend engineers / non-designers — never assume they know design terminology.
  - Tooltip copy must explain both the section title and the key terms within that section (target users are backend engineers / non-designers):
    - **Rationale**: "Why this direction suits your product — analysis based on the Phase 1 product definition and Phase 2 reference vibes."
    - **Core Palette**: "The 3-4 key colors that set the page's overall vibe. bg-page = page background; text-primary = main text color; accent = highlight color for buttons, prices, and emphasis."
    - **UI Semantic Tokens**: "Color variables named by UI element role, not by the color itself. surface-card = card background; border-subtle = light border; text-secondary = secondary caption text; badge-bg = tag/badge background."
    - **Typography System**: "The font pairing this direction uses. Display = big headline font; Body = body text font; Mono = monospace font, often used for prices, code, and labels."
    - **Layout Pattern**: "How the interface's key regions are arranged. Hero = the main visual area above the fold; CTA = call-to-action button area; listing area = where the product/content list lives."
    - **Signature Move**: "The most memorable animated micro-interaction of this direction — try it with hover/click (web) or tap/press (mobile). It gives the direction a memory hook instead of a plain default animation."
    - **Interface Mockup**: "A miniature interface preview built with the real colors, fonts, and layout, so you can see what the direction actually looks like."
  - Implementation requirements: pure-CSS tooltips with no external libraries; the info badge uses the direction's accent color or gray; the tooltip background uses the direction's card background color with body text color, ensuring readability.

The four directions **must** be derived from `01-product.md` and `02-references.md` — no fixed templates (like "there's always a midnight/dark/industrial direction"). The derivation logic:

1. **Read Phase 1 to determine the core tension**
   - Product type + target users → determines each direction's "category plausibility"
   - Mood/atmosphere keywords → determines each direction's "temperament keynote"
   - Key differentiator → determines each direction's "differentiated memory hook"
   - Conversion goal → determines each direction's "functional emphasis"

2. **Read Phase 2 to determine the aesthetic boundaries**
   - **Explicit preferences are hard constraints**: the user's verbatim statements in the "Explicit Preferences" section of `02-references.md` (e.g. "no red, blue, purple, or gradients; use serif fonts") must be decomposed and executed item by item — banned colors must not appear in any direction; mandated colors must appear at least in the safe direction and the reference-close direction; font preferences (e.g. serif-leaning) directly affect each direction's font selection
   - Vibes the user explicitly liked → at least one direction leans toward them
   - Elements the user explicitly rejected → all directions avoid them
   - Overall impressions of the references → determine the "familiarity vs breakthrough" ratio across directions

3. **Generate directions in four roles**
   - **Safe direction**: based on the user's expressed preferences; low risk, quick to land
   - **Bold direction**: a visual breakthrough built on the key differentiator; strong memory hook; reactions may be polarized
   - **Reference-close direction**: closest to the Phase 2 reference vibes
   - **Counter direction**: contrasts with the mainstream reference vibe, helping the user confirm their boundaries

4. **Layout diversity between directions (hard requirement)**: the four roles must differ in layout, not only in color and typography:
   - The four Layout Patterns must contain at least **2 structurally different layouts** — different region composition or information hierarchy, not the same skeleton in different colors. For the same homepage, one direction could use centered Hero + product grid, another sidebar nav + dense data band, another an editorial magazine-style arrangement.
   - The Bold direction's breakthrough must include layout, not just color: if its structure is identical to the Safe direction's, it is not bold.
   - Anti-pattern: ❌ all four directions share one layout skeleton (same nav / hero / grid arrangement) and differ only in palette or font = this is one direction wearing four skins; regenerate until the layouts genuinely differ.

5. **Direction naming rules**
   - Names must come from the direction's real design language, not a fixed word bank.
   - Good name examples: "Workbench White" (warm white base + deep teal + tidy shelf feel), "Clay Shelf" (warm beige base + ochre + handmade warmth).
   - Bad name examples: "Modern Minimal Version", "Dark Premium Version", "Default Option" — these are descriptions, not directions.

**Bad example**: no matter what the product is, generating "Midnight Warehouse / dark / industrial" as the bold direction.
**Good example**: if the product is "creators selling digital goods", the bold direction could be "Clay Shelf" (warm beige base + ochre + handmade warmth) or "Paper Catalog" (magazine-layout feel), depending on the Phase 1/2 inputs.

**Output**: `design/03-directions.html`

**Approval gate**: the user explicitly picks a direction, or gives a combination instruction.

---

## Phase 4: First Screen(s) Preview Loop

**Goal**: turn the chosen direction into a real design mockup of the first key interface(s), iterating until the user is satisfied.

**What the first screen(s) are is decided by Phase 1**: the 1–2 screens confirmed at the end of Phase 1 are the first screen(s). This could be a single homepage/dashboard/landing/core feature page, or a tightly coupled pair such as chat list + chat detail, storefront + product detail, or card feed + profile. Never assume it must be a "homepage", and never add a second screen that was not confirmed in Phase 1.

**Before generating v1, verify the key screen(s) with the user**: briefly restate the screen(s) recorded in `design/state.md` and ask the user to confirm that the persisted selection is still correct:

> In Phase 3 and Phase 4 we'll focus on the key screen(s) confirmed in Phase 1: **<screen A>**{** and <screen B>**}. I'll produce a first mockup for {**this screen** / **these two screens together**}. Does this persisted screen selection still look right? If you want different screen(s), we'll return to the Phase 1 screen-selection handoff before generating the Phase 4 preview. You can pick **one screen** or **two screens at most**.
>
> Once these first screen(s) are locked, Phase 5 will expand the same direction into the other core screens.

If the user requests different screen(s), do not generate a Phase 4 preview from the new selection. Return to the Phase 1 screen-selection handoff, obtain explicit confirmation, update both `design/state.md` and `01-product.md`, and regenerate `03-directions.html`. The regenerated directions file shows mockups of the new screen set, so the earlier direction choice no longer applies: ask the user to pick a direction again per the Phase 3 approval gate, and only then re-enter Phase 4. This keeps the Phase 3 direction and Phase 4 preview based on the same persisted screen set.

**Key requirements**:
- **Keep `impeccable` sub-skills as the primary constraint layer**; if unavailable, fall back to `frontend-design` or the built-in fallback rules
- Optionally load `typeset`, `layout`, `delight` to fine-tune details
- Every iteration generates a new version file (v1, v2, v3...) — never overwrite old versions
- Use real data, no Lorem Ipsum

**How to run**:

1. **Generate v1**:
   - If **1 Key Screen** was confirmed: create `design/04-<screen>-v1.html` (`<screen>` is the interface name, e.g. `home` / `dashboard` / `landing`).
   - If **2 Key Screens** were confirmed: create `design/04-<screen1>-<screen2>-v1.html` showing both screens together (side by side on desktop, stacked or tab-switchable on mobile). Each screen gets enough content to judge the layout, but the file is a single preview so the user can evaluate continuity between the two screens.
   - **Canvas must match the recorded device form factor**: phone products render each interface inside a portrait phone-shaped frame at realistic phone proportions; tablet products use a tablet-shaped frame; web/desktop products render at landscape, desktop-like proportions. Never stretch a phone interface across a full desktop-width canvas or render it in a tablet frame — the preview must look like the real device.
   - Which sections each interface contains is dynamically derived by the agent from the Phase 1 product definition and the Phase 3 chosen direction's Layout Pattern — not a fixed template:
     - Judgment principle: what action does the user open this interface to complete? Which sections support that action?
     - Take a digital-goods platform homepage: Nav, Hero, product listing, category/search entries, CTA, and Footer are usually necessary; but for a dashboard it might be sidebar + data cards + chart area; for a single-page portfolio, maybe just Nav, Hero, work grid, Footer
     - Real data (real product names, real prices, real descriptions)
     - Complete interaction states appropriate to the platform (web: hover/active/focus; mobile: tap/press/active)
     - Colors/typography/layout matching the chosen direction

2. **Open the preview**: `open design/04-<screen>-v1.html` {or `open design/04-<screen1>-<screen2>-v1.html`}

3. **User feedback loop**:
   - User says "looks good" → generate `DESIGN.draft.md`, then enter the fork decision (see step 5)
   - User says "change X" → generate v2, changing only X and keeping everything else
   - User says "wrong direction" → go back to Phase 3 and record the rejection reason

4. **Generate DESIGN.draft.md**: as soon as the first screen(s) are approved by the user, extract the design decisions from the final HTML version and generate `design/DESIGN.draft.md`:
   - **Structure must be isomorphic with the final DESIGN.md** (use the ten-chapter skeleton defined in Phase 7) — only the content is extracted from the first screen(s) first and marked as draft
   - Core Palette, UI Semantic Tokens
   - Typography system (font-family, weight, size, line-height)
   - Layout patterns, spacing, corner radii
   - The implemented signature move and base motion
   - UX decisions (the approved first screen(s)' platform-appropriate interaction states, loading/empty/error states, etc.)
   - Marked as "draft"; Phase 5 will keep updating it and Phase 6 will record validated polish decisions

5. **Fork decision (agent proactively suggests, user decides)**: after the first screen(s) are approved and the draft is generated, the agent proactively suggests the next step based on the product type and waits for the user's confirmation:

   > The first screen(s) are approved and DESIGN.draft.md is generated. There are three paths from here:
   > - **Phase 5 Core Screen Expansion**: if the product has other core interfaces, extend the approved direction into the smallest screen set that validates the key user paths
   > - **Phase 6 Cross-Screen Polish**: if this is a single-page product, or the user wants to refine an existing screen directly, run the relevant dimension-by-dimension polish passes
   > - **Phase 7, finalize DESIGN.md directly**: if the user only needs the approved interface(s) and no further polish is required, produce the final design-system document right away
   >
   > Suggestion: <the agent suggests based on the Phase 1 product definition>
   > Which path do you want? (Combinations are fine too, e.g. "5 first, then 6")

**Iteration rules**:
- Each iteration changes only what the user explicitly mentioned
- If 2 screens are shown together and the user only comments on one, regenerate only the affected screen's content inside the same preview file; do not silently redesign the second screen
- Never proactively introduce new elements
- Keep already-locked elements unchanged

**Output**: `design/04-<screen>-v*.html` {or `design/04-<screen1>-<screen2>-v*.html`} + `design/DESIGN.draft.md`

**Approval gate**: the user explicitly says "looks good", "that works", or "ship it" for the first screen(s), and `DESIGN.draft.md` has been generated.

---

## Phase 5: Core Screen Expansion

**Goal**: extend the approved first-screen(s) direction into the smallest set of core screens needed to validate the product's design system and key user paths. This phase is constrained expansion, not a new direction round.

**When to run**: after Phase 4 for any multi-page or multi-state product. Single-page projects may skip Phase 5 entirely and proceed directly to Phase 7.

**Core screen set**:
- Derive the target list from the product definition and the user's actual paths, not from a fixed sitemap template.
- Prefer 3–5 screens in the first batch. A digital-goods platform commonly needs a storefront, product detail, search/category, checkout, and purchase/download screen; add creator screens only when the creator workflow is in scope.
- Choose screens that cover different design pressures: expressive/brand-heavy, information-dense, transactional, and state-heavy.
- Do not generate every secondary page before the core system is validated.

**Key requirements**:
- Use `DESIGN.draft.md` as the active source. Do not silently create a second color, typography, radius, button, or motion system.
- Use real data and realistic content. Each page must include the states relevant to its role, including default, loading, empty, error, and important interaction states.
- Produce an implementation-oriented contract for each page: route, framework, reused/extended/new components, state matrix, data dependencies, accessibility requirements, and integration risks.
- Maintain a screen map and component inventory before generating the full set.
- If a screen exposes a cross-product design problem, update `DESIGN.draft.md` first, then re-apply the decision to the affected screens.
- Page-specific exceptions must be recorded as `Surface` rules; never hide them only in HTML/CSS.

**How to run**:

1. **Confirm the core screen set**: present the proposed screens and the user path they cover. Ask for a correction only if the product scope is ambiguous.
2. **Generate v1 for the set**: create `design/05-<screen>-v1.html` for each core screen. The first pass should be medium fidelity: realistic structure, content, components, states, and responsive intent, without exhaustive pixel polishing. Every screen keeps the Phase 4 canvas rule: phone products render inside portrait phone frames, tablet products in tablet frames, web/desktop at desktop proportions.
3. **User feedback loop on the whole set**:
   - Present the complete set to the user and ask: "Does this direction feel right across all screens?"
   - User says "looks good" → proceed to the fork decision below
   - User says "change X" → generate v2 for the affected screens (or all screens if X is global), changing only X
   - User says "replace screen Y with Z" or "remove screen Y" → adjust the core screen set and regenerate the affected screens
   - User says "wrong direction" → ask whether to adjust the current set or go back to Phase 4 / Phase 3; only go back when the user explicitly confirms the direction itself is wrong
4. **Iterate the set**: repeat step 3 until the user is satisfied with the overall direction and screen composition. If a change is global, update `DESIGN.draft.md` and propagate it. If it is local, update only the affected screen contract and record why.

**Exploration Mode**:
- Use it when the user requests alternatives for a screen or component.
- Keep alternatives within the selected direction and active design source.
- Compare structural differences, use cases, tradeoffs, and implementation impact. Do not create cosmetic duplicates that only change color.

**Output**:
- `design/05-<screen>-v*.html`
- `design/05-screen-map-v*.md`
- `design/component-inventory.md`
- `design/05-<target>-implementation-v*.md`
- updated `design/DESIGN.draft.md`

**Versioning rule**: every iteration bumps the version number for affected screen files, the screen map, and any implementation contract that changed. Never overwrite old versions, so the user can always compare v1, v2, v3, etc.

**Approval gate**: the user approves the overall direction of the core screen set, and every screen has an implementation contract and a current state matrix.

**Fork decision after approval**: once the user is satisfied with the core screen set, the agent proactively asks:

> The core screens are approved. From here:
> - **Phase 6 Cross-Screen Polish**: if you want detailed refinement on typography, spacing, components, responsiveness, or motion
> - **Phase 7, finalize DESIGN.md directly**: if the current fidelity is sufficient and no further polish is needed
>
> Which path do you want?

---

## Phase 6: Cross-Screen Polish

**Goal**: polish the first screen(s) and the Phase 5 core screens as one system, dimension by dimension. This phase is **optional** — it turns a plausible collection of screens into a coherent, accessible, production-ready interface family. If the user is already satisfied after Phase 5, skip directly to Phase 7.

**Phase 6 modes**:
- **Screen Mode**: for a narrow refinement of one existing screen; run only the relevant passes.
- **Core Set Mode**: for a new multi-screen product; run the passes across all core screens.
- **Extension Mode**: after Phase 7, apply the active canonical design source to a new screen or component, then run the relevant passes before approval.

**Pass order** (all passes are optional — the agent must confirm with the user which passes to run, and in what order):

1. **Content & Structure** — hierarchy, conversion path, navigation, content priority, labels, CTA intent, empty/error copy, and task clarity. Load `clarify` when available.
2. **Visual System** — typography (type scale, line-height, letter-spacing), color tokens, spacing rhythm, surfaces, borders, shadows, and visual continuity. Load `typeset`, `colorize`, and `layout` when available.
3. **Components & States** — reuse/extend/new decisions; platform-appropriate interaction states (web: hover/active/focus-visible; mobile: tap/press/active), disabled, loading, empty, error, and domain-specific states. Load `harden` when relevant.
4. **Responsive & Access** — representative widths, focus/keyboard access (web), touch targets (mobile), contrast, reduced motion, image loading, overflow, and layout stability. Load `adapt` and `audit` when relevant.
5. **Motion** — purposeful entrance, hover/press, feedback, and transition behavior; easing and duration tokens; reduced-motion fallback. Load `animate` and `audit` when relevant.

**Platform-driven pass order**:
- **Mobile-first products**: Responsive & Access should run early (often right after Visual System), or its checks should be folded into every pass rather than treated as a separate late-stage pass.
- **Desktop-only products**: Responsive & Access may run later, or be simplified.
- **Single-page products**: Content & Structure and Motion are usually sufficient; the remaining passes may be skipped.
- **Every pass is skippable**: if the user says "skip X" or "we'll handle X ourselves", record it in `06-polish-log.md` and move on.

**Global pass vs. surface pass**:
- Apply global token and component changes first, then verify every core screen.
- Apply page-specific exceptions only after the global pass, and record them as `Surface` rules.
- Do not let one page's local polish silently become a global design decision.

**How to run**:

1. Create or update `design/06-polish-log.md` before the first pass. Each entry records the pass, allowed scope, forbidden scope, changed files, acceptance criteria, and user feedback.
2. Run one dimension at a time. Do not ask the agent to fix typography, spacing, color, copy, and motion in one unconstrained request.
3. After each pass, generate new polished versions of affected screens as `design/06-<screen>-v*.html`. Never overwrite the original `04-*` or `05-*` files — they remain as milestones.
4. Update `DESIGN.draft.md` if the decision is global, and re-check the full core screen set.
5. A standalone `design/06-<dimension>-review.html` is optional when the dimension needs an interactive comparison, such as motion or responsive behavior.
6. Before moving to Phase 7, do a final cross-screen review: confirm visual hierarchy and primary actions are clear, shared components use the active tokens and state matrix, and no unresolved high-severity drift findings remain.

**Output**: `design/06-<screen>-v*.html` polished previews + `design/06-polish-log.md` + optional dimension review pages + updated `design/DESIGN.draft.md`

**Approval gate**: the user approves the polished core screen set, the selected passes have been recorded in `06-polish-log.md`, and the active design source contains the decisions that must survive into Phase 7.

---

## Phase 7: Design System (generating DESIGN.md)

**Goal**: solidify `DESIGN.draft.md` into the final, reusable DESIGN.md.

**Key requirements**:
- **Use `DESIGN.draft.md` as the input** — do not re-extract from HTML
- If Phase 5 / Phase 6 updated the draft, all updates must be merged
- DESIGN.md's structure must **fuse three parts**:
  1. **The google-labs-code/design.md spec** (official spec): Visual Theme / Color / Typography / Components / Layout / Depth / Do's and Don'ts / Responsive / Agent Prompt Guide
  2. **UX constraints (required, not optional)**: Phase 4, Phase 5, and Phase 6 are themselves about fixing UX — the first screen(s)' interaction states, the core-screen default/loading/empty/error states, and the cross-screen polish decisions are all UX decisions. These must be written back into DESIGN.md, including: interaction patterns, state feedback, empty states, loading states, error handling, navigation logic. If Phase 5/6 ran but the UX chapter is missing, the draft updates are incomplete and must be filled in.
  3. **Spec-driven constraints** (team engineering-practice supplement): cross-page consistency rules, component-reuse constraints, tech-stack bindings, acceptance criteria
- Also generate tokens.css and the necessary assets

**How to run**:

1. **Read DESIGN.draft.md**: confirm the draft already contains all approved design decisions:
   - Core Palette, UI Semantic Tokens
   - Typography system
   - Layout patterns, spacing, corner radii
   - Motion system (if Phase 6 ran)
   - Multi-screen component specs (if Phase 5 ran)
   - UX feedback and state rules (if Phase 5 / Phase 6 ran)

2. **Generate the final DESIGN.md**: use `templates/DESIGN-template.md` as the skeleton (ten-chapter structure + optional extensions), filling in the actual decisions from `DESIGN.draft.md`. **All visible text in DESIGN.md — chapter titles, section headings, table headers, field labels, explanatory paragraphs, and example prompts — must be written in the user's language.** Only code identifiers (CSS custom property names, token names, font family names, file paths) stay in English. Do not ship a Chinese product with a DESIGN.md whose headings are still in English.

   **Chapter add/remove principles**:
   - **Required chapters** (cannot be removed): Design Soul, Tokens, Components, UX Constraints, Do's and Don'ts, Agent Prompt Guide
   - **Chapters added/removed per product**:
     - Surfaces & Elevation: if the product has no explicit layering strategy (e.g. pure flat design), may be merged into Layout
     - Imagery & Layout: if the product has no illustration/imagery needs, may be simplified or removed
     - Responsive Behavior: if the product is desktop-only, may be simplified
     - Spec-driven Constraints: if the team has no engineering-constraint needs, may be removed
     - Motion & Transitions: if the Phase 6 motion pass didn't run, don't force-write a motion chapter
   - **Optional extensions**: Gradient System, Color/Typography/Radius Philosophy, Similar Brands, etc. — add only when the product needs them

   Chapter structure:

   **1. Design Soul (header)**
   - Brand name + one evocative sentence describing the style
   - Overview prose: overall temperament, color strategy, typography-role philosophy

   **2. Tokens (base rules)**
   - **Color Palette & Roles**: color token table, four columns: Name | Value (#hex) | Token name | Role. Role must explain "where it's used and why" (e.g. "text emphasis only; forbidden as button background")
   - **Typography Rules**: for each font, write out Substitute, weight, size, line-height, letter-spacing, OpenType features, and role. Plus a Type Scale table (role → size/line-height/spacing/token)
   - **Spacing & Shapes**: base unit, density, Spacing scale table, Border Radius table (per element), Shadows table, Layout (page max-width, section gaps, card padding)

   **3. Components (component specs)**
   - Describe each component: Role + full visual spec (background, text color, radius, padding, font and size, hover/press state, transition animation)
   - Cover at least: buttons, cards, nav bar, footer, inputs, tags, price display, empty-state component

   **4. UX Constraints (Interaction Rules, required chapter)**
   - **Source**: all interaction decisions approved by the user during Phase 4 first-screen(s) iteration, Phase 5 core-screen expansion, and Phase 6 polish
   - Interaction patterns for filter/search/sort
   - State feedback rules appropriate to the platform (web: hover/active/focus/disabled/loading; mobile: tap/press/active/disabled/loading)
   - Presentation specs for empty, loading, and error states (every core screen in Phase 5 designed these states)
   - Navigation logic and information architecture
   - Form validation and error message styles
   - Accessibility baseline appropriate to the platform (web: contrast, focus visibility, keyboard navigation; mobile: contrast, touch-target size, screen-reader labels)
   - **Note**: this chapter is not an "optional extension" — it is the direct solidification of Phase 4/6 work. If it's missing, the DESIGN.md is considered incomplete.

   **5. Do's and Don'ts (red-line rules)**
   - Do gives conventions; Don't gives bans
   - Must include AI-slop bans (e.g. "no Inter/DM Sans", "no gradient text", "no identical 3-card feature rows")
   - Must include brand-specific bans (e.g. "the accent color must not be used for large-area fills", "don't bold headlines")

   **6. Surfaces & Elevation**
   - Surfaces table: level 0/1/2/3 → color → usage (canvas/cards/inverted surface)
   - Elevation: shadow strategy (even explicitly "no shadows — layer by tone instead")

   **7. Imagery & Layout**
   - Imagery style (photography/illustration/logo walls/banned items)
   - Page skeleton (nav height, hero layout, column ratios, vertical rhythm)

   **8. Responsive Behavior**
   - Breakpoint rules
   - Mobile layout adjustment strategy
   - Minimum touch-target sizes

   **9. Spec-driven Constraints (optional, recommended)**
   - Cross-page consistency rules (e.g. "card radius is uniformly 12px on all pages")
   - Component-reuse constraints (e.g. "product cards must use the `<ProductCard />` component; no re-implementation")
   - Tech-stack bindings (e.g. "Tailwind CSS; colors must be referenced through CSS variables")
   - Acceptance criteria (e.g. "any new page must pass the `impeccable` / `frontend-design` constraint check")

   **10. Agent Prompt Guide (usage guide for agents)**
   - Quick Color Reference (cheat sheet)
   - Example Component Prompts: copy-paste-ready prompt examples for generating components
   - Common mistakes and how to fix them

   **Optional extensions** (vary by product):
   - Gradient System
   - Motion & Transitions (if the Phase 6 motion pass ran, this must be expanded in detail here)
   - Color/Typography/Radius Philosophy
   - Similar Brands: list brands with a similar style as reference

3. **Generate tokens.css**: CSS custom properties, ready to use in the project.

4. **Generate assets**: if there are logos, icons, etc., save them to `design/assets/`.

5. **Update AGENTS.md**: add a design-system reference note to the project root's AGENTS.md. For the normal flow, reference files inside `design/`. For existing-system mode, reference the active canonical source recorded in `design/state.md` and do not move an existing source merely to satisfy this example. Example for a newly generated design system:

   ```markdown
   ## Design System

   This project's design system was produced by the zero-to-design workflow. Before adding pages, components, or visual changes, read:

   - `design/DESIGN.md` — full design-system documentation (Tokens, Components, UX constraints, motion specs, etc.)
   - `design/tokens.css` — ready-to-use CSS custom properties

   All visual decisions (colors / typography / radii / shadows / motion / interactions) may only use the tokens and component specs in the active canonical design source. Do not invent your own colors or introduce visual language outside the spec.
   ```

6. **Clean up the draft**: after DESIGN.md is approved by the user, rename `DESIGN.draft.md` to `DESIGN.draft.md.bak` or delete it (user's choice) to avoid later confusion.

**Output file structure for the normal flow**:

```
design/
├── 01-product.md
├── 02-references.md
├── 03-directions.html
├── 04-<screen>-v1.html          (or 04-<screen1>-<screen2>-v1.html if 2 Key Screens)
├── 04-<screen>-v2.html          (or 04-<screen1>-<screen2>-v2.html)
├── ...
├── 05-<screen>-v*.html          (core screen expansion)
├── 05-screen-map-v*.md          (core screen map and user paths)
├── component-inventory.md       (shared component and state inventory)
├── 05-<target>-implementation-v*.md (implementation contract)
├── 06-polish-log.md             (dimension-by-dimension polish record)
├── 06-<screen>-v*.html          (polished previews; original 04/05 files stay untouched)
├── 06-<dimension>-review.html   (optional dimension review)
├── existing-system.md           (if existing-system intake ran)
├── DESIGN.md
├── tokens.css
└── assets/
    └── (logo, icons, etc.)
```

**Approval gate**: the user confirms DESIGN.md is complete and accurate, and consistent with the feedback from Phase 5 / Phase 6.

---

## State Management

Maintain `design/state.md` in the project root, recording:

```markdown
# zero-to-design State

## Current Phase
<current phase>

## Key Screens (locked in Phase 1, 1–2 screens)
- <screen A>
- <screen B> (optional — only when two tightly-coupled screens were confirmed)

## Platform (locked in Phase 1)
<Web / iOS / Android / Desktop> · form factor: <phone / tablet / desktop — required for iOS / Android>

## Entry Mode
<new-product / existing-system / extension>

## Phase 5 Mode
<core-set / extension / not-applicable>

## Phase 6 Mode
<screen / core-set / extension / not-applicable>

## Polish Pass
<current dimension / pending>

## Candidate Decisions
- <target>: <selected candidate or pending>
- Rejected candidates: <candidate → reason>

## Design System Source
- Canonical source: <path or "generated observed baseline">
- Source status: <validated / partially validated / generated from exploration>
- Existing-system intake: <not applicable / pending / complete>

## Decisions Locked
- Direction: <chosen direction name>
- Primary color: <hex>
- Fonts: <display/body>
- <other locked items>

## Design Constraints (constraint mode chosen in Phase 3)
- Primary constraint skill: <impeccable / frontend-design / built-in fallback / other>
- Additional skills: <bolder, shape, critique, etc., or "none">
- Chosen at: <date at the start of Phase 3>
- Notes: <special user requests, e.g. "built-in rules only", "prefer bold directions">

## Rejected Directions
- <direction name>: <rejection reason (user's exact words)>

## Open Questions
- <question list>

## File Checklist
- [ ] existing-system.md
- [x] 01-product.md
- [x] 02-references.md
- [x] 03-directions.html
- [ ] 04-<screen>-v1.html (or 04-<screen1>-<screen2>-v1.html if 2 Key Screens)
- [ ] DESIGN.draft.md
- [ ] 05-<screen>-v*.html
- [ ] 05-screen-map-v*.md
- [ ] component-inventory.md
- [ ] 05-<target>-implementation-v*.md
- [ ] 06-polish-log.md
- [ ] 06-<screen>-v*.html
- [ ] 06-<dimension>-review.html
- [ ] DESIGN.md
```

Update `design/state.md` after each Phase completes, after the active polish dimension changes, and after every Phase 5/6 candidate selection.

---

## Relationship with Existing Tools

- **Open Design**: this skill can serve as the upstream process for Open Design. First use zero-to-design to complete the direction and DESIGN.md, then import DESIGN.md into Open Design for subsequent pages.
- **impeccable / frontend-design**: this skill's Phases 3, 4, 5, 6, and 7 depend on them as the constraint layer against AI slop. `impeccable` sub-skills are the preferred primary constraint layer; `frontend-design` is a solid fallback when `impeccable` is unavailable.
- **Positioning**: this skill is a lightweight, single-session, single-agent design workflow emphasizing "conversational guidance + files on disk + continuously evolving DESIGN.md". It suits individual developers or small teams building a design system from 0 to 1 quickly.

## Failure Handling

- If the user rejects all directions in Phase 3: go back to Phase 2, re-collect references, or adjust the product definition.
- If the user is still unsatisfied after multiple Phase 4 iterations: iterate at most 5 times, then suggest going back to Phase 3 to switch directions.
- If Phase 5 exposes a conflict between core screens: update `DESIGN.draft.md`, record the conflict in the screen map, and regenerate only the affected screens before continuing.
- If the user is unsatisfied with a Phase 6 dimension pass: iterate that dimension across the affected screen set; if the issue is global, update the active canonical design source and re-apply it to every screen.
- If the user is unsatisfied with an extension-mode page or component: iterate only that target; if cross-page or cross-component specs are involved, update the active canonical design source and re-apply it to subsequent targets.
- If file generation fails at any stage: check whether the `impeccable` sub-skills loaded correctly, or whether `frontend-design` is being used as the fallback, and check file-path permissions.

## Completion Criteria

When `DESIGN.md` is generated and approved by the user, mark `status: complete` in `design/state.md` and tell the user:

> Design bootcamp complete. All outputs live in the `design/` directory:
> 1. Product definition (01-product.md)
> 2. Reference collection (02-references.md)
> 3. Design direction selection (03-directions.html)
> 4. First-screen(s) mockups (04-<screen>-v*.html, or 04-<screen1>-<screen2>-v*.html if 2 Key Screens)
> 5. Core screen expansion (05-<screen>-v*.html + 05-screen-map-v*.md + 05-<target>-implementation-v*.md + component-inventory.md)
> 6. Cross-screen polish (06-<screen>-v*.html + 06-polish-log.md + optional dimension review pages)
> 7. Extension-mode screen/component mockups (06-<screen>-v*.html / 06-<component>-v*.html, if they ran)
> 8. Design-system documentation (DESIGN.md + tokens.css + assets/)
> 9. AGENTS.md — a "Design System" section has been added, referencing the active canonical design source and tokens, so agents in future sessions will automatically read these constraints
> 10. DESIGN.draft.md.bak — backup of the original draft (if you chose to keep it)
>
> **Note**: In the normal flow, generated `DESIGN.md` and `tokens.css` stay inside the `design/` directory. In existing-system mode, preserve the project's existing canonical source location and reference it from `design/state.md`.
>
> All future page development should follow the constraints in the active canonical design source (already linked in AGENTS.md, so agents will read it automatically).
