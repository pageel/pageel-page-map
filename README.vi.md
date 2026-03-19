<div align="center">
  <img src="https://raw.githubusercontent.com/pageel/pageel-theme-kit/main/public/icon.svg" alt="Pageel Page Map" width="100" height="auto" />
  <h1>Pageel Page Map Skill</h1>
  <p><strong>Một AI Agent Skill giúp bất kỳ coding agent nào nhìn thấy và điều hướng layout trang web — thay vì chỉ thấy danh mục cây code.</strong></p>
  <p><em>Chỉ cần thêm <code>SKILL.md</code>, map các trang, và để AI ngừng đoán mò khi sửa component.</em></p>

[![AI Skill](https://img.shields.io/badge/AI_Skill-Agent--Ready-8B5CF6?style=for-the-badge)](./SKILL.md)
[![Astro](https://img.shields.io/badge/Astro-FF5D01?style=for-the-badge&logo=astro&logoColor=white)](https://astro.build)
[![MIT License](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)](./LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.0-blue?style=for-the-badge)](./docs/spec.md)

</div>

> **AI Agent Skill độc lập** — Hoạt động với mọi AI coding agent (Cursor, Windsurf, Gemini CLI, Claude Code). Thuộc hệ sinh thái [Pageel](https://github.com/pageel).
>
> 🌐 [English version](./README.md)

## 🌟 Vấn đề

Khi con người xây dựng hoặc sửa một trang web, chúng ta nhìn thấy **layout tổng thể** (nav, hero, sidebar, footer).
Khi AI Agent sửa trang web, chúng chỉ thấy hàng loạt file `.astro`, `.tsx`, hay `.vue` — tách biệt khỏi bức tranh toàn cảnh.
Điều này dẫn đến AI thường sửa nhầm component hoặc mất dấu cấu trúc phân cấp.

## 🚀 Giải pháp

Kiến trúc **Page Map** giải quyết vấn đề này bằng **hai file neo**:

1. **`PAGE_MAP.md`** — Wireframe ASCII trực quan thể hiện hình học layout, đánh dấu các section bằng tag như `[hero.title]`.
2. **`BLUEPRINT.md`** — Bảng ánh xạ liên kết các tag đó trực tiếp tới source code (`src/components/Hero.astro`).

Bằng cách cung cấp "bản đồ tư duy" chung này, AI Agent trở nên siêu chính xác khi định vị UI, và developer có thể hoán đổi theme mà không phá vỡ cấu trúc nội dung.

### 🗺️ Ví dụ: PAGE_MAP trông như thế nào

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
│  Feature cards grid (3 cột)                              │
├──────────────────────────────────────────────────────────┤
│ [footer]                                                 │
│  links ─── social ─── copyright                          │
└──────────────────────────────────────────────────────────┘
```

Sau đó **BLUEPRINT** ánh xạ mỗi tag tới code thực:

| Section | Tag | Component | Ghi chú |
|:--------|:----|:----------|:--------|
| header | `[header]` | `src/components/Header.astro` | Fixed, scroll effect |
| hero.content | `[hero.content]` | `src/pages/index.astro` (inline) | h1 + nút CTA |
| hero.visual | `[hero.visual]` | `src/components/HeroImage.tsx` | React, client:load |
| features | `[features]` | `src/components/FeatureGrid.astro` | Grid 3 cột |
| footer | `[footer]` | `src/components/Footer.astro` | Nền tối |

### 📊 Kết quả kiểm chứng

| Chỉ số | Kết quả |
|:-------|:--------|
| Tiết kiệm token trên mỗi trang | **~87% trung bình** |
| Độ chính xác điều hướng | **3/3 kịch bản test đạt** |
| Ảnh hưởng tới build | **Không** (chỉ là comment) |

> Đo trên một trang Astro production với hơn 120 trang.

## 📦 Bao gồm gì

| File | Mô tả |
|:-----|:------|
| `SKILL.md` | Hướng dẫn AI agent — giúp bất kỳ agent nào hiểu page map |
| `docs/spec.md` | Đặc tả format đầy đủ (đặt tên, inline tags, quy ước lưu trữ) |
| `templates/` | Template trống `PAGE_MAP.md` + `BLUEPRINT.md` |
| `examples/` | Ví dụ thực tế: Landing Page, Trang Tài liệu, Blog |

## 🚀 Bắt đầu nhanh

### 1. Cài Skill

Copy `SKILL.md` vào custom instructions hoặc thư mục skills của agent:

```bash
# Cho người dùng PARA Workspace
cp SKILL.md /path/to/workspace/.agent/skills/page-map/SKILL.md

# Cho Cursor / Windsurf / agent khác
# Copy nội dung SKILL.md vào custom instructions của agent
```

### 2. Tạo Page Maps

Lưu page maps trong `.pageel/page-maps/` ở root của repo:

```
your-project/
├── .pageel/
│   └── page-maps/
│       ├── index/
│       │   ├── PAGE_MAP.md    ← Wireframe trực quan
│       │   └── BLUEPRINT.md   ← Ánh xạ component
│       └── about/
│           ├── PAGE_MAP.md
│           └── BLUEPRINT.md
├── .pageelrc.json              ← (tuỳ chọn) CMS config
└── src/
```

### 3. Thêm Inline Tags

Đánh dấu các section trong source code để agent điều hướng chính xác:

```astro
{/* [hero.cta] */}
<a href="/docs" class="btn-primary">Bắt đầu</a>

{/* [hero.title] */}
<h1 class="text-6xl font-bold">Chào mừng</h1>
```

### 4. Để Agent làm việc

Giờ khi bạn nói _"sửa CTA trong hero"_, agent sẽ:
1. Đọc `.pageel/page-maps/index/BLUEPRINT.md` → tìm `[hero.cta]` → xác định file component
2. Grep `{/* [hero.cta] */}` trong source → điều hướng tới đúng dòng
3. Chỉ sửa section được đánh dấu — **không đoán mò**

## 📐 Đặc tả Format

Xem [`docs/spec.md`](./docs/spec.md) để biết đặc tả đầy đủ:
- Quy ước đặt tên section: `[section.subsection]`
- Format inline tag: `{/* [section.subsection] */}`
- Quy ước lưu trữ: `.pageel/page-maps/<page-name>/`
- Yêu cầu file PAGE_MAP và BLUEPRINT

## 🤝 Đóng góp

Mọi đóng góp đều được chào đón! Ý tưởng cải thiện:
- Layout ASCII cho framework mới (Next.js, SvelteKit, Nuxt)
- Schema cột BLUEPRINT tốt hơn
- Ví dụ tích hợp cho các AI agent khác

Xem [CONTRIBUTING.md](./CONTRIBUTING.md) để biết hướng dẫn.

## 📚 Liên quan

- [`pageel-theme-kit`](https://github.com/pageel/pageel-theme-kit) — Quản lý theme đầy đủ với validator + CLI
- `@pageel/mcp-page-map` — *(Sắp ra mắt)* MCP server expose page maps dưới dạng resources

## Giấy phép

[MIT](./LICENSE) — Xây dựng với ❤️ bởi đội ngũ [Pageel](https://github.com/pageel).
