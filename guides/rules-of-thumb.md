---
layout: default
title: Rules of thumb
parent: Workflow Guides
nav_order: 5
---

# Rules of thumb — áp cho mọi loại project

{: .no_toc }

[← Infra/DevOps](infra-devops) · [Workflow Guides](./)

---

## 1. Match skill theo *task*, không theo *project*

Một web project vẫn **chưa** load `payment-integration` cho tới khi có việc
billing thật. Loại project chỉ gợi ý skill *có thể* cần — task quyết định skill
*thực sự* bật.

## 2. Một chain, thứ tự cố định

Không reorder `planner → fullstack-developer → code-simplifier → tester →
code-reviewer`. Chỉ được *thêm* pre-step:

```
[researcher] ─▶ [ui-ux-designer] ─▶ [debugger] ─▶ planner ─▶ … (chain chuẩn)
   trước plan      khi UX nặng        khi đã hỏng
```

## 3. Trust but verify — sau *mỗi* agent

Tự chạy lại build/test + một functional smoke. **Không bao giờ** ký duyệt chỉ
dựa trên bản tóm tắt của subagent.

## 4. Context isolation

Brief mỗi agent bằng **đường dẫn rõ ràng + đúng spec/section liên quan**, không
bao giờ bằng lịch sử hội thoại. Agent sạch context → kết quả ổn định hơn.

## 5. Phân vân có nên thêm skill → đừng

**Absence rẻ hơn sprawl.** Mỗi skill thừa = thêm context, chain chậm, nhiễu
quyết định. Thiếu một skill dễ sửa hơn gỡ rối một chain phình.

---

## Bảng quyết định nhanh

| Tình huống | Hành động |
|---|---|
| Sắp implement bất kỳ thứ gì | `cook` trước, luôn luôn |
| Việc không tầm thường | `mk:plan` chia phase trước |
| Không biết code ở đâu | `scout` trước khi sửa |
| Có bug / CI đỏ | `debugger` + `mk:debug` *trước* mọi thứ |
| Cần API thư viện chính xác | `docs-seeker` (context7), không đoán |
| Phân vân thêm skill X | Không thêm. Chờ task thực sự cần |
| Trước khi merge | `code-review` gate, không bỏ qua |
| Hành động phá hủy / shared-state | Confirm trước. `code-reviewer` soi reversibility |

---

[← Infra/DevOps](infra-devops) · [Workflow Guides](./)
