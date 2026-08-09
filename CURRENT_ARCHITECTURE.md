# CURRENT_ARCHITECTURE.md — Codex 系统现状图
> 🔄 2026-08-09 (O4)：moomooapi / install-moomoo-opend / LEGAL 已从全局迁移至 投资研究/.agents/skills 与 docs/legal（本快照为迁移前状态）。

> 更新：2026-08-09 ｜ 维护：管理codex（本仓库）
> 用途：记录当前三层架构（Global / Shared / Project / Memory）的**实际状态**与标注，作为一切升级决策的基线。
> 原则：本文只描述现状 + 问题，不写方案。方案见文末「Delta Upgrade 摘要」（详细执行另行确认）。

---

## 1. 总览（一句话）

当前系统只有 **Global（~/.codex）** 和 **Project（8 个项目 + 投资研究）** 两层；
**Shared Knowledge 层完全不存在**；Memory 实际挂在「投资研究/memory/」下并被全局规则引用（位置错位）。

---

## 2. GLOBAL 层（How we work）

### 2.1 `~/.codex/AGENTS.md`（已存在，1.2KB）
内容：
- 第二大脑记忆协议 → 指向 `/Users/fqt/Documents/投资研究/memory/`
- 用户偏好：中文；真实数据；分析风格（swing high / swing low）
- 项目级规则入口：仅 KK Trading Alpha

问题标注：
- ⚠️ **记忆区位置错位**：全局规则把「中心记忆区」绑定在单个投资项目（投资研究/memory/）的子目录。按新体系，Memory 应与具体项目解耦，或至少独立于投资研究。
- ⚠️ **投资专用偏好混入 Global**：「swing high / swing low 结构评分」是投资分析方法，不属于「所有项目通用的 How to work」，应归 Shared/finance 或投资研究项目。
- ❌ **缺 Knowledge Router 引用**：系统 prompt 定义了 Router 概念，但 Global 层无任何落盘入口文件。
- ❌ **缺 Handoff / Agent Routing / Shared 约定**：全部只有系统 prompt 里的理念，未落盘。

### 2.2 `~/.codex/config.toml`（已存在）
- model：deepseek-v4-flash（custom provider，本地代理）
- MCP：node_repl（启用）、computer-use（禁用）
- plugins 启用 13 个：github / gmail / browser / visualize / sites / documents / pdf / spreadsheets / presentations / template-creator / chrome / computer-use
- trusted projects（7 个）：投资研究、数据分析训练、产品经理训练、英语培训、视频剪辑、AI落地、管理codex
- 问题：⚠️ **trusted 缺失 2 个已建项目**：表达能力提升、销售训练（目录存在但不在 trusted 列表）。

### 2.3 `~/.codex/skills/`（用户级 skills）
- `.system/`（官方系统 skills）：imagegen / openai-docs / plugin-creator / review-agent / skill-creator / skill-installer
- 用户自装（当前实际位置）：
  - `moomooapi`、`install-moomoo-opend` → **投资专用**（moomoo 行情/交易）
  - `pdf`、`playwright` → 通用工具
- 散文件：`LEGAL_MooMoo_api_cn/en.md`、`LEGAL_zh.md` → moomoo 法律文件，**投资专用**，不应散在全局目录。

标注：
- ⚠️ 投资专用 skills 与通用 skills 混放在全局 `~/.codex/skills/`，无分类。
- ❌ 缺全局通用工作方法 skills（web-research / source-verification / handoff / context-management / decision-log / research-cache 等均未创建）。

### 2.4 `~/.agents/`
- ❌ **不存在**（系统 prompt 提到的 `$HOME/.agents/skills/` 目前没有该目录）。
- ✅ 但项目级 `.agents/skills/` 已被使用（视频剪辑/Creator OS 有 5 个项目 skill）。

---

## 3. SHARED 层（Multiple projects may need this knowledge）

- ❌ **完全不存在**。没有 shared/ 目录、没有共享知识索引。
- 已识别但未沉淀的共享候选（散落在各项目里）：
  - 小红书平台通用方法 → 目前只在 视频剪辑 项目（.agents/skills/xiaohongshu-research 等）——按规则应部分提升为 Shared/content
  - DCF 模型模板（数据分析训练/DCF/*.xlsx + 手把手教学.md）→ Shared/finance
  - 产品经理模板（产品经理训练/模板/*.md）→ Shared（如多项目复用才迁移）
  - 投资分析方法（memory/notes/*.md：摆动高低点、市场主线判断、技术形态）→ Shared/finance 或投资研究项目
  - AI Agent 方法论（AI落地 报告中的可复用部分）→ Shared/ai

---

## 4. PROJECT 层（What this project is）

| 项目 | 路径 | 状态 | AGENTS.md | 自定义 Agent | 项目 Skill | 知识/产出 | 备注 |
|---|---|---|---|---|---|---|---|
| 投资研究 (KK Trading Alpha) | Documents/投资研究 | 最成熟（应用+研究） | ✅ 有 | 无 | 无（用全局 moomooapi） | README / PROGRESS / docs / output / memory/ | ⚠️ 兼当全局记忆区（错位） |
| 视频剪辑 (Creator OS) | Documents/ChatGPT/视频剪辑 | 系统范式最完整 | ✅ Router 式 | 6 个 (.codex/agents) | 5 个 (.agents/skills) | context/ + artifacts/ + cache/ + raw/ + scripts/ + templates/ | 参考架构；含小红书业务知识 |
| AI落地 | Documents/ChatGPT/AI落地 | 仅 1 份大报告（103KB） | ❌ | 无 | 无 | AI产品商业化落地研究报告.md | 报告含大量可提炼 Shared/ai 内容 |
| 数据分析训练 | Documents/ChatGPT/数据分析训练 | 教学资料 | ❌ | 无 | 无 | DCF 教学 + 求职/简历 | DCF 模板可提升 Shared/finance |
| 产品经理训练 | Documents/ChatGPT/产品经理训练 | 教学资料 | ❌ | 无 | 无 | README + 模板/ + 拆解/ | 模板可提升 Shared |
| 英语培训 | Documents/ChatGPT/英语培训 | 空仓库（仅 .git） | ❌ | 无 | 无 | — | 等有内容再建 |
| 表达能力提升 | Documents/ChatGPT/表达能力提升 | 空仓库（仅 .git） | ❌ | 无 | 无 | — | 等有内容再建；⚠️ 未 trusted |
| 销售训练 | Documents/ChatGPT/销售训练 | 空仓库（仅 .git） | ❌ | 无 | 无 | — | 等有内容再建；⚠️ 未 trusted |
| 管理codex（本仓库） | Documents/ChatGPT/管理codex | 空（仅 .git，无提交） | ❌ | 无 | 无 | — | 本次起建立系统文档 |

---

## 5. MEMORY 层

| 位置 | 状态 | 标注 |
|---|---|---|
| 投资研究/memory/ | ✅ 最完整（AGENTS.md 协议 + TODO + people/ + projects/ + notes/ + agent/） | ⚠️ 当前被全局指定为中心记忆区——位置错位，但**内容质量好**，不要重建 |
| ~/.codex/memories/ + memories_1.sqlite | Codex 内置记忆（目录空） | 官方机制，未利用 |
| Obsidian Vault | 几乎空（欢迎.md + 创建链接.md） | 用户提到「已有 Second Brain」——实际内容尚未进入，或指的就是 投资研究/memory |

---

## 6. 内容标注（GLOBAL / SHARED / PROJECT / MEMORY / ARCHIVE）

| 现有内容 | 现状位置 | 应属层级 | 动作倾向 |
|---|---|---|---|
| 第二大脑记忆协议（浏览/更新/TODO 流程） | ~/.codex/AGENTS.md | GLOBAL（方法） | KEEP，但把"记忆区位置"与投资研究解耦 |
| 语言/数据真实性偏好 | ~/.codex/AGENTS.md | GLOBAL | KEEP |
| swing high/low 分析风格 | ~/.codex/AGENTS.md | SHARED/finance 或 PROJECT/投资研究 | MOVE（从 Global 移出） |
| 投资研究/memory 全部内容 | 投资研究/memory/ | MEMORY（内容保留） | KEEP 内容；重新定义"全局记忆区"的位置归属 |
| moomooapi / install-moomoo-opend skills | ~/.codex/skills/ | PROJECT/投资研究 或 SHARED/finance | MOVE 或标注（验证后再动） |
| LEGAL_MooMoo_* 文件 | ~/.codex/skills/ | PROJECT/投资研究 | MOVE（归档到投资研究或 shared/finance/legal） |
| 视频剪辑 xiaohongshu-research 等 skill | 视频剪辑/.agents/skills/ | PROJECT/视频剪辑（平台通用部分可提升 SHARED/content） | KEEP；后续做「提升」评估 |
| DCF 模板/教学 | 数据分析训练/DCF/ | SHARED/finance（如多项目复用） | 待定（MERGE 候选） |
| 产品经理模板 | 产品经理训练/模板/ | SHARED（如多项目复用） | 待定 |
| 各空项目 | 各自仓库 | PROJECT（未激活） | ARCHIVE 级：不建 AGENTS，等激活 |
| AI落地 大报告 | AI落地/*.md | PROJECT/AI落地 + 可提炼 SHARED/ai | KEEP；提炼候选 |

---

## 7. 重复 / Context Waste / Agent Overuse 检查

**重复内容：**
- 「记忆协议」在 ~/.codex/AGENTS.md 与 投资研究/AGENTS.md 与 memory/AGENTS.md 三处重复（内容一致，可接受为逐层入口，但要确认不漂移）。
- 「用户偏好」在 ~/.codex/AGENTS.md 与 投资研究/AGENTS.md 重复。

**Context Waste：**
- 无 shared 层 → 跨项目知识只能整份复制或整份重读（AI落地 103KB 报告、投资研究 memory 每次全读）。
- 空项目无 AGENTS → 无污染（良好）。

**Agent Overuse：**
- 当前实际只有 视频剪辑 定义了 6 个项目 Agent（Director 判断后显式调用）——用量合理，无过度。

**Token 隐患：**
- 系统 prompt 已注入 30 节长文（本对话的这套规则），尚未落盘成文件 → 每次会话靠人肉粘贴，易漂移、耗 token。**落盘后应改为引用式。**

---

## 8. Delta Upgrade 摘要（详见讨论，确认后执行）

- **KEEP**：投资研究/memory 内容与协议、视频剪辑 整体架构、~/.codex 现有配置、现有官方 skills。
- **IMPROVE**：~/.codex/AGENTS.md（移除投资专用偏好、解除记忆区与投资研究的强绑定、加 Router 入口）；config.toml trusted 补 2 项。
- **ADD**：管理codex 仓库 = 系统控制台（ROUTER.md、GLOBAL_RULES.md、HANDOFF.md、DECISIONS.md、TODO）；Shared Knowledge 目录骨架 + 索引；通用方法 skills（按需渐进）。
- **MOVE（验证后）**：moomoo skills/LEGAL 归位；投资分析方法 → Shared/finance。
- **MERGE（候选）**：DCF 模板 / 产品经理模板 → Shared。
- **REMOVE**：无（当前无确认要删的内容；空目录仅标记 ARCHIVE）。
