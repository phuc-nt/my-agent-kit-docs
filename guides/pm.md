---
layout: default
title: PM / Product
parent: Workflow Guides
nav_order: 4
---

# PM / Product Workflows

Từ idea đến spec, đánh giá feasibility, theo dõi tiến độ.

[← Tất cả guides](.)

---

## 16. Viết PRD từ idea

> "Có idea: thêm chức năng export báo cáo PDF cho users"

### Bước 1 — Brainstorm

```
/mk:brainstorm "feature: users can export their dashboard data as PDF reports"
```

Kit phân tích: use cases, edge cases, technical considerations, effort estimation.

### Bước 2 — Plan thành spec

```
/mk:plan "PDF export feature: generate dashboard reports, schedule weekly emails, custom templates"
```

Kit tạo structured plan trong `plans/`:
- Phases với acceptance criteria
- Technical requirements
- Dependencies
- Risk assessment

### Bước 3 — Review plan

Đọc `plans/260403-pdf-export/plan.md`, chỉnh sửa nếu cần, rồi share cho dev team.

### Tips

- Plan file là markdown — copy vào Notion/Linear/Jira dễ dàng.
- Dùng `/mk:predict` trước khi finalize để 5 experts flag risks.

---

## 17. Đánh giá feasibility

> "Stakeholder muốn thêm real-time collaboration, có khả thi trong 1 sprint không?"

### Bước 1 — Expert debate

```
/mk:predict "adding real-time collaboration (like Google Docs) to our existing editor in 2 weeks"
```

5 experts (architect, security, performance, UX, ops) sẽ debate:
- Architect: WebSocket infrastructure cần gì?
- Performance: bao nhiêu concurrent users?
- Security: auth cho WebSocket connections?
- UX: conflict resolution khi 2 người edit cùng lúc?
- Ops: scaling, monitoring?

### Bước 2 — Edge cases

```
/mk:scenario "real-time collaborative editing with 10+ users"
```

Kit generate scenarios: network disconnect mid-edit, conflicting edits, permission changes during session, mobile vs desktop.

### Bước 3 — Trả lời stakeholder

Dựa trên output, bạn có data để nói:
- "Feasible nhưng cần 2 sprints thay vì 1, vì cần WebSocket infrastructure + conflict resolution"
- Hoặc: "Recommend phase 1: view-only real-time, phase 2: collaborative editing"

---

## 18. Theo dõi tiến độ

> "Sprint đang chạy, muốn xem đang ở đâu"

### Xem status

```
/mk:kanban
```

Kit đọc `plans/` và hiển thị kanban board: TODO → IN PROGRESS → DONE cho mỗi phase.

### Update plan

```
Cập nhật plan: phase-02 đã xong, phase-03 đang blocked vì chờ API key
```

Kit update status trong plan file, ghi note blocker.

### Generate report

```
/mk:docs update
```

Kit sync tiến độ vào `docs/project-roadmap.md`.
