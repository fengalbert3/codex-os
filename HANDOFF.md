# HANDOFF.md — 标准 Handoff 模板

> 更新：2026-08-09 ｜ 维护：管理codex
> 适用：Agent 切换 / Thread 切换 / Context 过长 / 会话结束 / 项目暂停。
> 规则：交接只写这份模板，不复制聊天历史；接任者读 Handoff + 必要文件，不重读全部历史。

## 模板（复制以下字段使用）

## Handoff — <任务名>
- 日期：
- 交接人： / 接任人：

Goal:
Completed:
Current State:
Important Files:
Decisions:
Known Issues:
Next Step:
Do Not Repeat:

---

## 示例（仅格式参考）

## Handoff — 系统审计
- 日期：2026-08-09
- 交接人：管理codex / 接任人：管理codex（下会话）

Goal: 完成 Codex 系统首次审计并落盘架构基线
Completed: CURRENT_ARCHITECTURE.md 已提交（210ec68）
Current State: 三层架构确认；Shared 骨架已建；全局 AGENTS 已瘦身
Important Files: 管理codex/{CURRENT_ARCHITECTURE,ROUTER,DECISIONS,TODO}.md
Decisions: D001 三层体系，不重构、不重建 Second Brain
Known Issues: config.toml trusted 变更需重启 Codex 生效；moomoo skills 归位待验证
Next Step: 验证 moomoo skills 迁移可行性 → 归位
Do Not Repeat: 不要重做全量目录扫描；直接读 CURRENT_ARCHITECTURE.md
