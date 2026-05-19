---
layout: default
title: Web full-stack
parent: Workflow Guides
nav_order: 3
---

# Web full-stack — React/Next + API + DB

{: .no_toc }

Đặc trưng: frontend SPA/SSR + API + database, thường có auth, đôi khi billing,
nhiều I/O và state.

[← CLI tool](cli-tool) · [Tiếp: Infra/DevOps →](infra-devops)

---

## Lõi vẫn áp dụng đầy đủ

5-agent chain + `cook`/`scout` — xem [Lõi bất biến](core). Bảng dưới là skill
*theo lớp* của stack web.

| Lớp | Skill trọng tâm | Nhấn mạnh agent |
|---|---|---|
| **Frontend** | `frontend-development`, `react-best-practices`, `ui-styling`, `frontend-design` (hoặc `ui-ux-pro-max` khi design-heavy), `web-frameworks` | thêm `ui-ux-designer` *trước* `fullstack-developer` khi UX không tầm thường |
| **Backend / API** | `backend-development`, `databases`, `better-auth` (chỉ khi auth trong scope), `payment-integration` (chỉ khi billing trong scope) | chain chuẩn |
| **Verify** | `web-testing` (browser/E2E), `test` | `tester` chạy E2E + unit trên code đã simplify |
| **Docs / API contract** | `docs`, `mintlify` (nếu có docs site công khai) | `docs-manager` sau khi tích hợp |

### Skill bổ sung hữu ích cho web (ngoài tài liệu gốc)

| Skill | Vì sao hợp web full-stack |
|---|---|
| `docs-seeker` | API framework (Next/React/ORM) đổi nhanh — tra context7 thay vì đoán theo trí nhớ |
| `sequential-thinking` | thiết kế data flow / state / cache nhiều tầng cần suy luận có cấu trúc |
| `security-scan` | web có bề mặt tấn công lớn (authn/z, injection, XSS) — quét trước khi ship |
| `performance` / `mk:debug` | điều tra render chậm, N+1 query, bundle phình |
| `mk:ship` | pipeline test → review → commit → PR khi release |

---

## Thứ tự chain cho web

```
researcher ─▶ ui-ux-designer ─▶ planner ─▶ fullstack-developer
           ─▶ code-simplifier ─▶ tester (+ web-testing) ─▶ code-reviewer
```

`ui-ux-designer` chỉ chèn khi UX không tầm thường — không mặc định.

---

## Bỏ / cẩn trọng

- **Bỏ:** mobile, shader/threejs/remotion, orchestration kiểu sprint
  time-boxed (trừ khi đúng là một sprint time-boxed thật).
- **Cẩn trọng:** đừng kéo `payment-integration` / `better-auth` vào nếu
  billing/auth *chưa* thực sự trong scope — chúng nặng và rất tình huống.
- **Cẩn trọng:** `ui-ux-pro-max` chỉ khi design là trọng tâm; project CRUD
  thường `ui-styling` là đủ.

---

[← CLI tool](cli-tool) · [Tiếp: Infra/DevOps →](infra-devops)
