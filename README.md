# Vibe Coding Knowledge Base

> **把每个项目阶段的经验，系统化沉淀成可复用的知识资产。**

这是一个专注于 **Vibe Coding** 实践经验的开源知识库。  
目标不是堆砌代码，而是记录「在 AI 辅助下做项目时，每个阶段真正有效的思考、提示词、决策、踩坑与反思」。

---

## 核心理念

Vibe Coding 的本质是 **人机协作的意图表达与验证循环**。  
经验如果只留在对话记录或个人笔记里，很快就会丢失。  
本仓库把「阶段」作为最小沉淀单元，强制每个重要项目阶段都产出结构化记录。

**我们沉淀的不是结果，而是过程中的决策与洞察。**

---

## 仓库结构

```
vibe-coding-knowledge-base/
├── docs/
│   ├── 00-philosophy.md          # 知识沉淀哲学与原则
│   ├── stages/                   # 项目阶段模板（强烈建议按此顺序记录）
│   │   ├── 01-ideation.md
│   │   ├── 02-planning-context.md
│   │   ├── 03-implementation.md
│   │   ├── 04-debug-validate.md
│   │   └── 05-reflection.md
│   └── templates/
│       └── stage-log.md          # 单个阶段的记录模板（复制使用）
├── projects/                     # 真实项目经验归档（按项目建文件夹）
│   └── _example-project/
├── prompts/                      # 可复用、经过验证的提示词库
├── lessons/                      # 跨项目提炼的通用教训
├── tools/                        # 工具使用经验（Cursor / Grok / Godot / Claude 等）
└── CONTRIBUTING.md
```

---

## 如何使用这个知识库

### 1. 为自己的项目沉淀经验
1. 在 `projects/` 下新建文件夹，以项目名命名。
2. 复制 `docs/templates/stage-log.md`。
3. 按阶段填写（不必每个项目都填满五个阶段，重要阶段优先）。
4. 把可复用的提示词提炼到 `prompts/`。
5. 把跨项目通用的洞见写到 `lessons/`。

### 2. 作为 AI 上下文使用
把本仓库作为 Cursor / Claude Code / Grok 的长期上下文源：
- 在项目根目录引用相关 `lessons/` 或 `prompts/`。
- 在新项目开始时，先读一遍相关阶段的历史记录。

### 3. 社区贡献
欢迎提交你自己的阶段经验（见 [CONTRIBUTING.md](CONTRIBUTING.md)）。  
我们更看重「真实踩坑 + 反思」而不是完美成功案例。

---

## 推荐工作流（与 Vibe Coding 对齐）

```
探索意图 → 写清楚 Context & 约束 → 小步实现 + 频繁验证 → 记录决策与失败 → 提炼可复用模式
```

每完成一个有价值的阶段，就花 5–15 分钟写一条 stage-log。  
长期坚持后，这个仓库会成为你个人最强的「AI 协作记忆」。

---

## License

MIT License. 欢迎 fork、改造、用于个人或团队知识管理。

---

**开始行动**：先去看 `docs/00-philosophy.md`，然后复制一份 `docs/templates/stage-log.md` 试试。
