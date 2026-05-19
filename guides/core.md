---
layout: default
title: Lõi bất biến
parent: Workflow Guides
nav_order: 1
---

# Lõi bất biến — mọi project, ~90% thời gian

{: .no_toc }

Kit chia làm **agents** (ai *làm* việc — agent viết code) và **skills**
(kiến thức/quy trình agent theo khi làm). Cả hai đều là lõi; code do **agent**
viết, không phải skill.

[← Workflow Guides](./) · [Tiếp: CLI tool →](cli-tool)

---

## 1. Agents — xương sống (chính những con này tạo ra code)

**Chuỗi tuần tự** — mỗi agent hoàn tất hẳn rồi mới sang con kế:

| Agent | Vai trò trong build |
|---|---|
| `planner` | biến spec thành `plan.md` + phase files (không redesign spec) |
| **`fullstack-developer`** | **viết code thực tế** — backend, frontend, infra; con ngựa kéo |
| `code-simplifier` | dọn dẹp giữ nguyên hành vi (DRY/KISS), không đụng contract đã khóa |
| `tester` | test code đã simplify; chỉ sở hữu file test, không sửa impl |
| `code-reviewer` | cổng chất lượng: đúng-vs-spec, security, robustness |

```
planner ─▶ fullstack-developer ─▶ code-simplifier ─▶ tester ─▶ code-reviewer
  spec       viết code              dọn (giữ hành vi)   test     quality gate
```

Thêm **3 agent gọi khi cần**:

| Agent | Khi nào |
|---|---|
| `researcher` | trước khi plan — gom nhiều topic song song |
| `debugger` | có bug / CI đỏ |
| `git-manager` | commit/push — conventional, không ref AI |

> Nếu phân vân "cái gì viết code?" → **`fullstack-developer`**. Các skill bên
> dưới là cái nó (và bạn) theo khi làm.

---

## 2. Skills lõi — quy trình quanh code (bật cho gần như mọi việc)

| Skill | Khi nào | Đi cặp với |
|---|---|---|
| **`cook`** | **LUÔN trước khi implement bất kỳ feature/plan/fix** — kỷ luật viết code | `fullstack-developer` |
| `mk:plan` | plan + chia phase trước việc không tầm thường | `planner` |
| `scout` | định vị code / gom context nhanh trước khi sửa | `fullstack-developer`, `debugger` |
| `sequential-thinking` | suy luận nhiều bước / phân tích / triage | bất kỳ |
| `mk:debug` / `fix` | điều tra & sửa defect hoặc CI fail | `debugger` |
| `test` | chiến lược test trên code đã simplify | `tester` |
| `code-review` | cổng chất lượng trước merge | `code-reviewer` |
| `git` | thao tác git an toàn | `git-manager` |
| `docs-seeker` | tra docs *hiện tại* của thư viện (context7) thay vì đoán API | `researcher`, `fullstack-developer` |

`backend-development` / `frontend-development` là skill **chuẩn-code theo
ngôn ngữ/stack** — là lõi *cho stack đó* (xem [Web full-stack](web-fullstack)),
tình huống ở chỗ khác.

> Nhớ 5-agent chain + `cook` + nhóm skill này là làm được ~90% mọi build.
> Mọi thứ còn lại là tình huống — chỉ thêm khi loại project gọi tới.

---

## 3. Lệnh hay dùng (gói lõi)

| Lệnh | Làm gì |
|---|---|
| `/mk:cook "feature X"` | pipeline đầy đủ plan → code → test → review |
| `/mk:plan "task"` | chia nhỏ task phức tạp thành phase |
| `/mk:fix "bug Y"` | điều tra + sửa với root-cause |
| `/mk:test` | chạy test + xem coverage |
| `/mk:code-review` | review trước merge |
| `/mk:debug` | deep debug, root-cause analysis |

---

[← Workflow Guides](./) · [Tiếp: CLI tool →](cli-tool)
