# DirectorDesk（mira_new）

一个人加 AI，从空仓库做到能安装的 3D 导演台。用户路径很短：写剧本，拿模型，摆机位，看分镜，导出 PNG。

代码在 [wisdom-km/mira_new](https://github.com/wisdom-km/mira_new)。能缩放的图在 [GitHub Pages](https://wisdom-km.github.io/mira_new/)。C++17，CMake + vcpkg，GLFW，ImGui，bgfx。大约两天走完 P0，后面的讨论进了这个知识库，产品源码没跟着改。

契约仍以产品仓库 `docs/dev-map` 为准。这里只记当时怎么想、踩过什么、为什么没把未来三年都预埋进去。

先记一句就够：不是一开始猜中所有功能，是先画清哪一块可以单独加、单独删。Vibe coding 没有共同记忆的团队，只有一段段对话。接缝同样必要。聊天不作数。

## 怎么走过来的

先写开发地图，再写窗口。空壳验证日志和中文路径。尽快把渲染和离屏 PNG 打通，因为后面导出和缩略图都要靠它。模型在后台加载，主线程再上传 GPU。剧本、机位、本地库、工程文件、分镜画布，按这个顺序接到一条能跑完的路上。在线资产和 AI 接口放在闭环之后；AI 至今没接到 App 上，这是故意冻结。

中间有过短命分支，phase-4 的 tag 因此不干净。视口滚轮会闪，是缩略图在主循环里多推了一帧。安装包的中文向导编不出来，因为 winget 的 Inno 不带那份语言文件。GitHub 上的架构图一度扁掉，是 SVG 被 CSS 限宽。这些写在 [04-debug.md](04-debug.md)。

P0 做完之后，我们把「模块数锁定」和「先完成再完美」写进产品地图，又在知识库里补了 IA：现在的乱，主要是四个窗口都像主角。

## 按时间读

1. [为什么做这个](01-ideation.md)
2. [架构怎么选](02-planning.md)
3. [代码实际落在哪](03-implementation.md)
4. [修过的坑](04-debug.md)
5. [做完之后的取舍](05-reflection.md)
6. [专业化和咨询怎么进文档](06-professionalize-discussion.md)
7. [导演台 IA 骨架草案](07-ia-skeleton.md)
8. [IA 那场讨论](08-ia-philosophy-log.md)

抽出去、换项目也能用的，在 [lessons](../../lessons/README.md)。填表和 Prompt 在 [templates](../../docs/templates/) 和 [prompts/architecture](../../prompts/architecture/)。
