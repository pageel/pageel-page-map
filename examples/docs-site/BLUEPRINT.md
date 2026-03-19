# BLUEPRINT: Documentation

| Section | Component | Props / Data | Description |
| :--- | :--- | :--- | :--- |
| `[sidebar.nav]` | `src/components/Sidebar.astro` | `items={docNav}` | Left navigation sidebar |
| `[content.title]` | `src/layouts/DocLayout.astro` | `title={frontmatter.title}` | Documentation article title |
| `[content.body]` | `src/layouts/DocLayout.astro` | `<slot />` | Implicit Markdown rendering area |
| `[content.pagination]`| `src/components/Pager.astro` | `prev={p}, next={n}` | Page navigation buttons |
