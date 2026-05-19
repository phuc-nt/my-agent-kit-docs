---
layout: default
title: Workflow Guides
nav_order: 2
has_children: true
permalink: /guides/
---

# Workflow Guides — chọn theo loại project

My Agent Kit ship **~80 skills + 14 agents**. Đa số là **tình huống** — chỉ bật
khi task thực sự cần. Skill sprawl làm phình context và chậm chain. Đây là bộ
"thực ra dùng gì" theo từng loại project.

[← Trang chính](../)

---

## Bắt đầu ở đâu

**Đọc [Lõi bất biến](core) trước.** 5-agent chain + ~9 skill lõi xử lý được
~90% mọi project. Mọi thứ bên dưới chỉ là phần *thêm vào* theo loại project.

```
┌─────────────────────────────────────────────┐
│  LÕI BẤT BIẾN  (mọi project, ~90%)           │
│  planner → fullstack-developer →             │
│  code-simplifier → tester → code-reviewer    │
│  + cook · mk:plan · scout · mk:debug · test  │
└───────────────┬─────────────────────────────┘
                │  thêm theo loại project ↓
   ┌────────────┼────────────┐
   ▼            ▼            ▼
 CLI tool   Web full-stack  Infra/DevOps
```

---

## Chọn loại project

| Loại project | Khi nào | Guide |
|---|---|---|
| **Lõi bất biến** | Đọc đầu tiên — đúng cho mọi project | [→ Lõi](core) |
| **CLI / single-binary** | Tool dòng lệnh, spec-locked, binary tĩnh | [→ CLI tool](cli-tool) |
| **Web full-stack** | React/Next + API + DB | [→ Web full-stack](web-fullstack) |
| **Infra / DevOps** | CI/CD, container, cloud, IaC, incident | [→ Infra/DevOps](infra-devops) |
| **Quy tắc chung** | Nguyên tắc áp cho mọi loại | [→ Rules of thumb](rules-of-thumb) |

---

## Nguyên tắc một dòng

> **Match skill theo task, không theo project.** Một web project vẫn *chưa*
> load `payment-integration` cho tới khi có việc billing thật. Phân vân có nên
> thêm skill → **đừng**. Absence rẻ hơn sprawl.

Chi tiết: [Rules of thumb](rules-of-thumb).

---

## Tìm theo vai trò?

Bộ guide cũ theo vai trò (Developer, Tech Lead, QA…) đã chuyển sang
[**Archived (by persona)**](archive/) — vẫn đọc được, nhưng cách chính giờ là
theo loại project ở trên.
