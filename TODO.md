# TODO.md — 管理codex 系统升级待办

> 更新：2026-08-09

## 本轮已确认执行（2026-08-09）
- [x] 首次系统审计 → CURRENT_ARCHITECTURE.md（commit 210ec68）
- [x] 管理codex 控制台文件：ROUTER.md / HANDOFF.md / DECISIONS.md / TODO.md
- [x] Shared 骨架 + 索引：/Users/fqt/Documents/Shared/{finance,content,ai}/INDEX.md
- [x] ~/.codex/AGENTS.md 瘦身（移除投资专用分析风格、记忆位置解耦、加 Router 引用）
- [x] config.toml trusted 补：表达能力提升、销售训练（需重启 Codex 生效）

## 待验证 / 下一步
- [ ] MOVE 候选：moomooapi / install-moomoo-opend / LEGAL_MooMoo_* 从全局 skills 归位（先验证投资研究可正常调用，再动）
- [ ] MERGE 候选：DCF 模板（数据分析训练）→ Shared/finance；产品经理模板 → Shared（出现第二个复用项目再迁）
- [ ] 记忆迁移候选：投资研究/memory/people/用户.md 的全局个人偏好 → 独立全局记忆区
- [ ] 通用方法 skills 渐进：web-research / source-verification / handoff / decision-log / research-cache（按需创建，不一次铺满）
- [ ] 空项目激活后再建 AGENTS：英语培训 / 表达能力提升 / 销售训练
- [ ] 定期 Context GC：扫描重复 Skills / 过时规则 / 无效缓存（建议每月一次）

## O1 执行（2026-08-09）
- [x] CODEX_OS.md 落盘（Version 1.0，123 行 / 8KB，含 TOC 章节路由 + 12 章 + 3 Appendix）
- [x] ~/.codex/AGENTS.md 保持小型：加入 CODEX_OS.md 条件引用 + 缺失 Runtime 规则（默认单 Agent / 优先复用 / 不读无关项目知识 / 输出简洁）
- [x] ROUTER.md 加入 CODEX_OS.md 入口（可发现性）
- [x] 静态验证：无任何自动加载机制引用 CODEX_OS.md 全文（仅条件引用）
- [ ] TEST C 真实验证：下一个新 Session 不粘贴 35 节 Prompt 且能定位规范
- [ ] O2-O5 暂缓（记忆归位 / reasoning 默认 / moomoo 归位 / Research Cache）——一次只改一个变量

## O2 执行（2026-08-09）
- [x] CreatorOS 项目记忆 → 视频剪辑/projects/CreatorOS-小红书美甲内容系统.md
- [x] AI 产品商业化研究 → AI落地/projects/ai-产品商业化研究.md（待办内联）
- [x] 全局用户偏好 → 管理codex/GLOBAL_MEMORY.md（投资相关留在 用户.md）
- [x] 投资研究/memory/TODO.md 清除 AI 产品 / 管理codex 节（信息已归位）
- [x] conventions.md 过时"第二大脑系统"节更新为 Router 路由
- [x] memory/AGENTS.md 加边界声明（本记忆区仅服务投资研究）
- [ ] TEST D 复核：迁移后全量 grep 无悬空引用

## O4 执行（2026-08-09）
- [x] moomooapi / install-moomoo-opend / LEGAL_MooMoo_* 从全局 ~/.codex/skills 迁移到 投资研究（.agents/skills/ + docs/legal/）
- [x] 同步更新硬编码路径：.env.local（MOOMOO_OPEND_SKILL_DIR）、bridge.mjs、provider.ts fallback、memory/notes/moomoo工作流.md、AGENTS.md
- [x] moomooapi SKILL.md（152KB）未压缩——列后续任务（Progressive Disclosure）
- [ ] TEST B 实机 dry-run：投资研究会话内运行 check_env.py 确认可调用
- [ ] 新 prefix 批准：.agents/skills/moomooapi/scripts/quote/ 首次运行需重新授权
