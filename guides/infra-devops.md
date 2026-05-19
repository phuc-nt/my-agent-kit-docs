---
layout: default
title: Infra / DevOps
parent: Workflow Guides
nav_order: 4
---

# Infra / DevOps / deploy

{: .no_toc }

Đặc trưng: "implementation" thường là config + pipeline, không phải app code.
Verification và root-cause analysis chiếm phần lớn — **debugger-heavy**, ít
phần build chain.

[← Web full-stack](web-fullstack) · [Tiếp: Rules of thumb →](rules-of-thumb)

---

## Lõi áp dụng — nhưng trọng tâm dịch về verify

5-agent chain vẫn đúng (xem [Lõi](core)), nhưng `tester` validate bằng
pipeline run thật, không phải unit test; `debugger` thường là agent *đầu tiên*.

| Khi | Dùng |
|---|---|
| CI/CD, container, cloud config | `devops`, `deploy` |
| Security posture / scanning | `security-scan`, `mk:security` |
| Điều tra pipeline hỏng / sự cố prod | `debugger` agent + `mk:debug` + `sequential-thinking` (skill dẫn ở đây) |
| Thay đổi IaC / config | chain chuẩn, nhưng `tester` validate qua pipeline run thật |
| Postmortem / decision record | `journal` (`journal-writer` agent) cho sự cố đáng ghi |
| Capture môi trường tái lập | `repomix` / `docs-manager` cho runbook |

### Skill bổ sung hữu ích cho infra (ngoài tài liệu gốc)

| Skill | Vì sao hợp infra/DevOps |
|---|---|
| `mk:ship` | chuẩn hóa bước release/promote có review gate trước khi đụng prod |
| `docs-seeker` | cú pháp provider (Terraform/K8s/cloud SDK) đổi liên tục — tra thay vì đoán |
| `sequential-thinking` | sự cố prod là suy luận nhân-quả nhiều bước; đây là skill *dẫn* |
| `code-review` | review config với góc nhìn blast-radius + reversibility |

---

## Thứ tự chain cho infra

```
[có gì đã hỏng?] ─▶ debugger (luôn gọi trước)
researcher ─▶ planner ─▶ fullstack-developer (config/IaC)
          ─▶ tester (validate bằng pipeline run) ─▶ code-reviewer (security + blast-radius)
```

---

## Bỏ / cờ cẩn trọng

- **Bỏ:** toàn bộ skill frontend/mobile/design/media.
- **Cờ đỏ:** thay đổi infra có **blast-radius cao** — confirm trước hành động
  phá hủy hoặc đụng shared-state; dựa vào `code-reviewer` cho security +
  khả năng đảo ngược. Không bao giờ tự ý destructive trên shared env.

---

[← Web full-stack](web-fullstack) · [Tiếp: Rules of thumb →](rules-of-thumb)
