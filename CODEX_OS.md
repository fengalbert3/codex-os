# CODEX_OS.md — Codex 工作系统规范（Canonical Specification）

> **Version**: 1.0 ｜ **Updated**: 2026-08-09 ｜ **Major changes**: 基线落盘（压缩自 35 节会话 Prompt，去重复/去语气/去过时方案）
> **定位**: REFERENCE / Source of Truth，**不是 Always-Loaded Context**。
> **读取规则**: 仅系统管理类任务按需定位章节；普通业务任务不读本文件（详见 §03）。

## TOC（章节路由，按需定位）
| # | 章节 | 何时查 |
|---|---|---|
| 01 | Principles 总原则 | 任何系统决策前 |
| 02 | Context Architecture 三层架构 | 判断内容归属 |
| 03 | Context Routing 上下文路由 | 任务→去哪找知识/记忆 |
| 04 | Task Routing & Agents 任务与 Agent 路由 | 是否启动 Agent |
| 05 | Skills 管理 | 建/改/删/评估 Skill |
| 06 | Knowledge & Second Brain | 知识归属/第二大脑管理 |
| 07 | Memory | 记忆协议 |
| 08 | Research Cache | 研究前查重 |
| 09 | Preflight & Handoff | 会话开始/交接 |
| 10 | Context Compression & GC | 长会话/清理 |
| 11 | Token Optimization | 优化决策/升级评估 |
| 12 | Learning Loop 沉淀循环 | 新经验是否沉淀 |
| A | Cost/Benefit 模板 | 任何新增组件前 |
| B | 迁移原则 | 跨层级迁移内容 |
| C | 禁止行为 | 红线检查 |

---

## 01 Principles（总原则）
- **共享能力，不共享无关上下文。**
- Global 管方法；Shared 管复用知识；Project 管具体业务；Memory 辅助 Recall；Archive 管历史；Router 决定什么时候读什么。
- 目标：`Maximum Useful Work / Minimum Token + Context + Repetition + Maintenance`。
- 归属三问：How to work? → GLOBAL；Multiple projects may need? → SHARED；One project only? → PROJECT LOCAL。
- **If it works, preserve it.** 不为"最佳实践"增加复杂度。

## 02 Context Architecture（三层架构）
- **GLOBAL**（方法，所有项目继承）：`~/.codex/AGENTS.md`（仅 Runtime 规则）；系统规范 = 本文件；控制台 = 管理codex 仓库（ROUTER/DECISIONS/TODO/HANDOFF）。
- **SHARED**（复用知识，按需检索，不自动加载）：`/Users/fqt/Documents/Shared/<领域>/INDEX.md`（索引先行）。
- **PROJECT LOCAL**（业务，默认隔离）：各项目目录，自有 AGENTS / 知识 / 产出。
- **MEMORY**：个人偏好、习惯、长期背景（辅助 Recall，非规则）。
- **ARCHIVE**：历史/旧产出，默认不进 Context。

## 03 Context Routing（上下文路由）
- 任务 → 判断领域 → Knowledge Router（管理codex/ROUTER.md）→ 定位最小必要内容 → 执行。
- **禁止**默认全量读取：整个 Repo / 整个 Second Brain / 整个 Knowledge Base / 本文件全文。
- 优先顺序：Search → Locate → Read relevant section → Execute。
- 本文件读取条件：仅系统管理类任务（管理 Codex / 工作流架构 / Skills / Agents / Context / Token / Second Brain / Global 配置 / Audit）。普通 coding/research/creator/investment/video/analysis 任务不读。

## 04 Task Routing & Agents（任务与 Agent 路由）
- **默认单 Agent。** 简单任务（格式修改/小 bug/简单脚本/简单 research）1 个 Agent 完成。
- 复杂任务：Manager + 1 Specialist（如 Manager+Researcher）。
- 只有真正独立的工作才并行（Manager + 多 Specialist）。
- Multi-Agent 能省时间、不一定省 Token：启动前判断"单 Agent 能否合理完成？"。
- Agent 最小 Context：只给 Goal / Relevant Context / Relevant Files / Constraints / Expected Output。
- 返回格式：Finding / Evidence / Decision / Files Changed / Risk / Next Step。

## 05 Skills（管理）
- 归属：跨项目通用 → Global 或 Shared；单项目 → Project Local。
- **Progressive Disclosure**：Skill 结构 = Name → Description → Workflow → References → Raw Material；先识别是否需要，再读具体内容。
- 定期扫描：重复 Skill / 未用 Skill / 重叠 Skill / 过大 Skill（如单个 SKILL.md >50KB 评估拆分）。
- 不一次铺满：只有出现实际需求才创建。
- **Skill Evaluation**（建/改前）：Problem → Current solution → New skill → Expected benefit → Token/Context impact → Maintenance cost → 只留明确收益的。

## 06 Knowledge & Second Brain
- 已有 Second Brain：**不重建**、不复制第二套。
- Store broadly，Retrieve narrowly：可以多存，但一次任务只读必要内容。
- 分级：HOT（当前常用，数量少）/ WARM（搜索可取，默认不加载）/ COLD（历史归档，默认绝不进 Context）。
- Shared 层**索引先行**：先建 INDEX.md 记录候选来源；出现第二个复用项目才正式迁移内容。

## 07 Memory
- Memory = 辅助 Recall（偏好/习惯/历史/常重复信息），**不是规则/知识/STATE/DECISIONS**。
- AGENTS = Rules；Knowledge = Facts；STATE = 当前情况；DECISIONS = 为什么这么选；Memory = Recall。
- 会话流程：开始前按 Router 读对应记忆入口 → 会话中沉淀值得保留的 → 结束前收尾（更新+告知+未决进 TODO）。
- 硬性禁止：转储聊天记录、保存密码/密钥/凭证/隐私。

## 08 Research Cache
- 互联网/GitHub 研究前：先查是否已研究（query/source/date/conclusion），判断新鲜度再决定是否重查。
- 新鲜度分级：STATIC（工作方法）/ SLOW（商业模式）/ MEDIUM（软件文档）/ FAST（财报）/ REALTIME（股价）。
- 缓存落盘位置由 Router 决定（候选：管理codex 或 Shared 维护研究索引）。

## 09 Preflight & Handoff
- **Preflight**：重要会话开始前，按 ROUTER.md 读本任务记忆入口（AGENTS/TODO/projects/notes），不读全部。
- **Handoff**：Agent 切换 / Thread 切换 / Context 过长 / 会话结束 / 项目暂停时使用（模板见 管理codex/HANDOFF.md）：Goal / Completed / Current State / Important Files / Decisions / Known Issues / Next Step / Do Not Repeat。
- 交接后接任者读 Handoff + 必要文件，不重读全部历史。

## 10 Context Compression & GC
- conversation ≠ memory。聊天过长 → 更新 STATE → 记 Decision → 写 Handoff → 压缩/开新会话。
- 定期清理：过时规则、重复知识、废弃 Skill、无效缓存、失效链接、冲突信息。
- 评价系统好坏的标准不是"存了多少"，而是"找到正确信息需要多少 Context"。

## 11 Token Optimization
- 指标：完成任务速度 / 准确率 / 重复工作减少 / Context 量 / Token 消耗 / 人工干预 / 知识复用率 / 维护成本。
- 任何升级（Agent/Skill/MCP/DB/RAG/Vector）先走 Cost/Benefit（见 Appendix A）。
- 技术栈优先级：Plain files → Markdown → Search → Git → Scripts → SQLite → MCP → Semantic Search → RAG → Vector DB/Knowledge Graph。不跳级。
- **Script First**：确定性工作（扫描/查重/索引/解析/转换/统计/diff）优先 Python/Shell/CLI，不让 LLM 重复推理。

## 12 Learning Loop（沉淀循环）
- Work → Learn → Codify → Reuse。
- 同一问题第二次出现时判断归属：Rule / Skill / Script / Shared Knowledge / Template / Memory。
- **不要所有经验都沉淀**：只有重复价值明显的才保存。

---

## Appendix A — Cost/Benefit 判断模板
```
Problem:
Current solution:
New solution:
Expected benefit:
Token impact:
Context impact:
Maintenance cost:
Complexity:
Recommendation:
```

## Appendix B — 迁移原则
`识别 → 比较 → 去重 → 迁移到 Global/Shared → 验证其他项目可正常调用 → 再删除旧副本`

## Appendix C — 禁止行为
- 重构整个系统 / 重建第二套 Second Brain / 所有知识全局同步 / 所有 Skill 全局化。
- 默认给 Agent 全部 Context / 默认启动多 Subagent / 复制相同知识到多个项目。
- 建立巨大 AGENTS.md 或 INDEX.md / 每次读取整个 Repo / 把 Conversation 当数据库 / 把全部 Memory 强制注入 Context。
- 未经评估部署 Vector DB / RAG / 为"最佳实践"破坏现有好用系统。
