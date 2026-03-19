---
name: page-map
description: AI Agent skill to read, manage, and manipulate website visual structure using PAGE_MAP.md and BLUEPRINT.md.
---

# Skill: page-map

> **Version**: 1.1.0

## Intent
Use this skill when attempting to modify page layout, analyze frontend structure, or create new views/components. This skill anchors the AI Agent's structural understanding before analyzing complex source code (`.astro`, `.tsx`, etc.).

## Instructions

### 1. Identify Existing Page Maps
Whenever tasked with analyzing or altering a UI page, search for `PAGE_MAP.md` and `BLUEPRINT.md` in this order:
1. **`.pageel/page-maps/<page-name>/`** — Standard location (preferred).
2. **Current or target directory** — Fallback for legacy or simple setups.

### 2. Reading Format
The structural layout relies on bracketed section names like `[section.subsection]`.
- `PAGE_MAP.md`: Shows visual ASCII wireframes to quickly grasp the layout geometry.
- `BLUEPRINT.md`: Provides a table mapping those brackets to exact component files (e.g., `src/components/Hero.astro`).

### 3. Modifying Code
Search within the target source code for inline tags such as `{/* [section.subsection] */}`. Apply your edits contextually near the tags. DO NOT alter sections outside of the designated tags unless specifically requested.

### 4. Creating New Layouts
When asked to create a new layout:
1. Create `PAGE_MAP.md` containing ASCII wireframes that illustrate the user's layout vision. Use `[section.subsection]` references.
2. Create `BLUEPRINT.md` to map those tags to the intended component files and props.
3. Store both files in `.pageel/page-maps/<page-name>/` at the repository root.
