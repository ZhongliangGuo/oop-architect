# OOP Architect

[English](README.md)

一个 [Claude Code](https://claude.ai/code) Skill，通过在 `CLAUDE.md` 中维护实时 Mermaid UML 图来设计、记录和追踪面向对象软件架构。

## 能做什么

当你开始或回到一个项目时，你需要立刻了解：什么已经完成、什么在进行中、各部分如何连接、有哪些约束。这个 Skill 把 `CLAUDE.md` 变成一份随代码自动更新的架构蓝图。

### 四种工作模式

| 情况 | 行为 |
|---|---|
| 新项目，还没有代码 | 从零设计类层次结构，生成 `CLAUDE.md` |
| 已有代码，没有 `CLAUDE.md` | 扫描代码，反向生成架构文档 |
| 已有项目，要新增功能 | 在现有架构上规划新组件 |
| 代码和 `CLAUDE.md` 已经不同步 | 全量 resync——扫描代码更新所有图表 |

### 生成内容

- **类图**：带完整类型签名、可见性标记（`+` `-` `#`）和每个类的实现状态（✅ 完成 / 🔶 部分完成 / 🔲 未开始）
- **时序图**：关键工作流（认证、请求生命周期等）
- **组件图**：多模块项目的模块依赖关系
- **进度表**、目录结构、设计决策、约束说明
- **内嵌维护规则**：让 `CLAUDE.md` 在不激活 Skill 的情况下自我更新

### 支持的语言

Python · Java · C# · Kotlin · TypeScript · JavaScript · Go · Rust · C++ · Swift · Ruby · PHP · 通用 OOP 兜底

---

## 安装

**项目级安装**（推荐团队使用，提交到仓库）：
```bash
git clone https://github.com/YOUR_USERNAME/oop-architect .claude/skills/oop-architect
```

**全局安装**（所有项目可用）：
```bash
git clone https://github.com/YOUR_USERNAME/oop-architect ~/.claude/skills/oop-architect
```

更新：
```bash
cd .claude/skills/oop-architect   # 或 ~/.claude/skills/oop-architect
git pull
```

---

## 使用方式

当你说以下类似的话时，Skill 会自动激活：

- *"帮我规划一下这个项目的架构"*
- *"设计一下任务队列系统的类"*
- *"我想新增一个功能：后台任务重试"*
- *"同步一下架构"* / *"从代码更新 CLAUDE.md"*
- *"给这个已有的项目生成 CLAUDE.md"*

也可以手动触发：`/oop-architect`

初始化之后，`CLAUDE.md` 会自我维护。Claude Code 在每次任务开始时读取其中内嵌的维护规则，在公共接口变化时自动更新图表，不需要再次激活 Skill。

---

## 背景

这个 Skill 源于一个 vibe coding 的真实痛点：编码过程总是被打断。几小时或几天后再回来，完全不记得哪些已经实现、哪些依赖什么、哪些约束是已经想清楚的。靠重读代码来重建心智模型既费时又容易遗漏。

解决方案是让 `CLAUDE.md` 成为一份活的架构蓝图——用 Mermaid UML 图追踪每个类、每个方法、每条关系的实现状态（✅ 完成 / 🔶 进行中 / 🔲 未开始），始终和代码保持同步。

**核心设计决策**是"维护规则放在哪里"。直觉上应该放在 Skill 里——但这意味着 Skill 需要在每次任务中都保持激活。更好的答案是：把维护规则直接写进生成的 `CLAUDE.md`。由于 Claude Code 在每次任务开始时都会自动加载 `CLAUDE.md`，这些规则就会被自然遵守，不需要 Skill 一直在场。Skill 只在初始规划和全量 resync 时才需要运行。

**专为 vibe coder 设计。** 许多用 Claude Code 做大型项目的用户懂 OOP，但不一定熟悉正式的设计模式。这个 Skill 在内部使用良好的架构模式，但始终用大白话解释——不说"这里用了工厂模式"，而说"新增一个数据库适配器只需要创建一个新文件，其他任何地方都不需要改"。模式名称只作为可选的补充注释，供有兴趣的用户查阅。

---

## 设计思路

### 原子化 reference 加载

大多数 Skill 会一次性把所有内容加载进上下文。这个 Skill 只加载当前任务需要的部分：

- **始终加载：** `SKILL.md`（约 95 行）+ 对应语言文件（约 25 行）
- **按阶段加载：** `references/uml-class.md`、`references/claude-md-template.md` 等
- **不需要就不加载：** 时序图/组件图规则、resync 流程、模板文件

这使得四种模式、所有语言下的上下文消耗都保持精简。

### 自我维护的 `CLAUDE.md`

生成的 `CLAUDE.md` 内嵌了自己的更新规则。Claude Code 在每次任务开始时都会读取并遵循这些规则——日常更新不需要激活 Skill，Skill 只在初始规划和全量 resync 时运行。

### 什么时候不该用这个 Skill

如果项目是单文件脚本、一次性数据处理、或纯函数式且没有共享状态，Skill 会直接告诉你，并建议更简单的方案，而不是强行套一个类层次结构。

---

## 文件结构

```
oop-architect/
├── SKILL.md                       # 入口——模式检测和编排逻辑
└── references/
    ├── uml-class.md               # 类图规则（Phase 1 始终加载）
    ├── uml-sequence.md            # 时序图规则（按需加载）
    ├── uml-component.md           # 组件图规则（按需加载）
    ├── claude-md-template.md      # CLAUDE.md 模板（新建时加载）
    ├── resync.md                  # 全量 resync 流程（Phase 2）
    ├── generate-from-code.md      # 从已有代码反向生成文档（Phase 3）
    ├── extend-design.md           # 在现有架构上扩展新功能（Phase 4）
    └── langs/
        ├── python.md
        ├── java-csharp-kotlin.md
        ├── typescript-javascript.md
        ├── go.md
        ├── rust.md
        ├── cpp.md
        ├── swift.md
        ├── ruby.md
        ├── php.md
        └── generic.md             # 其他语言的通用兜底
```
