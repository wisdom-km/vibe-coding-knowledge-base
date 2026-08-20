# 代码实际落在哪

按路线图一截一截做，Windows 实机，macOS 靠 CI。每截没验收，不做下一截。

给 AI 的规矩很死：先读地图，只做当前允许的。后来落成固定走法——面板只读快照、只丢 Command，App 里 visit 分发，拥有那个名词的模块改自己的状态，下一帧再把快照填回去。

看见和点击在 `src/UI`。路径、线程、HTTP 在 Platform，中文路径在这里用 UTF-8 和宽字符转换，别的模块不要自己搞 `wchar_t`。像素在 `backends/bgfx`。剧本在 Script，变换在 Scene，机位在 Camera，绑定就是 Link 里一张表。画布吃快照，不重新解析 Markdown。缩略图由 App 向 Renderer 要回读，Storyboard 不碰 bgfx。导出走离屏，不含地面格网。官方下载写死地址，失败用缓存。AI 目录在，App 零引用。

Windows Debug 大概一百来个用例。中文文件名必须测。

Agent 很容易把整个功能写进当时打开的文件。没有名词表，面板里就会长出解析器。官方清单走 `raw.githubusercontent.com`，有的网络会挂，产品上用最后一次有效缓存，而不是让库面板卡死。

0-1 的完成定义是主路径能走完并导出，不是文件夹齐了。不要问第四句：「顺便把后面 Phase 也写了吧。」
