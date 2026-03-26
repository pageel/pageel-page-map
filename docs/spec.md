# Page Map Format Specification

> **Project**: pageel-page-map
> **Version**: 2.0.0
> **Updated**: 2026-03-26

This document defines the standard formats for `PAGE_MAP.md`, `BLUEPRINT.md`, and `INDEX.md`, as well as naming conventions for structural layout mapping.

---

## 1. Naming Convention

Layout elements follow a hierarchical format enclosed in square brackets: `[Section.Subsection]`.

- **Format**: `[<major-section>.<minor-section>]`
- **Page maps**: `[page.section]` — e.g., `[index.hero]`, `[features.pricing]`
- **Component maps**: `[Component.Section]` — e.g., `[Hero.TechStackHeader]`, `[Calculator.ResultCard]`
- **Purpose**: Ensure consistent identification of layout zones across diagrams and source code.

## 2. Inline Tag Format

Within source code (e.g., `.astro`, `.jsx`, `.tsx`), each code block corresponding to a layout zone MUST be marked with a comment so that automation tools or AI can map it to `BLUEPRINT.md`.

- **Format**: `{/* [Section.Subsection] */}`
- **Example in Astro/JSX**:
  ```astro
  {/* [hero.title] */}
  <h1 class="text-3xl font-bold">Welcome to the ecosystem</h1>
  ```

## 3. `PAGE_MAP.md` Specification

- **Role**: Provides a high-level visual wireframe of a page or component structure. It acts as a stable anchor for human understanding and AI agent context.
- **Format Requirements**:
  - File MUST be named `PAGE_MAP.md`.
  - Use ASCII art or Markdown blocks for visual layout representation.
  - Every section shown in the visual mapping MUST include an identifier tag conforming to the naming convention: `[Section.Subsection]`.
  - For page-level maps, include cross-reference arrows to component maps: `[index.hero] → components/Hero/`
  - For component-level maps, visualize the internal HTML structure zones, not just a placeholder box.

## 4. `BLUEPRINT.md` Specification

- **Role**: Technical architecture map connecting the spatial structure (from `PAGE_MAP.md`) to the actual implemented components/files. This enables swappable components and scalable management.
- **Format Requirements**:
  - File MUST be named `BLUEPRINT.md`.
  - MUST use Markdown tables.
  - **Required Columns (page-level)**:
    1. **Section**: The tag based on the naming convention (e.g. `[index.hero]`).
    2. **Source**: The actual source file or component used (e.g. `src/components/Hero.astro`).
    3. **Hydration**: Framework directive — `client:load`, `client:visible`, `client:idle`, or `Static`.
    4. **Component Map**: Relative link to the component's `PAGE_MAP.md`, or `—` for inline sections.
  - **Required Columns (component-level)**:
    1. **Section**: The tag (e.g. `[Hero.Title]`).
    2. **Element**: HTML element or sub-component (e.g. `<h1>`, `<div.grid>`).
    3. **Props / Data**: Input parameters or data sources.
    4. **Notes**: Optional context or implementation notes.

## 5. Storage Convention

PAGE_MAP and BLUEPRINT files MUST be stored in a `.pageel/page-maps/` directory at the repository root, organized by type.

- **Pages** → `.pageel/page-maps/pages/<page-name>/`
- **Components** → `.pageel/page-maps/components/<ComponentName>/`
- **Site Index** → `.pageel/page-maps/INDEX.md`

**Naming rules:**
- Page directory names use **lowercase** matching the route slug (e.g., `index`, `features`, `contact`).
- Component directory names use **PascalCase** matching the component filename (e.g., `Hero`, `FeatureGrid`, `Calculator`).

**Directory structure:**
```
repo/
├── .pageel/
│   └── page-maps/
│       ├── INDEX.md           ← Site-wide coverage tracker
│       ├── pages/
│       │   ├── index/
│       │   │   ├── PAGE_MAP.md
│       │   │   └── BLUEPRINT.md
│       │   └── features/
│       │       ├── PAGE_MAP.md
│       │       └── BLUEPRINT.md
│       └── components/
│           ├── Hero/
│           │   ├── PAGE_MAP.md
│           │   └── BLUEPRINT.md
│           └── Navbar/
│               ├── PAGE_MAP.md
│               └── BLUEPRINT.md
├── .pageelrc.json       ← CMS config (if using pageel-cms)
└── src/
```

**Discovery**: AI agents SHOULD search `.pageel/page-maps/` first when looking for page structure information.

## 6. `INDEX.md` Specification

- **Role**: Site-wide coverage map tracking which pages and components have been mapped.
- **Location**: `.pageel/page-maps/INDEX.md`
- **Format Requirements**:
  - Separate tables for **Pages** and **Components**.
  - Components table includes a **Used by** column listing pages that use the component.
  - Each table ends with a **progress bar** using `█` (filled) and `░` (empty), total 20 characters.
  - Formula: `filled = round(mapped / total * 20)`, remainder is `░`. Followed by `X/Y (Z%)`.
- **Status icons**:
  - `✅ Mapped` — PAGE_MAP.md + BLUEPRINT.md completed.
  - `⬜ Pending` — Map not yet created.
  - `⏭️ Skip` — Utility component with no visual structure (e.g., SEO head tags, image optimizers).
- **Shared components**: A component needs only one map at `components/<Name>/`. Page BLUEPRINTs link to it — no duplicates.

## 7. Cross-Referencing

Page maps and component maps MUST be linked bidirectionally:

- **Page → Component**: In the page's `PAGE_MAP.md`, add arrow notation: `[index.hero] → components/Hero/`. In the page's `BLUEPRINT.md`, add a **Component Map** column linking to the component's `PAGE_MAP.md`.
- **Component → Page**: The `INDEX.md` **Used by** column tracks which pages use each component.

This ensures agents can navigate between abstraction layers without guessing.

## 8. Additional Inline Tag Formats

While `{/* */}` is the standard for JSX/Astro, other frameworks use different comment syntax:

| Framework       | Inline Tag Format                     | Example                                |
| :-------------- | :------------------------------------ | :------------------------------------- |
| Astro / JSX     | `{/* [section.tag] */}`               | `{/* [hero.title] */}`                 |
| HTML            | `<!-- [section.tag] -->`              | `<!-- [hero.title] -->`                |
| Vue (template)  | `<!-- [section.tag] -->`              | `<!-- [hero.title] -->`                |
| Svelte          | `<!-- [section.tag] -->`              | `<!-- [hero.title] -->`                |
| PHP             | `<?php /* [section.tag] */ ?>`        | `<?php /* [hero.title] */ ?>`          |

The key rule: the tag `[section.tag]` is always wrapped in the closest available comment syntax.

## 9. Migration from v1.x to v2.0

Users upgrading from v1.x (flat directory structure) should:

1. **Create subdirectories**: Add `pages/` and `components/` inside `.pageel/page-maps/`.
2. **Move page maps**: Move each `<page-name>/` folder into `pages/<page-name>/`.
3. **Create component maps**: For each reusable component, create a new directory under `components/<ComponentName>/` with its own `PAGE_MAP.md` and `BLUEPRINT.md`.
4. **Update BLUEPRINTs**: Add `Hydration` and `Component Map` columns to all page-level BLUEPRINTs.
5. **Create INDEX.md**: Add `INDEX.md` at `.pageel/page-maps/` root to track coverage.
6. **Update SKILL.md**: Replace the v1.x SKILL.md with the v2.0 version.
