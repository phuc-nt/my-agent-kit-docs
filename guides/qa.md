---
layout: default
title: QA / Tester
parent: Workflow Guides
nav_order: 6
---

# QA / Tester Workflows

Viết tests, test UI, regression testing.

[← Tất cả guides](.)

---

## 22. Viết test suite từ đầu

> "Project chưa có tests, cần bắt đầu"

### Bước 1 — Scan codebase

```
/mk:scenario "test scenarios for the entire application"
```

Kit phân tích code, generate test scenarios across 12 dimensions: happy path, edge cases, error handling, security, performance, concurrency...

### Bước 2 — Generate tests tự động

```
/mk:autoresearch
```

Config:
- **Goal:** coverage 80%
- **Scope:** src/**/*.ts
- **Verify:** jest --coverage
- **Guard:** npm test (đảm bảo tests pass)
- **Iterations:** 30

Kit tự lặp: viết tests → chạy → giữ nếu coverage tăng → tiếp.

### Bước 3 — Review tests

```
/mk:code-review --pending
```

Kit review tests vừa generate: đảm bảo tests có ý nghĩa, không test implementation details.

### Tips

- Bắt đầu từ critical paths (auth, payment, data mutations).
- Kit sẽ không dùng mocks cho database — tests chạy thật.

---

## 23. Test UI across browsers

> "Cần test responsive + accessibility"

### Run UI tests

```
/mk:test ui http://localhost:3000
```

Kit sẽ:
1. Chụp screenshots ở nhiều viewport (mobile, tablet, desktop)
2. Kiểm tra responsive layout
3. Chạy accessibility audit (WCAG compliance)
4. Thu thập console errors
5. Test form submissions
6. Kiểm tra loading states

### Output

Kit xuất report với:
- Screenshots per viewport
- Accessibility violations (with severity)
- Console errors found
- Performance metrics

### Fix issues

```
/mk:fix "accessibility: missing alt text on images, form labels not associated"
```

---

## 24. Regression testing

> "Sau refactor, cần verify không break gì"

### Bước 1 — Chạy full test suite

```
/mk:test
```

Kit chạy: typecheck → unit tests → integration tests → e2e tests → coverage report.

### Bước 2 — So sánh coverage

Kit báo cáo:
- Tests pass/fail count
- Coverage % (so với trước refactor)
- Files với coverage giảm

### Bước 3 — Fix nếu có regressions

```
/mk:fix "test failures after refactoring auth module"
```

Kit phân tích: test fail vì code sai hay test cần update? Fix accordingly.

### Bước 4 — Verify lại

```
/mk:test
```

Lặp lại cho đến khi 100% pass, coverage không giảm.
