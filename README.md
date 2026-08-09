# Codex OS — 个人 Codex 工作系统架构（可复用模板）

一套把 **Codex（AI 编程助手）** 组织成「三层知识架构」的实战模板，作者本人正在使用。

> 核心理念：**共享能力，不共享无关上下文。**
> **GLOBAL 管方法 → SHARED 管复用知识 → PROJECT 管具体业务 → Memory 辅助 Recall。**
> 目标公式：`Maximum Useful Work / Minimum Token + Context + Repetition + Maintenance`

## 这是什么

把"用 AI 干活"从**每次重复解释、重复粘贴、重复研究**，变成**一次落盘、按需检索**的系统：

- 一个轻量 **Global 规则层**（`~/.codex/AGENTS.md`，只放所有项目都必须执行的 Runtime 规则，保持 <3KB）
- 一份 **Canonical 系统规范**（`CODEX_OS.md`：三层架构 / 路由 / Skills / Agents / Memory / Research Cache / Token 优化，按章节 TOC 按需读取，**禁止自动全文加载**）
- 一个 **Knowledge Router**（`ROUTER.md`：任务 → 去哪里找知识/记忆）
- 一套 **项目记忆协议**（简洁、带日期、可检查、git 可回滚）
- 一个 **Shared 共享层**（多项目复用知识，索引先行，不自动加载）
- 标准 **Handoff / DECISIONS / TODO** 控制台文件

## 文件地图

| 文件 | 作用 | 何时读 |
|---|---|---|
| `CODEX_OS.md` | 系统规范（Source of Truth） | 仅系统管理任务，按 TOC 定位章节 |
| `ROUTER.md` | 知识路由（任务→位置） | 每次重要会话前 |
| `HANDOFF.md` | 交接模板 | Agent/Thread 切换、会话结束 |
| `DECISIONS.md` | 系统级决策日志（Why） | 需要回顾决策时 |
| `TODO.md` | 系统升级待办 | 每次会话开始 |
| `GLOBAL_MEMORY.md` | 跨项目稳定的个人偏好 | 按需 |
| `CURRENT_ARCHITECTURE.md` | 系统现状审计（基线） | Audit 时 |
| `CURRENT_CODEX_ARCHITECTURE.md` | 实际架构图（含问题清单） | Audit 时 |

## 为什么这样设计（而不是更复杂）

- **Plain files + Markdown + Git**，不依赖数据库/向量检索/云端
- 规范是 **Reference，不是 Always-Loaded Context**——普通任务零感知
- 记忆/知识**按领域隔离**，一个项目不读取另一个项目的无关信息
- **脚本优先**：确定性工作用代码，LLM 只做推理
- **If it works, preserve it**：不为"最佳实践"增加复杂度

## 快速开始

1. 克隆本仓库作为你的控制台：`git clone <本仓库> 管理codex`
2. 读 `ADAPT.md`，把路径和项目名换成你自己的
3. 把 `CODEX_OS.md` 的「Reference」引用写进你的 `~/.codex/AGENTS.md`
4. 按 `ROUTER.md` 建立你的 Shared 目录和项目记忆
5. 第一次真实使用后，按 `CURRENT_CODEX_ARCHITECTURE.md` 的方法做一次你自己的 Audit

> 文中的 `/Users/fqt/...` 路径、项目名（投资研究/视频剪辑等）来自作者真实环境，仅作示例，见 `ADAPT.md`。
