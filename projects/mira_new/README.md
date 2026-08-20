# 案例：DirectorDesk（mira_new）

**一句话**：用 vibe coding 从空仓库做到可安装的 3D 导演台——Markdown 剧本 → 资源库 → 预设机位 → 分镜画布 → PNG 导出。

| 项 | 内容 |
|----|------|
| 产品名 | DirectorDesk |
| 代码仓库 | [wisdom-km/mira_new](https://github.com/wisdom-km/mira_new) |
| 架构目录 | [wisdom-km.github.io/mira_new](https://wisdom-km.github.io/mira_new/) |
| 技术栈 | C++17 · CMake + vcpkg · GLFW · Dear ImGui · bgfx |
| 周期 | 2026-08-18 → 2026-08-19（P0 闭环 + 知识沉淀） |
| 工具 | Cursor · 多轮 Agent · GitHub Actions |
| 当前状态 | Phase 10 完成；Demo 迭代政策 `07`/`08` 生效；AI 模块冻结 |

源码里的权威地图仍在产品仓库：`docs/dev-map/00`–`08`。本案例只沉淀**过程、决策、坑**，不复制契约签名，避免第二个事实源。

## 读这个案例之前先记住

架构的核心不是「一开始猜到以后所有功能」，而是先画接缝：

**哪一块可以独立加、独立删、独立坏，而不把整栋楼拆掉。**

Vibe coding 把「很多人一起改」换成「很多段没有共同记忆的对话」。接缝同样必要。聊天不作数。

## 时间线（0 → 1）

| 顺序 | Phase / 事件 | 源码证据 | Tag |
|------|----------------|----------|-----|
| 0 | 先写开发地图，再写代码 | `docs/dev-map/` 先于业务 | — |
| 1 | 空壳：窗口、日志、UTF-8 路径、CI | `src/Core` `src/Platform` | `phase-0-skeleton` |
| 2 | 尽早打掉渲染风险：视口 + 离屏 PNG | `IRenderer` + `backends/bgfx` | `phase-1-render-camera` |
| 3 | 后台加载 GLB/OBJ，主线程上 GPU | `IModelLoader` + `ResultQueue` | `phase-2-model-import` |
| 4 | Markdown 剧本 Scene/Shot | `src/Script` | `phase-3-script` |
| 5 | 预设机位、多相机、地面格网 | `src/Camera` | 经短命分支合入，无独立 `phase-4` tag |
| 6 | 本地资源库 | `src/Asset/Library.cpp` | `phase-5-local-assets` |
| 7 | `.ddproj` + Shot↔相机 | `ProjectFile` `Link::Table` | `phase-6-project-link` |
| 8 | 分镜画布 + 导出（本地闭环走通） | `Storyboard` `Export` | `phase-7-core-loop` |
| 9 | 官方在线资产（固定源） | `OfficialCatalog.cpp` | `phase-8-online-assets` |
| 10 | 供应商无关 AI 接口，不接线 | `src/AI`，App 未调用 | `phase-9-ai-interfaces` |
| 11 | UX、安装包、文档 | `packaging/windows` | `phase-10-p0`… |
| 12 | 滚轮闪屏、Inno 语言、架构图 | 见 `04-debug.md` | `phase-10-p1` |
| 13 | 接缝知识库 + 模块数锁定 | mira_new 的 `07`/`08` | 文档提交 |
| 14 | 先完成再完美、建议进地图 | 见 `06-professionalize-discussion.md` | 知识库，未改产品源码 |
| 15 | IA 哲学：锁槽位与选择模型 | 见 `07-ia-skeleton.md` | 草案，未改产品源码 |

## 本文件夹

- [01-ideation.md](01-ideation.md) — 为什么做、用户路径宪法
- [02-planning.md](02-planning.md) — 架构路线怎么选、预埋接缝不预埋房间
- [03-implementation.md](03-implementation.md) — 按 Phase 落地，源码落点
- [04-debug.md](04-debug.md) — 真实坑与修复
- [05-reflection.md](05-reflection.md) — 哪些能做哪些不能、下一步
- [06-professionalize-discussion.md](06-professionalize-discussion.md) — 先完成再完美、专业化重构原则、咨询如何进 md
- [07-ia-skeleton.md](07-ia-skeleton.md) — 导演台 IA 骨架草案（主舞台、选中、七槽、三工作区）
- [08-ia-philosophy-log.md](08-ia-philosophy-log.md) — IA 讨论阶段记录

跨项目提炼：

- [lessons/seams-not-rooms.md](../../lessons/seams-not-rooms.md)
- [lessons/dev-map-beats-chat.md](../../lessons/dev-map-beats-chat.md)
- [lessons/complete-then-professionalize.md](../../lessons/complete-then-professionalize.md)
- [lessons/advice-to-map-loop.md](../../lessons/advice-to-map-loop.md)
- [lessons/ia-philosophy.md](../../lessons/ia-philosophy.md)
- [lessons/lock-ia-skeleton.md](../../lessons/lock-ia-skeleton.md)
- [prompts/architecture/dev-map-first.md](../../prompts/architecture/dev-map-first.md)
- [prompts/architecture/advice-intake.md](../../prompts/architecture/advice-intake.md)
- [prompts/architecture/ia-slot-orders.md](../../prompts/architecture/ia-slot-orders.md)
- [docs/templates/advice-intake.md](../../docs/templates/advice-intake.md)
- [docs/templates/ia-skeleton.md](../../docs/templates/ia-skeleton.md)
