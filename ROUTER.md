# ROUTER.md — Knowledge Router（知识路由）

> 更新：2026-08-09 ｜ 维护：管理codex
> 用途：回答「这个任务，去哪里找知识 / 读哪个记忆」。只做路由，不装知识。

## 0. 判断顺序
1. 这是 **How to work**（方法/规则）？→ Global：`~/.codex/AGENTS.md` + 管理codex 仓库
2. **多个项目可能复用**？→ Shared：`/Users/fqt/Documents/Shared/`
3. **只属于一个项目**？→ Project Local（见 §4）
4. 是**个人偏好/习惯/历史经验**？→ Memory（见 §3）

## 1. GLOBAL（方法）
| 内容 | 位置 |
|---|---|
| 全局规则 | `~/.codex/AGENTS.md` |
| 系统规范（Canonical，禁止自动加载） | 管理codex/CODEX_OS.md（按 TOC 定位章节） |
| 系统架构/审计基线 | 管理codex/CURRENT_ARCHITECTURE.md |
| 系统级决策 | 管理codex/DECISIONS.md |
| 系统升级待办 | 管理codex/TODO.md |
| Handoff 模板 | 管理codex/HANDOFF.md |

## 2. SHARED（复用知识，按需读取）
| 领域 | 位置 | 当前内容 / 候选 |
|---|---|---|
| finance | /Users/fqt/Documents/Shared/finance/ | INDEX.md；候选：DCF 模板、投资分析方法 |
| content | /Users/fqt/Documents/Shared/content/ | INDEX.md；候选：小红书通用方法 |
| ai | /Users/fqt/Documents/Shared/ai/ | INDEX.md；候选：AI Agent 方法论 |
| （新领域） | /Users/fqt/Documents/Shared/<领域>/INDEX.md | 出现第二个项目复用时再建，禁止预先铺满 |

## 3. MEMORY（记忆路由，按领域读取）
| 领域 | 位置 | 说明 |
|---|---|---|
| 投资研究 | /Users/fqt/Documents/投资研究/memory/ | KK Trading Alpha 项目记忆（AGENTS.md/TODO/people/projects/notes） |
| 视频剪辑/Creator OS | /Users/fqt/Documents/ChatGPT/视频剪辑/context/ | 项目单源知识（creator/audience/brand/content/analytics） |
| 系统管理 | 管理codex/DECISIONS.md + TODO.md | 本系统决策与待办 |
| 全局个人偏好 | 管理codex/GLOBAL_MEMORY.md | 跨项目稳定偏好（语言/数据真实性） |

## 4. PROJECT（业务，各项目自治）
| 项目 | 位置 | 入口 |
|---|---|---|
| 投资研究 | /Users/fqt/Documents/投资研究/ | AGENTS.md |
| 视频剪辑 | /Users/fqt/Documents/ChatGPT/视频剪辑/ | AGENTS.md（Router 式） |
| AI落地 | /Users/fqt/Documents/ChatGPT/AI落地/ | AI产品商业化落地研究报告.md |
| 数据分析训练 | /Users/fqt/Documents/ChatGPT/数据分析训练/ | 求职准备计划.md / DCF/ |
| 产品经理训练 | /Users/fqt/Documents/ChatGPT/产品经理训练/ | README.md |
| 英语培训 | /Users/fqt/Documents/ChatGPT/英语培训/ | （未激活，不建 AGENTS） |
| 表达能力提升 | /Users/fqt/Documents/ChatGPT/表达能力提升/ | （未激活，不建 AGENTS） |
| 销售训练 | /Users/fqt/Documents/ChatGPT/销售训练/ | （未激活，不建 AGENTS） |
