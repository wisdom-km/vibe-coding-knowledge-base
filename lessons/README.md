# Lessons 通用教训库

跨项目提炼出的通用洞见。

这里不放具体项目的函数签名或 Command 清单，只放「模式 / 反模式」。项目细节在 `projects/<name>/`。

**读法**：新开一个 vibe coding 项目时，按下面「建议阅读顺序」扫一遍；做 UI 专业化时加读 IA 两篇。

## 建议阅读顺序

1. [dev-map-beats-chat.md](dev-map-beats-chat.md) — 聊天不作数  
2. [seams-not-rooms.md](seams-not-rooms.md) — 预埋接缝，不预埋空房间  
3. [complete-then-professionalize.md](complete-then-professionalize.md) — 先完成再完美  
4. [advice-to-map-loop.md](advice-to-map-loop.md) — 咨询进地图  
5. [ia-philosophy.md](ia-philosophy.md) — IA 是什么  
6. [lock-ia-skeleton.md](lock-ia-skeleton.md) — 锁槽位再优化  

配套模板与 Prompt 在仓库根 README 的「真实案例」下列出。

## 已沉淀

### 记忆与接缝

- [dev-map-beats-chat.md](dev-map-beats-chat.md)  
  开发地图覆盖聊天记忆。新开对话只 clone 仓库，也要知道该做什么、不该做什么。

- [seams-not-rooms.md](seams-not-rooms.md)  
  架构回答「哪一块可以独立加、独立删、独立坏」。预埋接口与所有权，不预埋空表、空服务、空模块。

### 完成之后怎么变专业

- [complete-then-professionalize.md](complete-then-professionalize.md)  
  「先完成再完美」和「做成专业领域软件」是同一条路的两段。专业化是修订地图，不是抄 Maya 目录推倒重来。

- [advice-to-map-loop.md](advice-to-map-loop.md)  
  专家或 AI 的建议默认是草案。人勾选吸收 / 推迟 / 拒绝后，只改被点名的 markdown，禁止聊完直接重构。

### 信息架构（IA）

- [ia-philosophy.md](ia-philosophy.md)  
  IA 管东西放哪、叫什么、一次处理哪一层，不管颜色图标。DCC 六条：一个主舞台、一种选中、按职责分区、工作区换班、名字稳定、主路径外露。

- [lock-ia-skeleton.md](lock-ia-skeleton.md)  
  先锁槽位和选择模型，再搬家、减入口，最后才换皮。Vibe coding 按槽位下单，禁止「整体更专业一点」。

## 待写主题

- 为什么「先让 AI 解释根因」比直接修更有效
- Context 文件过长的代价
- 小步提交在 Vibe Coding 中的真实价值
- 什么时候应该停下来自己写，而不是继续提示

每条 lesson 用独立 `.md` 文件，标题清晰；本 README 只做目录。新增 lesson 时必须同时改本文件。
