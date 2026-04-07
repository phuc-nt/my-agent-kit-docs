---
layout: default
title: Tech Writer
parent: Workflow Guides
nav_order: 8
---

# Tech Writer Workflows

API docs, slides, release notes — từ code thành tài liệu.

[← Tất cả guides](.)

---

## 28. Viết docs cho API

> "API chưa có docs, developers bên ngoài không biết dùng"

### Bước 1 — Scan API

```
/mk:docs init
```

Kit scan codebase: tìm routes, controllers, request/response schemas → tạo docs ban đầu.

### Bước 2 — Generate API reference

```
/mk:cook "generate comprehensive API documentation with endpoints, request/response examples, authentication guide, and error codes"
```

Kit tạo:
- Endpoint list với method, path, description
- Request/response examples (JSON)
- Authentication flow
- Error codes + handling guide
- Rate limiting info

### Bước 3 — Review

```
/mk:code-review codebase
```

Kit cross-check: docs có match code thực tế không? Endpoint nào thiếu? Schema nào outdated?

### Output

Docs trong `docs/` — markdown format, dễ convert sang Mintlify, GitBook, hoặc Swagger.

---

## 29. Tạo slides / báo cáo

> "Cần slides cho demo sprint review"

### Bước 1 — Generate slides

```
/mk:preview --html --slides "Sprint 5 review: features shipped, metrics, next sprint goals"
```

Kit tạo HTML slides bao gồm:
- Features completed (từ git log + plans/)
- Code metrics (coverage, lines changed)
- Demo screenshots
- Next sprint priorities

### Bước 2 — Mở browser

Kit tự mở slides trong browser — self-contained HTML, không cần server.

### Tạo báo cáo dạng doc

```
/mk:cook "create sprint report document: features delivered, bugs fixed, coverage metrics, deployment status"
```

Kit generate markdown report từ git history + test results + deployment logs.

---

## 30. Viết release notes

> "Chuẩn bị release v2.0, cần viết changelog + release notes"

### Bước 1 — Generate từ git history

```
/mk:cook "write release notes for v2.0: summarize all changes since v1.0 tag, group by category (features, fixes, improvements), write user-facing descriptions"
```

Kit đọc git log, group commits, viết mô tả thân thiện cho users:

```markdown
## What's New in v2.0

### Features
- **PDF Export** — Export dashboard data as PDF reports
- **Team Sharing** — Invite team members to collaborate

### Fixes
- Fixed 500 error when user has no avatar
- Fixed timezone issue in scheduled reports

### Improvements
- 3x faster dashboard loading
- Better mobile responsive layout
```

### Bước 2 — Review

```
/mk:code-review --pending
```

Đảm bảo release notes chính xác, không bỏ sót changes quan trọng.
