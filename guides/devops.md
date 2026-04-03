---
layout: default
title: DevOps Workflows — My Agent Kit
---

# DevOps Workflows

CI/CD, Docker, hotfix — infrastructure automation.

[← Tất cả guides](.)

---

## 25. Setup CI/CD

> "Project chưa có pipeline, cần setup GitHub Actions"

### Bước 1 — Plan

```
/mk:plan "setup CI/CD with GitHub Actions: lint, test, build, deploy to Railway"
```

Kit analyze project stack, tạo plan phù hợp.

### Bước 2 — Implement

```
/mk:cook plans/260403-cicd/plan.md
```

Kit tạo:
- `.github/workflows/ci.yml` — lint + test on every PR
- `.github/workflows/deploy.yml` — deploy on merge to main
- Environment secrets setup instructions

### Bước 3 — Test pipeline

```
/mk:git cp
```

Push code, xem GitHub Actions chạy. Nếu fail:

```
/mk:fix "CI pipeline failing: jest not found in GitHub Actions"
```

### Bước 4 — Document

```
/mk:docs update
```

Kit tạo `docs/deployment-guide.md` với pipeline diagram, secrets cần setup, rollback steps.

---

## 26. Dockerize project

> "Cần đóng gói Docker lần đầu"

### Bước 1 — Generate Dockerfile

```
/mk:cook "create Dockerfile and docker-compose.yml: Node.js app + PostgreSQL + Redis"
```

Kit tạo:
- Multi-stage `Dockerfile` (build + production)
- `docker-compose.yml` với services
- `.dockerignore`

### Bước 2 — Test

```
/mk:test
```

Kit verify: Docker build thành công, app start đúng, health check pass.

### Bước 3 — Optimize

```
/mk:fix "optimize Docker image size, currently 1.2GB"
```

Kit optimize: multi-stage build, alpine base, layer caching, remove dev dependencies.

### Bước 4 — Deploy

```
/mk:deploy
```

Kit detect Dockerfile → gợi ý Fly.io / Railway / TOSE.sh → deploy.

---

## 27. Hotfix production

> "Production down, cần fix gấp"

### Bước 1 — Debug

```
/mk:debug "production 500 error on /api/checkout since last deploy"
```

Kit phân tích: recent commits, error logs, stack traces → tìm root cause.

### Bước 2 — Fix

```
/mk:fix --quick "null pointer in checkout handler after migration"
```

`--quick` mode: scout → diagnose → fix → test. Nhanh nhất có thể.

### Bước 3 — Ship hotfix

```
/mk:ship
```

Kit tự: run tests → create PR → (bạn merge) → deploy.

### Bước 4 — Post-mortem

```
/mk:docs update
```

Kit ghi lại: root cause, fix applied, prevention measures vào docs.

### Tips

- Luôn chạy `/mk:test` trước khi ship hotfix — đừng tạo bug mới.
- Dùng `/mk:fix --review` nếu fix liên quan đến payment/auth — cần review trước khi deploy.
