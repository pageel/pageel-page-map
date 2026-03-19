# Cấu trúc kỹ thuật định dạng Page Map (Format Specification)

> **Dự án**: pageel-page-map
> **Phiên bản**: 1.0.0
> **Ngày cập nhật**: 2026-03-19

Tài liệu này định nghĩa chuẩn định dạng của các tập tin `PAGE_MAP.md` và `BLUEPRINT.md`, cùng quy ước đặt tên nhằm mục đích quy chuẩn hoá quá trình tách biệt và quản lý layout.

---

## 1. Naming Convention (Quy ước đặt tên)
Quy ước đặt tên các phần tử layout tuân theo chuẩn phân cấp và được đặt trong ngoặc vuông: `[section.subsection]`.
- **Định dạng**: `[<tên-phần-chính>.<tên-phần-phụ>]`
- **Ví dụ**: `[hero.title]`, `[content.sidebar]`, `[footer.links]`
- **Mục đích**: Đảm bảo sự đồng bộ trong việc định danh các section của trang trên cả tài liệu sơ đồ và mã nguồn.

## 2. Inline Tag Format (Công cụ gắn thẻ mã nguồn)
Trong mã nguồn (ví dụ `.astro`), mỗi đoạn code tương ứng với layout block cần được đánh dấu bằng chú thích (comment) để các công cụ tự động hoặc AI có thể đối chiếu chính xác với `BLUEPRINT.md`.
- **Định dạng**: `{/* [section.subsection] */}`
- **Ví dụ trong Astro/JSX**:
  ```astro
  {/* [hero.title] */}
  <h1 class="text-3xl font-bold">Chào mừng đến với hệ sinh thái</h1>
  ```

## 3. Định dạng `PAGE_MAP.md`
- **Vai trò**: Cung cấp bức tranh tổng thể về cấu trúc trực quan (wireframe dạng văn bản) của một ứng dụng/trang web. Đây là tệp ổn định (stable) dùng cho góc nhìn con người và tổng quan cho hệ thống AI.
- **Yêu cầu Format**:
  - Tên tệp bắt buộc: `PAGE_MAP.md`
  - Khuyến khích sử dụng Text/ANSI art qua các khối Markdown để minh họa trực quan cho giao diện.
  - Mỗi section trình bày trong bản vẽ bắt buộc phải kèm theo tag phân định danh theo naming convention: `[section.subsection]`.

## 4. Định dạng `BLUEPRINT.md`
- **Vai trò**: Bản đồ kỹ thuật giúp mapping (liên kết) giữa cấu trúc không gian (từ `PAGE_MAP.md`) sang các thành phần cụ thể đã được lập trình sẵn. Đây là tệp có khả năng hoán đổi linh hoạt (swappable component mapping).
- **Yêu cầu Format**:
  - Tên tệp bắt buộc: `BLUEPRINT.md`
  - Bắt buộc sử dụng cấu trúc bảng Markdown (Markdown tables) cho mục đích đối chiếu.
  - **Cấu trúc cột được đề xuất**:
    1. **Block / Section**: Tên tag theo naming convention (VD: `[hero.title]`).
    2. **Component**: Tên phần tử/mã nguồn sẽ được sử dụng thực tế (VD: `HeroBanner.astro`).
    3. **Props/Data**: Tham số dữ liệu đầu vào.
    4. **Mô tả**: Ghi chú tuỳ chọn.
