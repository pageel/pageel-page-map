# 🗺️ Pageel Page Map Ecosystem

<div align="center">
  <p><strong> Bridging the gap between human visualization and AI structural comprehension. </strong></p>
</div>

> **Notice**: This project is built to perfectly integrate with [`pageel-theme-kit`](https://github.com/pageel/pageel-theme-kit) and the upcoming `@pageel/mcp-page-map` server.

## 🌟 The Problem
When humans build or modify a webpage, we see a global visual layout (nav, hero, sidebar, footer).
When AI Agents modify a webpage, they see endless trees of `.astro`, `.tsx`, or `.vue` files isolated from the big picture. 
This often leads to AI altering the wrong component or losing track of the structural hierarchy.

## 🚀 The Solution
The **Page Map** architecture solves this by providing **two anchor files**:
1. `PAGE_MAP.md`: An intuitive ASCII/Text wireframe showing the exact visual layout geometry and identifying sections with tags like `[hero.title]`.
2. `BLUEPRINT.md`: A mapping table linking those tags directly to the actual source code (`src/components/Hero.astro`).

By supplying this shared "mental map," AI Agents become hyper-accurate in UI localization, and developers can instantly swap themes without breaking content structures.

## 📦 What's Included?
- `docs/spec.md`: The complete format specification for `PAGE_MAP` and `BLUEPRINT`.
- `SKILL.md`: A drop-in AI instructions file making any standard agent understand the page map context.
- `templates/`: Blank templates to scaffold your projects.
- `examples/`: Real-world mappings for a **Landing Page**, **Documentation Site**, and **Blog**.

## 🚀 Quick Start
1. **Empower your AI**: Copy `SKILL.md` into your agent's custom instructions or `.agents/skills` folder.
2. **Scaffold Layouts**: Copy `templates/PAGE_MAP.md` and `templates/BLUEPRINT.md` into your UI folder (e.g., `src/pages/`).
3. **Map the Code**: Inside your component code, use inline comment tags matching your sections.
   ```astro
   {/* [hero.cta] */}
   <a href="/docs" class="btn-primary">Get Started</a>
   ```

## 🤝 Contributing
Contributions are welcome! If you have better ASCII layouts or new framework examples, feel free to open a PR.

---
*Maintained with ❤️ by the Pageel Team.*
