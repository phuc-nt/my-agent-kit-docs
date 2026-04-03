---
layout: default
title: Tech Lead Workflows — My Agent Kit
---

# Tech Lead Workflows

Review, plan, secure, onboard — lead hiệu quả hơn.

[← Tất cả guides](.)

---

## 12. Review PR của team

> "Team member gửi PR #42, cần review nhanh"

### Review PR cụ thể

```
/mk:code-review #42
```

Kit chạy 3 stages:
1. **Spec compliance** — PR có đúng yêu cầu ticket không?
2. **Code quality** — naming, patterns, security, performance
3. **Adversarial** — cố tìm edge cases, race conditions, resource leaks

Output: danh sách findings với severity (critical/warning/info), verdict approve/request-changes.

### Review toàn bộ codebase

```
/mk:code-review codebase parallel
```

Kit spawn nhiều reviewers song song, mỗi reviewer focus 1 area. Dùng khi cần audit tổng thể trước release.

### Tips

- Chỉ critical findings mới block merge — informational findings note lại cho sau.
- Kit tự kiểm tra: SQL injection, XSS, secrets in code, missing auth checks.

---

## 13. Lên plan sprint

> "Cần chia task cho sprint 2 tuần, 3 developers"

### Bước 1 — Brainstorm scope

```
/mk:brainstorm "sprint goals: user dashboard, notification system, admin panel"
```

Kit phân tích: effort, dependencies, risk.

### Bước 2 — Plan chi tiết

```
/mk:plan "sprint: user dashboard (high), notification system (medium), admin panel (low)"
```

Kit tạo phases với dependencies rõ ràng, estimate relative complexity.

### Bước 3 — Predict risks

```
/mk:predict "implementing dashboard + notification + admin in 2-week sprint"
```

5 expert personas (architect, security, performance, UX, ops) debate plan, flag risks trước khi bắt đầu.

### Bước 4 — Generate edge cases

```
/mk:scenario "user dashboard with real-time notifications"
```

Kit generate test scenarios across 12 dimensions — giúp QA biết test gì.

---

## 14. Onboard member mới

> "Có developer mới join, cần docs cho họ đọc"

### Bước 1 — Generate docs

```
/mk:docs init
```

Kit tạo:
- `docs/codebase-summary.md` — overview project
- `docs/system-architecture.md` — component diagram, data flow
- `docs/code-standards.md` — naming, patterns, conventions

### Bước 2 — Review docs

```
/mk:code-review codebase
```

Kit scan codebase, bổ sung vào docs những patterns quan trọng mà auto-generate có thể bỏ sót.

### Deliverable

Gửi member mới:
1. Đọc `README.md` trước
2. Đọc `docs/system-architecture.md`
3. Đọc `docs/code-standards.md`
4. Cài kit: `npx my-agent-kit init`
5. Thử: `/mk:cook "add a simple health check endpoint"` để làm quen workflow

---

## 15. Audit security codebase

> "Trước release, cần scan security toàn bộ"

### Bước 1 — Scan

```
/mk:security
```

Kit chạy STRIDE + OWASP audit: scan code cho SQL injection, XSS, auth bypass, secrets exposure, dependency vulnerabilities.

### Bước 2 — Review findings

Kit xuất report với severity levels (critical/high/medium/low), grouped theo OWASP category.

### Bước 3 — Auto-fix

```
/mk:security --auto-fix
```

Kit tự fix những findings có thể tự động sửa (ví dụ: escape output, add CSRF token, remove hardcoded secrets).

### Bước 4 — Verify

```
/mk:test
```

Chạy tests sau khi fix, đảm bảo security patches không break functionality.

### Bước 5 — Re-scan

```
/mk:security
```

Chạy lại, đảm bảo 0 critical findings.
