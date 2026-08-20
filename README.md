# Vibe Coding Knowledge Base

跟 AI 写代码，聊完就忘。这个仓库用来把当时怎么想的写下来。

不是成品备份，也不是教程站。是决策、翻车、以及换个项目还用得上的判断。

## 想先看真人故事

第一份完整记录是 [DirectorDesk](projects/mira_new/)：C++ 做的 3D 导演台，两天 vibe coding 走出可安装的 P0。地图怎么先写、渲染怎么闪过、后来为什么不继续拆模块，都在那个文件夹里。

不想顺着项目读，直接看 [lessons](lessons/README.md)。常用的几篇：

- [01 · 聊天为什么靠不住](lessons/01-聊天为什么靠不住.md)
- [02 · 接缝和空房间](lessons/02-接缝和空房间.md)
- [03 · 先做完，再谈专业](lessons/03-先做完再谈专业.md)
- [04 · 别人给的建议往哪放](lessons/04-别人给的建议先放进地图.md)
- [05 · IA 到底管什么](lessons/05-IA到底管什么.md)
- [06 · 骨架锁死之后怎么改](lessons/06-骨架锁死之后怎么改.md)

填表用 [建议卡](docs/templates/advice-intake.md) 和 [IA 骨架](docs/templates/ia-skeleton.md)。给 AI 复制的短指令在 `prompts/architecture/`。

产品仓库：[mira_new](https://github.com/wisdom-km/mira_new)。架构图：[Pages](https://wisdom-km.github.io/mira_new/)。

## 里面有什么

```
docs/          怎么记、记什么（哲学、阶段说明、空白表）
projects/      真实项目，按文件夹归档
lessons/       抽出来、换项目还能用的判断
prompts/       真用过的提示词
tools/         某个工具自己的坑（现在几乎是空的）
```

`docs/stages/` 是五个阶段各自该写什么。动手时复制 `docs/templates/stage-log.md` 到自己的项目文件夹就行，不必五个阶段都填满。

## 自己记一笔

在 `projects/` 下建一个以项目名命名的文件夹。把当时的约束、选了什么、翻了什么车写进去。过几天回头看，哪一句换个项目还成立，再挪到 `lessons/` 或 `prompts/`。

给 AI 当长期记忆用也可以：新开对话时，先让它读相关的 lesson，别把整段聊天记录贴回去。

怎么投稿见 [CONTRIBUTING.md](CONTRIBUTING.md)。真实踩坑比完美成功有用。

## License

MIT。欢迎 fork、改成自己的记法。
