# Page Map Format Specification

> **Project**: pageel-page-map
> **Version**: 1.0.0
> **Updated**: 2026-03-19

This document defines the standard formats for `PAGE_MAP.md` and `BLUEPRINT.md`, as well as naming conventions for structural layout mapping.

---

## 1. Naming Convention
Layout elements follow a hierarchical format enclosed in square brackets: `[section.subsection]`.
- **Format**: `[<major-section>.<minor-section>]`
- **Examples**: `[hero.title]`, `[content.sidebar]`, `[footer.links]`
- **Purpose**: Ensure consistent identification of page sections across layout diagrams and source code.

## 2. Inline Tag Format
Within source code (e.g., `.astro`, `.jsx`), each code block corresponding to a layout block MUST be marked with a comment so that automation tools or AI can map it to `BLUEPRINT.md`.
- **Format**: `{/* [section.subsection] */}`
- **Example in Astro/JSX**:
  ```astro
  {/* [hero.title] */}
  <h1 class="text-3xl font-bold">Welcome to the ecosystem</h1>
  ```

## 3. `PAGE_MAP.md` Specification
- **Role**: Provides a high-level visual wireframe of an application/page structure layer. It acts as a stable anchor for human understanding and AI system context.
- **Format Requirements**:
  - File MUST be named `PAGE_MAP.md`.
  - Encouraged to use ASCII art or Markdown blocks for visual layout representation.
  - Every section shown in the visual mapping MUST include an identifier tag conforming to the naming convention: `[section.subsection]`.

## 4. `BLUEPRINT.md` Specification
- **Role**: Technical architecture map connecting the spatial structure (from `PAGE_MAP.md`) to the actual implemented components/files. This enables swappable components and scalable management.
- **Format Requirements**:
  - File MUST be named `BLUEPRINT.md`.
  - MUST use Markdown tables.
  - **Recommended Columns**:
    1. **Section**: The tag based on the naming convention (e.g. `[hero.title]`).
    2. **Component**: The actual source file or component used (e.g. `HeroBanner.astro`).
    3. **Props/Data**: Input parameters or data sources.
    4. **Description**: Optional context or notes.

## 5. Storage Convention

PAGE_MAP and BLUEPRINT files MUST be stored in a `.pageel/page-maps/` directory at the repository root. Each page gets its own subdirectory.

- **Location**: `.pageel/page-maps/<page-name>/`
- **Rationale**: Hidden dot-folder keeps page maps separate from source code, consistent with `.pageelrc.json` (pageel-cms) and familiar patterns like `.vscode/`, `.github/`.
- **Directory structure**:
  ```
  repo/
  ├── .pageel/
  │   └── page-maps/
  │       ├── index/
  │       │   ├── PAGE_MAP.md
  │       │   └── BLUEPRINT.md
  │       ├── about/
  │       │   ├── PAGE_MAP.md
  │       │   └── BLUEPRINT.md
  │       └── ...
  ├── .pageelrc.json       ← CMS config (if using pageel-cms)
  └── src/
  ```
- **Naming**: Subdirectory name SHOULD match the page route (e.g., `index`, `contact`, `docs-index`).
- **Discovery**: AI agents SHOULD search `.pageel/page-maps/` first when looking for page structure information.
