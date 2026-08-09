# ADAPT — 如何把它改成你自己的系统

本仓库文件来自作者真实环境（路径、项目名、决策记录均真实）。直接复制可以，但**强烈建议改成你自己的**：

## 1. 路径（全局替换）
- `/Users/fqt/Documents/投资研究` → 你的投资/研究项目目录
- `/Users/fqt/Documents/ChatGPT/管理codex` → 你放置本仓库的位置
- `/Users/fqt/Documents/Shared/` → 你的共享知识目录
- `~/.codex/` → 你的 Codex 全局目录（Linux/Windows 路径不同）

## 2. 项目（替换为自己的业务）
- `投资研究` / `视频剪辑` / `AI落地` / `数据分析训练` … → 换成你的真实项目
- `ROUTER.md` 的 PROJECT 表按你的项目重写

## 3. Global 配置（最小改动）
- 参考 `CODEX_OS.md` §02/§03，把你的 `~/.codex/AGENTS.md` 保持 <3KB：
  - 记忆协议（Router 引用式）
  - 用户偏好（语言、数据真实性）
  - 工作方式 Runtime 规则（Search before read 等 7 条）
  - 系统规范 Reference 指针（禁止自动加载）

## 4. Shared 层（索引先行）
- 建 `/你的路径/Shared/<领域>/INDEX.md`，**先只写候选来源，不复制内容**
- 出现第二个项目复用时才正式迁移（MOVE 不 COPY）

## 5. 项目记忆（每个项目一份）
- 参考结构：`AGENTS.md` + `memory/`（TODO / projects / notes / people / agent）
- 规则：简洁、带日期、可检查；禁止转储聊天记录/密钥

## 6. 决策与 Handoff
- `DECISIONS.md`：只记真正重要的（Decision/Reason/Alternative/Impact/Date）
- `HANDOFF.md`：Agent 切换 / 长会话 / 暂停时使用，不复制聊天历史

## 注意
- 公开前先 grep 你的仓库：`grep -rniE "token|secret|api_key|password|bearer" .`
- 本仓库的 `DECISIONS.md` / 架构快照是作者的历史记录，可保留作"真实案例"，也可删除后从你自己的第一次 Audit 开始。
