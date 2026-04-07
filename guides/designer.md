---
layout: default
title: Designer
parent: Workflow Guides
nav_order: 5
---

# Designer Workflows

Từ mockup đến code, review UI, xây design system.

[← Tất cả guides](.)

---

## 19. Implement design → code

> "Có mockup Figma, cần biến thành responsive HTML/CSS"

### Bước 1 — Mô tả design

```
/mk:cook "implement this design: header with logo + nav, hero section with gradient background, 3-column feature cards, testimonial carousel, CTA section, footer with links. Dark theme, rounded corners, use Tailwind CSS."
```

Hoặc nếu có screenshot:

```
Implement giao diện giống screenshot này: [paste screenshot path]
```

Kit sẽ: phân tích layout → implement HTML + Tailwind → responsive → review.

### Bước 2 — Preview

```
/mk:preview --html index.html
```

Mở browser, kiểm tra visual.

### Bước 3 — Iterate

```
/mk:fix "hero section needs more padding, cards should have hover shadow"
```

Fix nhanh, preview lại.

---

## 20. Review UI consistency

> "UI bị lệch style giữa các pages"

### Bước 1 — Scan

```
/mk:code-review codebase
```

Kit scan toàn bộ frontend: tìm inconsistent colors, spacing, font sizes, component patterns.

### Bước 2 — Fix

```
/mk:fix "standardize button styles across all pages to use primary/secondary variants"
```

Kit tìm tất cả buttons, refactor về shared components.

### Bước 3 — Verify

```
/mk:test ui http://localhost:3000
```

Kit chụp screenshots tất cả pages, kiểm tra responsive, accessibility.

---

## 21. Tạo design system

> "Cần chuẩn hóa components cho team"

### Bước 1 — Scan existing patterns

```
/mk:plan "create design system: extract existing UI patterns into reusable components"
```

Kit scan codebase, liệt kê: buttons (bao nhiêu variants), colors (bao nhiêu khác nhau), spacing, typography.

### Bước 2 — Implement

```
/mk:cook plans/260403-design-system/plan.md
```

Kit tạo: shared component library, design tokens (colors, spacing, typography), documentation.

### Bước 3 — Document

```
/mk:docs update
```

Kit generate `docs/design-guidelines.md` với danh sách components, usage examples, do's and don'ts.
