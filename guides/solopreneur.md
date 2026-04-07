---
layout: default
title: Solopreneur
parent: Workflow Guides
nav_order: 2
---

# Solopreneur Workflows

Một mình làm hết — từ idea đến production.

[← Tất cả guides](.)

---

## 9. MVP từ zero

> "Có idea SaaS todo app, cần ship MVP trong 1 tuần"

### Bước 1 — Setup

```bash
mkdir my-saas && cd my-saas
npm init -y
npx my-agent-kit init --all
```

Thêm context vào `CLAUDE.md`:

```markdown
## My Project
- Stack: Next.js + Prisma + PostgreSQL
- Goal: MVP todo app with auth and teams
- Deploy: Vercel
- Style: ship fast, iterate later
```

### Bước 2 — Plan

```
/mk:plan "MVP todo app: auth (Google OAuth), CRUD todos, team sharing, deploy to Vercel"
```

Kit chia thành 4-5 phases, mỗi phase có acceptance criteria rõ ràng.

### Bước 3 — Implement từng phase

```
/mk:cook plans/260403-mvp-todo/plan.md
```

Kit implement phase-by-phase, tự chạy tests giữa mỗi phase.

### Bước 4 — Deploy

```
/mk:deploy
```

Kit detect Next.js → gợi ý Vercel → setup → deploy → trả về production URL.

### Tips

- Dùng `/mk:cook --fast` cho phases đơn giản (CRUD).
- Dùng `/mk:cook --auto` nếu không muốn approve từng bước.
- Cuối ngày: `/mk:ship` để commit + push mọi thứ.

---

## 10. Landing page nhanh

> "Cần landing page cho product, có trong 1 ngày"

### Bước 1 — Design + Code cùng lúc

```
/mk:cook "create landing page: hero section with CTA, features grid (3 features), pricing table (free/pro), footer. Modern, dark theme, responsive."
```

Kit tự: plan layout → implement HTML/CSS → responsive → review.

### Bước 2 — Preview

```
/mk:preview --html index.html
```

Mở trực tiếp trong browser để review.

### Bước 3 — Deploy

```
/mk:deploy
```

Kit detect static site → gợi ý GitHub Pages hoặc Cloudflare Pages (miễn phí).

### Bước 4 — Iterate

```
/mk:fix "CTA button needs more contrast, pricing table misaligned on mobile"
```

Sửa nhanh, deploy lại.

---

## 11. Thêm payment

> "Cần tích hợp Stripe để thu phí subscription"

### Bước 1 — Plan

```
/mk:plan "integrate Stripe subscription payments: checkout, webhook, customer portal"
```

Kit research Stripe best practices, plan phases: schema → API → webhook → portal.

### Bước 2 — Implement

```
/mk:cook plans/260403-stripe/plan.md
```

Kit implement: Stripe SDK setup → checkout session → webhook handler → customer portal redirect → test với Stripe CLI.

### Bước 3 — Test

```
/mk:test
```

Kit verify: webhook signatures, subscription lifecycle, error handling.

### Bước 4 — Ship

```
/mk:ship
```

### Lưu ý

- Đảm bảo `STRIPE_SECRET_KEY` nằm trong `.env` (không commit).
- Kit tự kiểm tra security: không log API keys, validate webhook signatures.
