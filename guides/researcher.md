---
layout: default
title: Researcher Workflows — My Agent Kit
---

# Researcher Workflows

Phân tích code, xử lý documents, research kỹ thuật.

[← Tất cả guides](.)

---

## 31. Phân tích codebase lạ

> "Cần hiểu repo open-source 50k+ lines để contribute"

### Bước 1 — Generate overview

```
/mk:docs init
```

Kit scan toàn bộ repo: file structure, dependencies, entry points, patterns → tạo docs.

### Bước 2 — Deep dive

Hỏi cụ thể:

```
Giải thích kiến trúc plugin system trong repo này
```

```
Vẽ diagram data flow từ API request đến database
```

```
/mk:preview --diagram "request lifecycle from HTTP to database"
```

### Bước 3 — Tìm entry point để contribute

```
/mk:plan "add support for WebSocket connections to the existing HTTP server"
```

Kit phân tích existing architecture, đề xuất cách thêm feature mà không break patterns.

### Tips

- Bắt đầu bằng `docs/system-architecture.md` sau khi chạy `/mk:docs init`.
- Hỏi "file nào handle X?" trước khi đọc code — kit trả lời nhanh hơn đọc thủ công.

---

## 32. Xử lý documents hàng loạt

> "100 PDF invoices, cần extract data thành spreadsheet"

### Bước 1 — Extract từ PDF

```
/mk:cook "read all PDF files in ./invoices/, extract: invoice number, date, amount, vendor name. Save as invoices.xlsx"
```

Kit dùng pdf skill để: parse PDF → extract text/tables → structure data → export Excel.

### Bước 2 — Verify

```
Kiểm tra 5 dòng đầu trong invoices.xlsx có đúng với PDF gốc không
```

### Các format khác

**Word → structured data:**
```
/mk:cook "extract all section headings and tables from contract.docx, save as markdown"
```

**Excel analysis:**
```
/mk:cook "analyze sales.xlsx: monthly revenue trend, top 10 products, year-over-year comparison. Create summary report."
```

**PowerPoint → docs:**
```
/mk:cook "extract all text and speaker notes from presentation.pptx, save as markdown document"
```

### Lưu ý

Cần cài Python dependencies trước:

```bash
cd .claude/skills && bash install.sh
```

---

## 33. Research kỹ thuật

> "So sánh 3 database options cho project mới"

### Bước 1 — Research

```
/mk:brainstorm "database for real-time analytics: PostgreSQL vs ClickHouse vs TimescaleDB. Consider: query speed, write throughput, operational complexity, cost, ecosystem."
```

Kit phân tích pros/cons từ nhiều góc: performance, operations, cost, developer experience.

### Bước 2 — Structured analysis

```
/mk:plan "evaluate and select database for real-time analytics dashboard"
```

Kit tạo comparison matrix:

| Criteria | PostgreSQL | ClickHouse | TimescaleDB |
|---|---|---|---|
| Write throughput | ★★★ | ★★★★★ | ★★★★ |
| Query speed | ★★★ | ★★★★★ | ★★★★ |
| Ops complexity | ★★ | ★★★★ | ★★★ |
| Cost | ★★ | ★★★ | ★★★ |
| Ecosystem | ★★★★★ | ★★★ | ★★★★ |

### Bước 3 — Risk assessment

```
/mk:predict "choosing ClickHouse for real-time analytics in a small team"
```

5 experts flag risks: operational overhead, hiring difficulty, migration complexity.

### Bước 4 — Document decision

```
/mk:docs update
```

Kit lưu decision record vào `docs/` — lý do chọn, alternatives considered, trade-offs accepted.
