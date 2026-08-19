# 阶段记录：Implementation

**项目名称**：DirectorDesk（mira_new）  
**阶段**：Implementation  
**日期**：2026-08-18 → 2026-08-19  
**工具与模型**：Cursor Agent 按 Phase 连续实现；Catch2 做门禁  
**项目当前约束**：Windows 实机；macOS 只靠 CI；每 Phase 未验收不得做下一 Phase

---

## 1. 这个阶段的目标是什么？

按 `02-ROADMAP` 把主路径做成可运行产品，而不是同时铺开所有模块的「完美骨架」。

## 2. 我给 AI 的核心提示词 / 上下文

强制阅读顺序：`00`→`01`→`02`→`03`→`05`→当前 `modules/*.md`。  
每步只允许当前 Phase。结束必须改 `03-CURRENT-STATUS.md`。

加功能的固定走法（后写入 `07`）：

```text
Panel 只读 AppViewState、只 push Command
→ Application visit 分发
→ 拥有该名词的模块改自己的状态
→ 下一帧快照回 UI
```

## 3. 实际发生了什么？

按源码目录，功能落点如下（这是 0-1 真正怎么写出来的）：

| 用户名词 | 实现位置 | 关键接缝 |
|----------|----------|----------|
| 窗口/路径/线程/HTTP | `src/Platform` | UTF-8 在 `Paths.cpp` 用 `u8path` / `WideCharToMultiByte`；其它模块禁止 `wchar_t` |
| 日志/Command/队列 | `src/Core` | `Command` 是 `std::variant` 值对象 |
| 画像素 | `backends/bgfx` 实现 `IRenderer` | ImGui 后端不进 IRenderer |
| 看见图、点按钮 | `src/UI/*Panel.cpp` | CMake 只链 core+imgui |
| 剧本 | `src/Script/Parser.cpp` | 结构唯一来源；画布不得重新解析 |
| 节点变换 | `src/Scene` | DragFloat3，无 ImGuizmo |
| 机位 | `src/Camera` | 物体默认朝 +Z |
| Shot 绑相机 | `src/Link/ShotLink.cpp` | 整库就是一张表 |
| 画布布局 | `src/Storyboard` | 吃 `StoryboardSourceSnapshot` |
| 缩略图像素 | App 调 `RequestReadback`，结果交回 Storyboard | Storyboard 不碰 bgfx |
| 导入模型 | `ObjLoader` / `GlbLoader` 注册 | loader 只出 CPU `ModelData` |
| 导出 PNG | `src/Export` + 离屏 target | 导出不含地面格网 |
| 工程文件 | `src/App/ProjectFile.cpp` | 版本化 JSON `.ddproj` |
| 官方下载 | `OfficialCatalog.cpp` | 编译期写死 URL，失败用缓存 |
| AI | `src/AI/Null*.cpp` `Mock*.cpp` | **App 零引用**，冻结 |

验证习惯：Windows Debug 约 104 cases / 564 assertions；中文文件名测试强制存在。

## 4. 关键决策与取舍

| 决策点 | 当时为什么这样选 | 事后看是否正确 |
|--------|------------------|----------------|
| Phase 1 就做离屏 PNG | 导出是主路径，风险要早死 | 正确。后来缩略图复用同一条缝 |
| 后台加载、主线程上传 GPU | 业务状态单线程 | 正确 |
| 格网只在视口 | 参考图要干净 | 正确，用 `RenderSceneView` 开关而不是 Scene 节点 |
| 在线库固定唯一源 | 防任意第三方 GitHub | 正确；国内网络靠缓存降级 |
| 不拆 Application.cpp | Demo 优化是锁模块数不是再切文件 | 现行政策，待编排痛了再拆文件 |

## 5. 踩坑与惊喜

**踩坑**：

- Agent 容易在「此刻打开的文件」里写完整个功能。没有名词表就会出现面板解析 Markdown。
- Phase 4 走了 `cursor/phase-4-camera-presets` 分支，和「默认 main」纪律打架，历史变乱。
- 官方清单走 `raw.githubusercontent.com`，部分网络会挂——产品上用最后一次有效缓存，而不是让库面板卡死。

**惊喜**：

- 一旦 Command 变体加好，新按钮的 diff 模式非常稳定：头文件一个 struct，visit 一个分支，面板一句 push。
- Catch2 把布局确定性、中文路径从「看起来能跑」里救出来。

## 6. 可复用的经验

实现阶段只问三句：

1. 用户动的是哪个名词？  
2. 像素/文件/网络归谁？  
3. 这一 Phase 的验收测了没有？  

禁止第四句：「顺便把后面 Phase 也写了吧。」

## 7. 给未来自己的一句话

0-1 的完成定义是主路径能走完并导出，不是模块文件夹齐了。
