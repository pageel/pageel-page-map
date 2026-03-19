<div align="center">
  <img src="https://raw.githubusercontent.com/pageel/pageel-theme-kit/main/public/icon.svg" alt="Pageel Page Map" width="100" height="auto" />
  <h1>Pageel Page Map</h1>
  <p><strong>An AI Agent Skill that teaches any coding agent to see and navigate webpage layouts — not just code trees.</strong></p>
  <p><em>Drop in <code>SKILL.md</code>, map your pages, and watch your AI stop guessing which component to edit.</em></p>

[![AI Skill](https://img.shields.io/badge/AI_Skill-Agent--Ready-8B5CF6?style=for-the-badge)](./SKILL.md)
[![Astro](https://img.shields.io/badge/Astro-FF5D01?style=for-the-badge&logo=astro&logoColor=white)](https://astro.build)
[![MIT License](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)](./LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.0-blue?style=for-the-badge)](./docs/spec.md)

</div>

> **Standalone AI Agent Skill** — Works with any AI coding agent (Cursor, Windsurf, Gemini CLI, Claude Code). Part of the [Pageel](https://github.com/pageel) ecosystem.

## 🌟 The Problem

When humans build or modify a webpage, we see a global visual layout (nav, hero, sidebar, footer).
When AI Agents modify a webpage, they see endless trees of `.astro`, `.tsx`, or `.vue` files — isolated from the big picture.
This often leads to AI altering the wrong component or losing track of the structural hierarchy.

## 🚀 The Solution

The **Page Map** architecture solves this by providing **two anchor files**:

1. **`PAGE_MAP.md`** — An intuitive ASCII wireframe showing the exact visual layout geometry, identifying sections with tags like `[hero.title]`.
2. **`BLUEPRINT.md`** — A mapping table linking those tags directly to the actual source code (`src/components/Hero.astro`).

By supplying this shared "mental map," AI Agents become hyper-accurate in UI localization, and developers can instantly swap themes without breaking content structures.

### 🗺️ Example: What a PAGE_MAP Looks Like

```
┌──────────────────────────────────────────────────────────┐
│ [header]                                                 │
│  logo ─── nav(docs, blog, contact) ─── actions(gh, lang) │
├──────────────────────────────────────────────────────────┤
│ [hero]                                                   │
│ ┌───────────┬──────────────────┬──────────────────┐      │
│ │ [hero.    │ [hero.content]   │ [hero.visual]    │      │
│ │  sidebar] │                  │                  │      │
│ │           │ Welcome to       │ <HeroImage/>     │      │
│ │ vertical  │ My Project       │                  │      │
│ │ text      │ tagline + CTA    │                  │      │
│ └───────────┴──────────────────┴──────────────────┘      │
├──────────────────────────────────────────────────────────┤
│ [features]                                               │
│  Feature cards grid (3 columns)                          │
├──────────────────────────────────────────────────────────┤
│ [footer]                                                 │
│  links ─── social ─── copyright                          │
└──────────────────────────────────────────────────────────┘
```

Then the **BLUEPRINT** maps each tag to real code:

| Section | Tag | Component | Notes |
|:--------|:----|:----------|:------|
| header | `[header]` | `src/components/Header.astro` | Fixed, scroll effect |
| hero.content | `[hero.content]` | `src/pages/index.astro` (inline) | h1 + CTA button |
| hero.visual | `[hero.visual]` | `src/components/HeroImage.tsx` | React, client:load |
| features | `[features]` | `src/components/FeatureGrid.astro` | 3-col grid |
| footer | `[footer]` | `src/components/Footer.astro` | Dark background |

### 📊 Validated Results

| Metric | Result |
|:-------|:-------|
| Token savings per page | **~87% average** |
| Agent navigation accuracy | **3/3 test scenarios passed** |
| Build impact | **Zero** (comments only) |

> Measured during real-world testing on a production Astro site with 120+ pages.

## 📦 What's Included

| File | Description |
|:-----|:------------|
| `SKILL.md` | Drop-in AI agent instructions — makes any agent understand page map context |
| `docs/spec.md` | Complete format specification (naming, inline tags, storage convention) |
| `templates/` | Blank `PAGE_MAP.md` + `BLUEPRINT.md` templates |
| `examples/` | Real-world mappings: Landing Page, Documentation Site, Blog |

## 🚀 Quick Start

### 1. Install the Skill

Copy `SKILL.md` into your agent's custom instructions or skills folder:

```bash
# For PARA Workspace users
cp SKILL.md /path/to/workspace/.agent/skills/page-map/SKILL.md

# For Cursor / Windsurf / other agents
# Copy SKILL.md content into your agent's custom instructions
```

### 2. Create Page Maps

Store page maps in `.pageel/page-maps/` at your repository root:

```
your-project/
├── .pageel/
│   └── page-maps/
│       ├── index/
│       │   ├── PAGE_MAP.md    ← Visual wireframe
│       │   └── BLUEPRINT.md   ← Component mapping
│       └── about/
│           ├── PAGE_MAP.md
│           └── BLUEPRINT.md
├── .pageelrc.json              ← (optional) CMS config
└── src/
```

### 3. Add Inline Tags

Mark sections in your source code so the agent can navigate precisely:

```astro
{/* [hero.cta] */}
<a href="/docs" class="btn-primary">Get Started</a>

{/* [hero.title] */}
<h1 class="text-6xl font-bold">Welcome</h1>
```

### 4. Let the Agent Work

Now when you say _"fix the CTA in hero"_, the agent will:
1. Read `.pageel/page-maps/index/BLUEPRINT.md` → find `[hero.cta]` → locate component file
2. Grep `{/* [hero.cta] */}` in source → navigate to exact line
3. Edit only the tagged section — **no guesswork**

## 📐 Format Specification

See [`docs/spec.md`](./docs/spec.md) for the complete specification covering:
- Section naming convention: `[section.subsection]`
- Inline tag format: `{/* [section.subsection] */}`
- Storage convention: `.pageel/page-maps/<page-name>/`
- PAGE_MAP and BLUEPRINT file requirements

## 🤝 Contributing

Contributions are welcome! Ideas for improvement:
- ASCII layouts for new framework patterns (Next.js, SvelteKit, Nuxt)
- Better BLUEPRINT column schemas
- Integration examples for other AI agents

See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

## 📚 Related

- [`pageel-theme-kit`](https://github.com/pageel/pageel-theme-kit) — Full theme management with validator + CLI
- `@pageel/mcp-page-map` — *(Coming soon)* MCP server exposing page maps as resources

## License

[MIT](./LICENSE) — Built with ❤️ by the [Pageel](https://github.com/pageel) team.
