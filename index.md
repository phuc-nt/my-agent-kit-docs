---
layout: default
title: Installation
nav_order: 1
description: "Install My Agent Kit — 14 agents, 90+ skills, 20+ hooks for Claude Code."
permalink: /
---

# My Agent Kit
{: .fs-9 }

AI coding agent kit — 14 agents, 90+ skills, 20+ hooks, structured workflows.
{: .fs-6 .fw-300 }

Built for **Claude Code**, with cross-tool support for GitHub Copilot, Codex CLI, Cursor, Windsurf, and others.

[Get started — npx my-agent-kit init](#install){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[npm](https://www.npmjs.com/package/my-agent-kit){: .btn .fs-5 .mb-4 .mb-md-0 }

---

## Tính năng nổi bật

- **14 agents** — chuỗi chuyên trách: planner → fullstack-developer → code-simplifier → tester → code-reviewer, cùng researcher / debugger / git-manager gọi khi cần
- **90+ skills** — `cook`, `mk:plan`, `mk:fix`, `mk:test`, `mk:debug`, `mk:ship`, `docs-seeker`, `scout`, `sequential-thinking`… bật theo task
- **20+ hooks** — tự động hóa theo sự kiện (session-init, privacy-block, dev-rules-reminder…)
- **`fix` pipeline** — root cause → repro → minimal fix → regression test
- **Statusline config-driven** — theme parity giữa chế độ compact / minimal / full
- **Workflow guides theo loại project** — chọn đúng skill cho CLI / web / infra → xem [Workflow Guides](guides/)
- **Cross-tool** — Claude Code đầy đủ; Copilot, Codex CLI, Cursor, Windsurf qua `CLAUDE.md` / `AGENTS.md`

---

## Install

### Via npx (recommended)

```bash
# Vào project của bạn
cd /path/to/your-project

# Cài kit (Claude Code only)
npx my-agent-kit init

# Hoặc cài với hỗ trợ đa tool (Copilot + Codex)
npx my-agent-kit init --all

# Xem trước sẽ tạo gì
npx my-agent-kit init --dry-run
```

### Options

| Flag | Mô tả |
|---|---|
| `--dry-run` | Xem trước, không cài |
| `--force` | Ghi đè nếu đã cài trước đó |
| `--upgrade` | Clean upgrade — xóa các file cũ đã bị loại bỏ trước khi copy bản mới |
| `--skills-install` | Cài thêm Python dependencies cho AI skills |
| `--copilot` | Tạo `.github/copilot-instructions.md` |
| `--codex` | Tạo `.codex/config.toml` + `.agents/skills/` symlink |
| `--all` | Bật tất cả cross-tool configs |

---

## Sau khi cài

Project sẽ có:

```
your-project/
├── .claude/          ← 14 agents, 90+ skills, 20+ hooks, rules
├── CLAUDE.md         ← Instructions cho Claude Code + Copilot
├── AGENTS.md         ← Instructions cho Codex CLI + 6 tools khác
├── plans/            ← Thư mục kế hoạch
├── .github/          ← (nếu --copilot hoặc --all)
├── .codex/           ← (nếu --codex hoặc --all)
└── .agents/skills/   ← (nếu --codex hoặc --all) symlink → .claude/skills/
```

---

## Setup project đầu tiên

### 1. Thêm context vào CLAUDE.md

Mở `CLAUDE.md` trong project, thêm ở cuối:

```markdown
## My Project
- Stack: Node.js + React + PostgreSQL
- Style: functional, prefer composition over inheritance
- Testing: Jest + React Testing Library
- Deploy: Docker on AWS ECS
- Conventions: camelCase, 2-space indent, ESM imports
```

AI tự điều chỉnh code style, testing, deploy strategy theo context này.

### 2. Khởi động

```bash
claude                    # Claude Code
codex                     # Codex CLI (nếu đã cài --codex)
```

### 3. Generate docs

```
/mk:docs init
```

AI scan codebase và tạo documentation trong `docs/`.

### 4. (Tùy chọn) Python dependencies

```bash
cd .claude/skills && bash install.sh
```

Cần cho skills: `ai-multimodal`, `media-processing`, `stitch`, `design`.

### 5. (Tùy chọn) Copilot trong VS Code

Thêm vào VS Code `settings.json`:

```json
{
  "github.copilot.chat.codeGeneration.useInstructionFiles": true
}
```

Copilot sẽ tự đọc `CLAUDE.md`, `.claude/rules/`, `.claude/skills/`.

---

## Các lệnh hay dùng

| Lệnh | Khi nào dùng |
|---|---|
| `/mk:cook "feature X"` | Implement feature mới (plan → code → test → review) |
| `/mk:fix "bug Y"` | Gặp bug cần fix |
| `/mk:test` | Chạy tests + xem coverage |
| `/mk:code-review` | Review code trước khi merge |
| `/mk:ship` | Ship to production (test → review → commit → push → PR) |
| `/mk:plan "task"` | Lên kế hoạch trước khi làm task phức tạp |
| `/mk:docs init` | Tạo docs cho project |

---

## Tips

### Nên làm

- **Viết CLAUDE.md càng cụ thể càng tốt** — AI đọc file này mỗi lần bạn gõ prompt. Càng rõ context → AI càng chính xác.
- **Bắt đầu task lớn bằng `/mk:plan`** — AI chia nhỏ thành phases, dễ track và rollback.
- **Dùng `/mk:cook` thay vì prompt thủ công** — tự chạy pipeline plan → code → test → review.
- **Xóa skills không dùng** cho gọn:
  ```bash
  rm -rf .claude/skills/shopify .claude/skills/threejs .claude/skills/shader
  ```

### Không nên làm

- **Đừng sửa trực tiếp `.claude/`** trừ khi hiểu cấu trúc — dùng `/mk:help` để xem hướng dẫn.
- **Đừng commit secrets** — `.claude/.env` và `.claude/skills/.venv/` nên nằm trong `.gitignore`.
- **Đừng viết CLAUDE.md quá dài** — mỗi dòng thêm = thêm token mỗi turn. Ngắn gọn, đúng trọng tâm.

### Khi bị stuck

- `/mk:problem-solving` — 6 kỹ thuật phá bế tắc
- `/mk:debug` — Deep debugging với root cause analysis
- `/mk:autoresearch` — AI tự chạy loop tối ưu metric (ví dụ: tăng coverage lên 80%)

---

## Cập nhật kit

```bash
# Clean upgrade — drops files đã bị loại bỏ ở phiên bản mới
npx my-agent-kit init . --upgrade --force

# Hoặc full reinstall (mất customizations trong .claude/)
npx my-agent-kit init --force
```

> **Lưu ý:** `CLAUDE.md` sẽ bị ghi đè khi dùng `--force` — backup trước nếu đã customize.

`--upgrade` đọc danh sách file đã loại bỏ và dọn sạch trước khi copy bản mới,
nên không để lại rác từ lần cài cũ.

---

## Cross-Tool Support

| Tool | Đọc gì | Hỗ trợ |
|---|---|---|
| **Claude Code** | `CLAUDE.md` + full `.claude/` | Đầy đủ (14 agents, 90+ skills, 20+ hooks) |
| **GitHub Copilot** | `CLAUDE.md` + `.claude/rules/` + `.claude/skills/` | Native từ VS Code 1.108 |
| **Codex CLI** | `AGENTS.md` + `.codex/config.toml` + `.agents/skills/` | Qua config + symlink |
| **Cursor / Windsurf** | `AGENTS.md` | Chỉ instructions |

---

## Workflow Guides

Hướng dẫn **theo loại project** — đọc [Lõi bất biến](guides/core) trước
(5-agent chain + ~9 skill lõi xử lý ~90% mọi project), rồi thêm theo loại:

**[→ Xem tất cả Workflow Guides](guides/)**

| Loại project | Khi nào |
|---|---|
| [Lõi bất biến](guides/core) | Đọc đầu tiên — đúng cho mọi project |
| [CLI / single-binary](guides/cli-tool) | Tool dòng lệnh, spec-locked, binary tĩnh |
| [Web full-stack](guides/web-fullstack) | React/Next + API + DB |
| [Infra / DevOps](guides/infra-devops) | CI/CD, container, cloud, IaC, incident |
| [Rules of thumb](guides/rules-of-thumb) | Nguyên tắc áp cho mọi loại |

> Bộ guide cũ theo vai trò (Developer, Tech Lead, QA…) đã chuyển sang
> [Archived (by persona)](guides/archive/).

---

## Links

- **npm:** [npmjs.com/package/my-agent-kit](https://www.npmjs.com/package/my-agent-kit)
