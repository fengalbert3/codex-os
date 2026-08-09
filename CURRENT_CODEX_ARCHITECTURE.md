# CURRENT_CODEX_ARCHITECTURE.md — Codex 实际架构现状
> 🔄 2026-08-09 (O4)：全局 skills 已移除 moomooapi / install-moomoo-opend / LEGAL（迁至 投资研究 项目级）。

> 更新：2026-08-09（Phase 1 Audit，纯只读检查）｜ 维护：管理codex
> 依据：实际磁盘检查（~/.codex、/Users/fqt/Documents 下全部项目、memory、Shared、Obsidian），codex-cli 0.147.0-alpha.6.5。
> 本轮未做任何修改。所有发现仅记录。

---

## 1. 实际架构图

```
ME（用户）
│
▼
GLOBAL  ~/.codex/
│   ├─ AGENTS.md（全局规则，1.3KB，自动加载）
│   ├─ config.toml（deepseek-v4-flash / reasoning=high / 10 trusted / 12 plugins / MCP: node_repl）
│   ├─ skills/（全局可见）
│   │    ├─ .system/：imagegen · openai-docs · plugin-creator · review-agent · skill-creator · skill-installer
│   │    └─ 用户级：moomooapi(1.4M) · install-moomoo-opend · pdf · playwright
│   ├─ agents/ → 不存在
│   └─ memories/ → 空（sqlite 40KB 空库）
│
▼
SHARED  /Users/fqt/Documents/Shared/  ← 仅骨架
│   ├─ README.md（规则）
│   ├─ finance/INDEX.md · content/INDEX.md · ai/INDEX.md（只索引候选，无内容）
│
▼
PROJECT（各自 AGENTS / 知识 / 工具）
│
├── 投资研究（KK Trading Alpha）
│    ├─ AGENTS.md（项目契约）· README · PROGRESS.md(24K) · docs/ · output/ · tests/ · app/ · lib/ · scripts/
│    └─ memory/ ← 实际最完整的"记忆/第二大脑"（内含其他项目文件，见 §5）
│
├── 视频剪辑（Creator OS）← 架构最完整的项目
│    ├─ AGENTS.md（Router）· README · docs/SYSTEM.md
│    ├─ .codex/agents/：6 个（director/research/audience/creative/production/editor，各带 reasoning 覆盖）
│    ├─ .agents/skills/：5 个（research/brief/pack/comments/footage）
│    ├─ context/（单源知识）· artifacts/ · cache/(空) · raw/(空) · templates/ · scripts/（5 个）
│    └─ projects/2026-08/README.md
│
├── AI落地（1 份 103KB 报告，无 AGENTS）
├── 数据分析训练（DCF 教学 + 求职资料，无 AGENTS）
├── 产品经理训练（README + 模板/，无 AGENTS）
├── 英语培训 / 表达能力提升 / 销售训练（空仓库，无 AGENTS）
│
└── 管理codex（本仓库，系统控制台）
     ├─ CURRENT_ARCHITECTURE.md · CURRENT_CODEX_ARCHITECTURE.md（本文）
     ├─ ROUTER.md · HANDOFF.md · DECISIONS.md · TODO.md
     └─ git：main 分支 2 commits
│
▼
SECOND BRAIN / KNOWLEDGE
├─ 投资研究/memory/（AGENTS·TODO·people·projects·notes·agent）← 事实上的中心记忆
├─ Obsidian Vault（欢迎.md + 创建链接.md，几乎空，未启用）
└─ ~/.codex/memories_1.sqlite（空）
```

## 2. 关键事实（非猜测）

| 项 | 实际状态 |
|---|---|
| 全局 AGENTS | 1.3KB，新版（记忆路由见 ROUTER、工作方式、用户偏好、项目入口） |
| 项目 AGENTS | 仅 投资研究、视频剪辑 两个有；其余 6 个 ChatGPT 项目无 |
| 全局 Agents | 无（~/.codex/agents 不存在） |
| 项目 Agents | 仅 视频剪辑 6 个（toml 已核实，各带 developer_instructions + reasoning 覆盖） |
| Skills | 全局 10 个（4 用户 + 6 系统）；项目 5 个（仅视频剪辑）；无 Shared skill |
| MCP | config 仅 node_repl（启用）+ computer-use（禁用）；全盘无 .mcp.json；13 个插件提供 app/connector 工具 |
| Memory | 投资研究/memory 最完整；~/.codex/memories 空；Obsidian 空 |
| Research Cache | 无正式机制；视频剪辑 cache/ 为空；投资研究仅代码级 TTL 缓存（报价60s/K线30min） |
| 状态文件 | 投资研究 PROGRESS.md + memory/TODO.md；管理codex DECISIONS/HANDOFF/TODO；无各项目 STATE.md |
| Scripts | 投资研究 1 个（moomoo-opend-bridge.mjs）；视频剪辑 5 个（hash/merge/validate/scaffold） |

## 3. 跨项目互通现状

- **AGENTS**：GLOBAL（~/.codex/AGENTS.md）所有会话继承；PROJECT LOCAL（投资研究/视频剪辑）。无跨项目重复规则（全局已不含投资专用风格）。
- **Skills**：全局 skills 所有项目可见；项目 skills 仅视频剪辑可用。**分类错误**：moomooapi / install-moomoo-opend / LEGAL_MooMoo_* 是投资专用却全局可见。
- **Knowledge**：**不互通**。无 Shared 内容；唯一"跨项目共享"的是 投资研究/memory/，且里面误存了 CreatorOS、AI产品商业化两个其他项目的文件（见 §5 污染）。
- **Memory**：因历史"中心记忆区"设计，投资研究/memory 事实上跨项目使用（存了其他项目文件）→ 投资研究会话会读到无关上下文。

## 4. 已做对的（KEEP）

1. 视频剪辑 Creator OS 全架构（Router + 项目 agents + skills + 单源 context + 脚本优先 + 数据分级）
2. 投资研究 memory 体系（简洁、带日期、可检查）
3. Agent reasoning 分级（视频剪辑：director/creative/research=high，audience/production/editor=medium）
4. 全局 AGENTS 已瘦身（1.3KB，无巨型规则文件）
5. 项目隔离（空项目不建 AGENTS；无跨项目自动加载）
6. Shared 索引先行（不提前搬内容）
7. 脚本优先（6 个确定性工具脚本）
8. 投资研究代码级 TTL 缓存 + fetch 超时（避免重复网络/MCP 调用）

## 5. 发现的问题（仅记录）

- **P1 主 Prompt 未落盘**：35 节系统 Prompt 是会话文本，每会话重复注入（~10K token），无版本管理。
- **P2 跨项目知识混居**：投资研究/memory/projects/ 含 CreatorOS、ai-产品商业化研究；people/用户.md 含全局偏好 → 分类错误 + 潜在 Context 污染。
- **P3 全局默认 reasoning=high**：所有会话（含琐事）默认高推理，flash 模型上开销放大。
- **P4 moomooapi SKILL.md 152KB**：投资专用却全局可见；一旦加载即耗大量 Context。
- **P5 无 Research Cache**：跨会话研究无缓存索引（金十/竞品/行情均可能重复查）。
- 次要：AI落地 103KB 报告无摘要索引；PROGRESS.md 24KB 每次投资会话按协议必读；skills 清单随插件数量膨胀。

## 6. 结论

实际结构：**GLOBAL → PROJECT**（+ 空的 SHARED 骨架），唯一共享机制是"挂靠在一个项目下的 memory"。
目标三层（GLOBAL → SHARED → PROJECT）**尚未真正实现**，但改造方向明确、无需要推倒重来的部分。
