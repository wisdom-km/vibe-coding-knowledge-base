# 教训：聊天不作数，开发地图才作数

**来源**：[DirectorDesk / mira_new](../projects/mira_new/)  
**适用**：多轮 Cursor / Claude / Grok 接力的中长期项目

## 模式

Vibe coding 的记忆在对话里，对话一结束架构就消失。对抗方式：

1. 仓库内一份开发地图（愿景、边界、路线、现状、规范）
2. Agent Prompt **只规定工作方式**，不复制会漂移的技术事实
3. 每次工作结束更新「当前状态」
4. 构建系统禁止错误依赖（比 Prompt 硬）

DirectorDesk 的落地：`docs/dev-map/00`–`08` + `AGENTS.md` 只做指针。

## 反模式

- 把整份架构粘进 Cursor Rule，改一处忘改另一处
- 用上一场聊天当需求，和仓库现状对着干
- 不更新现状文件，下一场 AI 从 Phase 0 重新发明

## 检验问题

新开一场对话，不贴聊天记录，只 clone 仓库：Agent 能否知道现在该做什么、不该做什么？不能，就还没沉淀。
