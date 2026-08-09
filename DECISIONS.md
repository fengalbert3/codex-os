# DECISIONS.md — 系统级决策日志

> 更新：2026-08-09 ｜ 维护：管理codex
> 只记录真正重要的决策（影响全局/多项目）。格式：Decision / Reason / Alternative / Impact / Date。

## D001 三层架构确认 + 先审计后升级（2026-08-09）
- Decision: 全系统按 GLOBAL（方法）→ SHARED（复用知识）→ PROJECT（业务）三层管理；管理codex 作为系统控制台。
- Reason: 现状只有 Global + Project，缺 Shared 层；升级必须基于审计，不重构。
- Alternative: 直接按系统 prompt 重建全套 → 拒绝（用户明确禁止重构与重建 Second Brain）。
- Impact: 建立 Shared 骨架；全局 AGENTS 瘦身；记忆区与投资研究解耦。

## D002 记忆区定位（2026-08-09）
- Decision: 投资研究/memory/ 明确为「投资研究项目记忆」，不再被全局强绑定为中心记忆区；全局记忆路由见 ROUTER.md。
- Reason: 全局规则不应依赖单一项目路径（架构错位）；内容质量好，不重建。
- Alternative: 物理迁移记忆目录 → 风险高、收益低，暂缓；列为迁移候选。
- Impact: 全局 AGENTS 解除对投资研究路径的硬引用；各领域记忆按 Router 读取。

## D003 Shared 采用「索引先行」策略（2026-08-09）
- Decision: Shared 层先建目录骨架 + INDEX.md（只写候选来源路径），不复制内容。
- Reason: 避免提前搬移造成破坏；只有出现第二个项目复用时才正式迁移（去重原则）。
- Alternative: 立即把 DCF/小红书方法等搬进 Shared → 可能在未验证前破坏现有项目调用。
- Impact: Shared 层零风险起步；MOVE/MERGE 候选记录在 TODO.md。

## D004 CODEX_OS 规范落盘 + 渐进加载（2026-08-09）
- Decision: 35 节系统 Prompt 压缩落盘为 `管理codex/CODEX_OS.md`（Canonical Spec）；Global AGENTS 保持小型，仅条件引用、不加载。
- Reason: 结束"每会话重复粘贴大 Prompt"；同时避免退化为"每会话自动读取大文件"（PERSIST FULL SPEC / LOAD MINIMUM RULES / RETRIEVE DETAILS ON DEMAND）。
- Alternative: 全文复制进 Global AGENTS → 拒绝（巨型 AGENTS 违背最小 Context 原则）。
- Impact: 每会话省 ~10K token 粘贴成本；系统管理任务按 TOC 定位章节；普通业务任务零影响；一次只改一个变量（O2-O5 暂缓）。

## D005 记忆边界清理（O2，2026-08-09）
- Decision: 把投资研究/memory 中混入的 Creator OS / AI 产品 / 全局用户偏好归位；本记忆区明确为投资研究专属。
- Reason: 消除跨项目 Context 污染；全局偏好只保留少量稳定信息；一个知识一个 Source of Truth。
- Alternative: 复制多份到各项目 → 拒绝（不复制原则）；重建 Second Brain → 拒绝（范围外）。
- Impact: 投资任务不再读到无关项目记忆；Creator OS / AI 产品各自项目拥有自己的项目记忆；全局偏好集中在 GLOBAL_MEMORY.md。

## D006 MooMoo Skill 归位（O4，2026-08-09）
- Decision: moomooapi / install-moomoo-opend / LEGAL_MooMoo_* 从全局迁移到 投资研究 项目级 .agents/skills 与 docs/legal。
- Reason: 仅投资研究真实使用（grep 全 Documents 确认无其他项目引用）；减少全局 Skill 噪音与无关触发。
- Alternative: 留在全局 + 标注 → 拒绝（分类错误）；迁到 Shared/finance → 拒绝（当前无第二个金融项目使用，不预建）。
- Impact: 投资研究会话仍可发现（项目级 discovery）；其他项目不再暴露 moomoo 触发词；硬编码路径已同步更新。
