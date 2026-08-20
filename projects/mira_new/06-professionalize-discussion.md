# 阶段记录：专业化怎么想（只讨论，不改代码）

**项目名称**：DirectorDesk（mira_new）  
**阶段**：Planning / Reflection（P0 之后）  
**日期**：2026-08-21  
**工具与模型**：Cursor Grok 4.6；产品负责人 Wisdom  
**项目当前约束**：主路径已通；明确不改源代码；要把「先完成再完美 + 咨询后整理成 md」收成可复用知识

---

## 1. 这个阶段的目标是什么？

讨论：若要把 Demo 做成更专业的领域软件，重构原则是什么；以及如何把专家/AI 建议稳定地变成 vibe coding 能遵守的文档。不实施重构。

## 2. 我给 AI 的核心提示词 / 上下文

「先完成再完美。边做边优化，咨询专业人士和 AI，把新建议整理成适合 vibe coding 的 md。只讨论知识库，不改源码。」

对照已有：产品 `07`/`08`、知识库 `seams-not-rooms`、`dev-map-beats-chat`。

## 3. 实际发生了什么？（过程）

讨论收敛成两条可重复规则，而不是一份 DirectorDesk 重构任务单：

1. 专业化是**下一场地图修订**，不是推倒重来。导演台的专业是路径变深，不是变成通用 DCC。  
2. 咨询默认产出**建议卡**，人勾选后再改指定 md；禁止「聊完直接重构」。

## 4. 关键决策与取舍

| 决策点 | 当时为什么这样选 | 事后看是否正确 |
|--------|------------------|----------------|
| 不在这次改 mira_new 源码 | 知识未入库就改代码 = 聊天覆盖仓库 | 待下一轮执行时再验证 |
| 专业能力按「是否已有接缝」排序 | Command 已在，Undo 是启用不是发明 | 与 0-1 决策一致 |
| 知识库与产品地图分开写 | 避免第三份架构正文 | 沿用 08 的指针原则 |
| 提供 advice-intake 模板 | 让「边做边咨询」可重复 | 下一轮咨询即可试用 |

对 DirectorDesk **以后**可能的专业化顺序（仍是讨论，不是批准施工）：

1. 痛了再把 `Application.cpp` 按文件切开（仍属 App）  
2. 用户误操作变多时启用 Undo（走现有 Command）  
3. 选择/焦点从散落状态收成明确快照  
4. `00` 改了再谈时间轴、真 AI、插件  

未批准：抄 DCC 插件框架、微服务、为专业化新建一堆空模块。

## 5. 踩坑与惊喜

**踩坑**：把「专业」理解成功能清单，AI 会立刻铺 Undo+时间轴+脚本+云，全部撞红线。  
**惊喜**：「咨询 → md → 再编码」本身就是 vibe coding 的康威定律：文档边界 = AI 权限边界。

## 6. 可复用的经验 / 提示词 / 模式

- [complete-then-professionalize.md](../../lessons/complete-then-professionalize.md)  
- [advice-to-map-loop.md](../../lessons/advice-to-map-loop.md)  
- [advice-intake 模板](../../docs/templates/advice-intake.md)  
- [advice-intake Prompt](../../prompts/architecture/advice-intake.md)  

## 7. 给未来自己的一句话

完美不是重写；完美是把活下来的接缝用疼了再加深，并且先写进地图。
