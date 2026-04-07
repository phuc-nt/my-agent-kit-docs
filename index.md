---
layout: default
title: Installation
nav_order: 1
description: "Install My Agent Kit — 14 agents, 80+ skills, 15 hooks for Claude Code."
permalink: /
---

# My Agent Kit
{: .fs-9 }

AI coding agent kit — 14 agents, 80+ skills, 15 hooks, structured workflows.
{: .fs-6 .fw-300 }

Built for **Claude Code**, with cross-tool support for GitHub Copilot, Codex CLI, Cursor, Windsurf, and others.

[Get started — npx my-agent-kit init](#install){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[GitHub](https://github.com/phuc-nt/my-agent-kit){: .btn .fs-5 .mb-4 .mb-md-0 }

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

### Via git clone

```bash
git clone https://github.com/phuc-nt/my-agent-kit.git
cd my-agent-kit
./mk-init.sh /path/to/your-project --all
```

### Options

| Flag | Mô tả |
|---|---|
| `--dry-run` | Xem trước, không cài |
| `--force` | Ghi đè nếu đã cài trước đó |
| `--skills-install` | Cài thêm Python dependencies cho AI skills |
| `--copilot` | Tạo `.github/copilot-instructions.md` |
| `--codex` | Tạo `.codex/config.toml` + `.agents/skills/` symlink |
| `--all` | Bật tất cả cross-tool configs |

---

## Sau khi cài

Project sẽ có:

```
your-project/
├── .claude/          ← 14 agents, 80+ skills, 15 hooks, rules
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
npx my-agent-kit init --force       # Ghi đè .claude/ bằng bản mới nhất
```

> **Lưu ý:** `CLAUDE.md` sẽ bị ghi đè khi dùng `--force` — backup trước nếu đã customize.

---

## Cross-Tool Support

| Tool | Đọc gì | Hỗ trợ |
|---|---|---|
| **Claude Code** | `CLAUDE.md` + full `.claude/` | Đầy đủ (14 agents, 80+ skills, 15 hooks) |
| **GitHub Copilot** | `CLAUDE.md` + `.claude/rules/` + `.claude/skills/` | Native từ VS Code 1.108 |
| **Codex CLI** | `AGENTS.md` + `.codex/config.toml` + `.agents/skills/` | Qua config + symlink |
| **Cursor / Windsurf** | `AGENTS.md` | Chỉ instructions |

---

## Workflow Guides

33 hướng dẫn theo tình huống thực tế cho 9 vai trò:

**[→ Xem tất cả Workflow Guides](guides/)**

| Vai trò | Guides |
|---|---|
| [Developer](guides/developer) | Xây feature, fix bug, test, refactor, ship |
| [Solopreneur](guides/solopreneur) | MVP, landing page, payment |
| [Tech Lead](guides/tech-lead) | Review PR, plan sprint, security audit |
| [PM / Product](guides/pm) | PRD, feasibility, tracking |
| [Designer](guides/designer) | Design → code, UI review, design system |
| [QA / Tester](guides/qa) | Test suite, UI test, regression |
| [DevOps](guides/devops) | CI/CD, Docker, hotfix |
| [Tech Writer](guides/tech-writer) | API docs, slides, release notes |
| [Researcher](guides/researcher) | Codebase analysis, documents, research |

---

## Links

- **npm:** [npmjs.com/package/my-agent-kit](https://www.npmjs.com/package/my-agent-kit)
- **GitHub:** [github.com/phuc-nt/my-agent-kit](https://github.com/phuc-nt/my-agent-kit)
