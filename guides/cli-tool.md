---
layout: default
title: CLI / single-binary
parent: Workflow Guides
nav_order: 2
---

# CLI tool — spec-locked, single binary

{: .no_toc }

Đặc trưng: spec là luật (agent implement, không redesign), một binary tĩnh,
ít/không phụ thuộc runtime, file nhỏ, version cộng dồn (additive). Ví dụ: CLI
viết bằng Go/Rust, embedded asset, SQLite no-CGO, vanilla JS/CSS cho dashboard.

[← Lõi](core) · [Tiếp: Web full-stack →](web-fullstack)

---

## Lõi vẫn áp dụng đầy đủ

5-agent chain + `cook`/`scout` khi code — xem [Lõi bất biến](core). Bảng dưới
chỉ là phần *thêm vào hoặc nhấn mạnh* cho stack này.

| Khi | Dùng | Ghi chú |
|---|---|---|
| Triage một BLOCKER của reviewer | `sequential-thinking` + `mk:debug` | spec-locked → lỗi thường là impl lệch spec, không phải spec sai |
| Giải thích kiến trúc khi demo | `/mk:preview --diagram` / `--explain` | chỉ cho demo/walkthrough, **không** trong lúc build |
| Commit | `git` / `git-manager` | conventional, không ref AI, không push trừ khi được yêu cầu |
| Đóng gói / release binary | `mk:ship` (giai đoạn cuối) | sau khi qua review gate |
| Đảm bảo file ≤ giới hạn dòng, không CGO… | `code-reviewer` | đưa ràng buộc spec vào brief của reviewer |

### Skill bổ sung hữu ích cho CLI (ngoài tài liệu gốc)

| Skill | Vì sao hợp CLI |
|---|---|
| `mk:plan` | spec-locked rất hợp plan theo phase cộng dồn — mỗi version một phase file |
| `docs-seeker` | tra API stdlib/thư viện chuẩn thay vì đoán (Go/Rust ít deps → sai API là tốn) |
| `repomix` | gói toàn repo nhỏ thành 1 context để brief agent — CLI repo thường đủ nhỏ để làm trọn |
| `journal` (`journal-writer`) | ghi lại quyết định kiến trúc giữa các version (vì sao chọn no-CGO…) |

---

## Cố tình KHÔNG dùng (skill sprawl / YAGNI cho stack này)

`frontend-design`, `ui-ux-pro-max`, `react-best-practices`, `tanstack`,
`web-frameworks`, `databases` (nếu schema khóa & nhỏ), `deploy`, `devops`,
`payment-integration`, `better-auth`, và nhóm mobile / shopify / stitch /
remotion / threejs / shader.

> Kéo bất kỳ cái nào ở trên vào một spec CLI đã khóa là **skill sprawl** — tốn
> context, không đổi lại gì. Spec nhỏ + binary tĩnh thì đơn giản là vũ khí.

---

## Thứ tự chain cho CLI

```
researcher? ─▶ planner ─▶ fullstack-developer ─▶ code-simplifier
            ─▶ tester ─▶ code-reviewer (nhấn: spec-compliance + ràng buộc binary)
debugger: gọi TRƯỚC nếu có cái gì đã hỏng
```

Không reorder chain. Chỉ *thêm* pre-step (researcher / debugger). `tester`
validate hành vi CLI thật (chạy binary với fixture), không chỉ unit test.

---

[← Lõi](core) · [Tiếp: Web full-stack →](web-fullstack)
