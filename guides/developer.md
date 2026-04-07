---
layout: default
title: Developer
parent: Workflow Guides
nav_order: 1
---

# Developer Workflows

8 tình huống phổ biến nhất khi code hàng ngày.

[← Tất cả guides](.)

---

## 1. Xây feature từ đầu

> "Thêm chức năng login với Google OAuth"

### Bước 1 — Lên kế hoạch

```
/mk:plan "implement Google OAuth login with session management"
```

Kit sẽ chia task thành phases (database → API → frontend → tests), lưu trong `plans/`.

### Bước 2 — Implement

```
/mk:cook "implement Google OAuth login"
```

Hoặc trỏ vào plan đã tạo:

```
/mk:cook plans/260403-1200-google-oauth/plan.md
```

Kit sẽ tự: research best practices → implement từng phase → chạy tests → review code → hỏi bạn approve.

### Bước 3 — Ship

```
/mk:ship
```

Kit tự: merge target branch → chạy tests → review → bump version → tạo PR.

### Tips

- Dùng `/mk:cook --fast` nếu feature nhỏ, không cần research phase.
- Dùng `/mk:cook --auto` nếu tin tưởng kit tự quyết (skip approval gates).
- Dùng `/mk:cook --parallel` nếu feature có nhiều phần độc lập (ví dụ: 3 API endpoints song song).

---

## 2. Fix bug production

> "API `/users` trả 500 khi user không có avatar"

### Nhanh (bug rõ ràng)

```
/mk:fix --quick "GET /users returns 500 when user has no avatar"
```

Kit scout → diagnose → fix → test. Dùng cho lỗi lint, type error, null check.

### Chuẩn (bug cần phân tích)

```
/mk:fix "GET /users returns 500 when user has no avatar"
```

Kit sẽ: scout files liên quan → phân tích root cause (không đoán) → fix → viết regression test → verify.

### Nghiêm trọng (cần review trước khi fix)

```
/mk:fix --review "payment endpoint returning wrong amount"
```

Kit sẽ dừng ở mỗi bước để bạn approve trước khi tiếp.

### Sau khi fix

```
/mk:git cp
```

Commit + push luôn. Kit tự viết commit message chuẩn conventional commits.

---

## 3. Tiếp nhận codebase lạ

> "Vừa join project, chưa biết gì về codebase"

### Bước 1 — Generate docs

```
/mk:docs init
```

Kit scan toàn bộ codebase, tạo: `docs/codebase-summary.md`, `docs/system-architecture.md`, `docs/code-standards.md`.

### Bước 2 — Hỏi cụ thể

```
Giải thích cách authentication hoạt động trong project này
```

```
File nào handle payment logic?
```

Kit đã có context từ docs vừa tạo, trả lời chính xác hơn.

### Bước 3 — Bắt đầu task đầu tiên

```
/mk:plan "add email verification to signup flow"
```

Kit sẽ plan dựa trên kiến trúc hiện tại, không phải generic template.

---

## 4. Tăng test coverage

> "Coverage đang 40%, cần lên 80% trước release"

### Chạy tự động qua đêm

```
/mk:autoresearch
```

Kit sẽ hỏi:
- **Goal:** coverage 80%
- **Scope:** src/**/*.ts
- **Verify command:** jest --coverage
- **Guard command:** npm test
- **Iterations:** 30

Kit tự lặp 30 vòng: viết tests → chạy coverage → giữ nếu tăng, bỏ nếu giảm → lặp lại.

### Hoặc viết tests thủ công có hướng dẫn

```
/mk:test
```

Kit chạy tests hiện tại, báo cáo files nào thiếu coverage, gợi ý viết tests cho đâu.

---

## 5. Refactor an toàn

> "File `api.ts` 800 dòng, cần tách module"

### Bước 1 — Plan

```
/mk:plan "refactor api.ts into separate route modules"
```

Kit phân tích dependencies, đề xuất cách tách mà không break imports.

### Bước 2 — Implement

```
/mk:cook plans/260403-refactor-api/plan.md
```

Kit tách từng module, update imports, giữ API contract.

### Bước 3 — Verify

```
/mk:test
```

Chạy toàn bộ test suite. Coverage không được giảm, không test nào fail.

### Bước 4 — Review

```
/mk:code-review --pending
```

Kit review staged changes: kiểm tra spec compliance → code quality → adversarial review (tìm edge cases bị break).

---

## 6. Review & ship PR

> "Code xong, cần review rồi merge vào main"

### Review

```
/mk:code-review --pending
```

Kit chạy 3 stages:
1. **Spec compliance** — code có đúng yêu cầu không?
2. **Code quality** — standards, security, performance
3. **Adversarial** — cố tìm cách break code

### Hoặc review PR của người khác

```
/mk:code-review #42
```

### Ship khi review pass

```
/mk:ship
```

Kit tự: merge latest main → run tests → review → bump version → commit → push → tạo PR trên GitHub.

### Ship beta

```
/mk:ship beta
```

Pipeline nhẹ hơn: skip docs update, push to dev/beta branch.

---

## 7. Setup project mới

> "Bắt đầu project Node.js + React từ đầu"

### Bước 1 — Tạo project & cài kit

```bash
mkdir my-app && cd my-app
npm init -y
npx my-agent-kit init --all
```

### Bước 2 — Thêm context

Mở `CLAUDE.md`, thêm:

```markdown
## My Project
- Stack: Node.js + React + PostgreSQL
- Style: functional, ESM imports
- Testing: Vitest + React Testing Library
- Deploy: Docker on Railway
```

### Bước 3 — Bootstrap

```
/mk:cook "setup project structure with Express API, React frontend, and PostgreSQL connection"
```

Kit tạo cấu trúc project, cài dependencies, setup configs.

### Bước 4 — Generate docs

```
/mk:docs init
```

---

## 8. Debug performance

> "App load mất 5 giây, cần tìm bottleneck"

### Bước 1 — Phân tích

```
/mk:debug "app takes 5 seconds to load, need to find bottleneck"
```

Kit chạy 4-phase investigation:
1. Reproduce → 2. Analyze → 3. Root cause → 4. Verify

### Bước 2 — Fix

```
/mk:fix "optimize slow database query in /api/dashboard"
```

### Bước 3 — Tối ưu tự động

```
/mk:autoresearch
```

- **Goal:** load time < 1s
- **Verify:** `curl -w '%{time_total}' http://localhost:3000`
- **Iterations:** 20

Kit tự lặp: optimize → đo → giữ nếu nhanh hơn → tiếp tục.

### Bước 4 — Verify

```
/mk:test
```

Đảm bảo optimization không break gì.
