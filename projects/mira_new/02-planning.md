# 阶段记录：Planning & Context

**项目名称**：DirectorDesk（mira_new）  
**阶段**：Planning  
**日期**：2026-08-18  
**工具与模型**：Cursor；开发地图 `00`–`06` 作为唯一上下文  
**项目当前约束**：C++ 桌面应用；要长期迭代也要现在能跑；AI 会跨对话丢失记忆

---

## 1. 这个阶段的目标是什么？

选定一条架构路线：为变化预留接缝，不为幻想预留房间。并把边界写进 `01`，用 CMake 当硬门禁。

## 2. 架构路线：怎么选，不选什么

对照源码，实际走的是 **单仓、分层模块、接口隔离第三方**，不是微服务，也不是一个 `main.cpp` 通吃。

### 选了什么（接缝）

| 大公司做法 | 缩到本仓库 | 源码 |
|------------|------------|------|
| 体验 / 应用 / 领域 / 基础设施 | UI → App(Command) → 名词模块 → Platform/backends | `src/UI` 只链 `dd_core` + imgui |
| 面向接口 | `IRenderer` `IModelLoader` `IHttpClient` `IImageGenService` | `include/DirectorDesk/**/I*.h` |
| 数据所有权 | 剧本属 Script；节点属 Scene；绑定属 Link；App 只组装 | `StoryboardSourceSnapshot` 不含 Script 对象 |
| 谁有权改哪块 | CMake 禁止反向依赖 | `src/UI/CMakeLists.txt` 写明不得链 GLFW/bgfx |
| 异步 | 后台只交回值 | `Core::ResultQueue`；加载器出 `ModelData`，GPU 仍在主线程 |

四层在本仓库的落点：

- **体验**：`IPanel::Draw(const AppViewState&, CommandQueue&)`
- **用例**：`Application.cpp` 里 `std::visit` 分发 Command
- **领域**：Script / Scene / Camera / Link / Storyboard / Asset / Export
- **基础设施**：`backends/bgfx`、`backends/curl`、GLFW 窗口

### 明确不选什么（空房间）

- 不为三年后每个按钮建空表、空服务
- 不上功能开关平台、插件框架、多租户——单用户桌面 Demo 用 git 回退就够
- 不把 13 个 CMake 库再拆成 13 个进程
- 不在 P0 实现 Undo；Command 保持值对象即可（接缝在，房间空着）
- AI 只留 Null/Mock；`Application.cpp` **至今未接线**——这是正确的冻结，不是半成品愧疚

### 动态选择规则（后来写进 `07`）

出现任意两条才抽新模块：第二种实现、第二个调用方、没有窗口测不了、AI 反复写错地方、变更频率已分叉。

Demo 阶段：**部分模块化**——控制面全留，模块数锁定，禁止为小功能建第 14 个库。

## 3. 实际发生了什么？

- 好：Phase 1 就把 `IRenderer` 和离屏回读做掉。导出与视口是**第二调用方**，这条缝若不先打，后面分镜缩略图会把 bgfx 拖进 Storyboard。
- 好：OBJ 与 GLB 逼出 `IModelLoader` 注册表，而不是 `Library.cpp` 里堆 `if (ext)`。
- 人工干预：拒绝 ImGuizmo、拒绝自定义 GitHub 源、拒绝 UI 持有 `Scene::Document`。
- 走偏：短命分支 `cursor/phase-4-camera-presets` 与「默认在 main 工作」的纪律冲突，tag 列表里没有干净的 `phase-4`。

## 4. 关键决策与取舍

| 决策点 | 当时为什么这样选 | 事后看是否正确 |
|--------|------------------|----------------|
| C++17 不是 20 | 工具链兼容 | 正确 |
| vcpkg manifest 锁 baseline | 可复现构建 | 正确，但首次配置很慢 |
| GLFW_NO_API，bgfx 建交换链 | 避免双图形 API | 正确，也是闪屏 bug 的背景 |
| UI 只读快照 | 防 AI 把解析器写进面板 | 正确；代价是 `AppViewState` 很胖 |
| App 当唯一编排者 | 跨模块快照必须有一个组装者 | 正确；代价是 `Application.cpp` ~1600 行 |
| 先本地闭环再在线库 | `00` 开发顺序 | 正确 |
| Link 独立成库 | 绑定是稳定名词 | 偏薄（一个 map 表），但删除关联功能时干净；现阶段不合并 |

## 5. 踩坑与惊喜

**踩坑**：把「高度模块化」理解成「文件夹越多越好」。P0 结束后正确收敛是**锁模块数**，不是继续拆。

**惊喜**：CMake `target_link_libraries` 比 Prompt 更硬。模型再健忘，也链不上 bgfx。

## 6. 可复用的经验

规划阶段交付物应是：

1. 用户路径宪法（`00`）  
2. 模块 DAG + 禁止项（`01`）  
3. 有验收的 Phase 门禁（`02`）  
4. 一份「聊天覆盖不了地图」的 Agent Prompt（`06`）  

不要交付：假想功能清单、空接口实现、微服务图。

## 7. 给未来自己的一句话

功能可以没有，接缝必须先有；接缝有了之后，停止为想象建房间。
