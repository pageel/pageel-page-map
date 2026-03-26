# BLUEPRINT: [Page Name]

> Page-level blueprint linking sections to source components.

| Section              | Source                         | Hydration      | Component Map                                     |
| :------------------- | :----------------------------- | :------------- | :------------------------------------------------ |
| `[page.nav]`         | `src/components/Navbar.astro`  | Static         | [components/Navbar/](../../components/Navbar/PAGE_MAP.md) |
| `[page.hero]`        | `src/components/Hero.astro`    | Static         | [components/Hero/](../../components/Hero/PAGE_MAP.md)     |
| `[page.content]`     | `src/pages/index.astro`        | —              | — (inline: main content area)                     |
| `[page.footer]`      | `src/components/Footer.astro`  | Static         | — (simple, no internal map needed)                |
