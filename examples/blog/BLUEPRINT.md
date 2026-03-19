# BLUEPRINT: Blog List

| Section | Component | Props / Data | Description |
| :--- | :--- | :--- | :--- |
| `[header.banner]` | `src/components/Header.astro` | | Common site banner |
| `[blog.featured_post]`| `src/components/FeaturedCard.astro` | `post={latestPost}` | Most recent highlighted post |
| `[blog.grid_item]` | `src/components/PostCard.astro` | `post={postItem}` | Single post card in the grid |
| `[blog.pagination]` | `src/components/Pagination.astro` | `page={page}` | Page count navigation |
