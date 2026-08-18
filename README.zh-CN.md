# zero-to-design

[English](README.md) · **简体中文**

一个交互式 agent skill，既支持从零建立设计系统，也支持接入已有系统后增量设计页面和组件。已有系统可以直接复用现有设计资产；如果没有设计文档，skill 会先探索系统并提取一套可追踪的设计基线，再进入核心页面扩展或针对性的跨屏打磨。

👉 **在线示例：** [Pulse（含可交互产物）](https://mitaraifail.github.io/zero-to-design/)

```mermaid
flowchart TD
    Existing["<b>已有系统入口</b><br/>复用资产 / 探索系统"]
    P1["<b>Phase 1 · 产品定义</b> → 01-product.md"]
    P2["<b>Phase 2 · 参考图收集</b> → 02-references.md"]
    P3["<b>Phase 3 · 方向选择</b> → 03-directions.html"]
    P4["<b>Phase 4 · 首屏迭代</b> → 04-screen-v*.html（或 04-screen1-screen2-v*.html）"]
    Draft["生成 <b>DESIGN.draft.md</b><br/>十章骨架草稿 · 反馈循环中枢"]
    P7["<b>Phase 7 · 固化设计系统</b><br/>→ DESIGN.md + tokens.css + assets/"]

    subgraph OPT["核心页面扩展与跨屏打磨"]
        P5["<b>Phase 5 · 核心页面扩展</b><br/>→ 05-screen*.html · 页面地图"]
        P6["<b>Phase 6 · 跨屏打磨</b><br/>→ 打磨日志 · 维度评审"]
    end

    Existing -->|新增核心页面| P5
    Existing -->|局部改进| P6
    P1 --> P2 --> P3
    P3 --> C1{用户选择}
    C1 -->|选字母 / 组合| P4
    C1 -->|都不对| P3
    P4 --> C2{用户反馈}
    C2 -->|改 X| P4
    C2 -->|方向错了| P3
    C2 -->|不错| Draft
    Draft --> C3{分流决策}
    C3 -->|多页面产品| P5
    C3 -->|只需单页| P6
    P5 -->|核心页面齐了| P6
    P6 -->|各维度都 OK| P7
    P7 --> Done(["完成 · DESIGN.md 留在 design/<br/>AGENTS.md 已关联引用"])
    Done -.->|之后设计新页面（扩展模式）| P6
```

## 它能做什么

`zero-to-design` 是一个为 AI coding agent 设计的对话式设计工作流，专为后端工程师和非设计师打造。它支持两类任务：从零建立设计系统，或接入已有系统后继续设计多屏页面和组件。已有系统入口会优先寻找并验证现有 `DESIGN.md`、Token、组件和工程约束；如果这些资产不存在，则通过代码与运行中的页面探索生成“观察得到的设计基线”。新增核心页面进入 Phase 5，局部改进则可以直接进入 Phase 6。

| Phase | 名称 | 产出 |
|-------|------|------|
| 1 | 产品定义 | `01-product.md` — 8 个关键问题锁定"做什么、做成什么感觉" |
| 2 | 灵感收集 | `02-references.md` — 参考网站、截图标注、喜欢/不喜欢、显式偏好 |
| 3 | 方向选择 | `03-directions.html` — 3-4 个真正不同的设计方向，每个含配色、字体、布局和可交互的签名动作 |
| 4 | 首屏迭代 | `04-<screen>-v*.html`（或 `04-<screen1>-<screen2>-v*.html`）+ `DESIGN.draft.md` — 迭代 1–2 个关键首屏直到你说"不错" |
| 5 | 核心页面扩展 | `05-<screen>.html` + `05-screen-map.md` + `component-inventory.md` — 最小核心页面集、真实状态与实现契约 |
| 6 | 跨屏打磨 | `06-polish-log.md` + 可选维度评审页 — 字体、间距、色彩、组件、响应式、无障碍与动效 |
| 7 | 设计系统固化 | `DESIGN.md` + `tokens.css` + `assets/` — 最终可复用的设计系统，并在 AGENTS.md 中关联引用 |

## 为什么写这个 skill

我最近要从零搭一个新网站。最难的部分不是代码——而是让 AI 生成的界面既好看，又能保持一致。

这段经历沉淀出一条三步路径，最终长成了 `zero-to-design`。

**第一步："AI 味"只是缺少方向的产物。**
让模型"做一个现代感的落地页"而不给任何具体要求时，它返回的是训练数据的统计平均值：紫色渐变、Inter 字体、三列功能卡、fade-up 动画。现有的"去 AI 味"技能可能矫枉过正，把你真正喜欢的东西也一并抹掉。真正的解法是同时给模型正向的设计指导和明确的红线规则。

**第二步：这些规则的容器是 `DESIGN.md`。**
没有单一事实来源时，agent 写的每个页面都会漂移：不同的按钮、不同的间距、不同的交互模式。`DESIGN.md` 正在成为 AI 可读设计系统的事实标准——颜色、字体、组件、UX 约束、Do/Don't 规则全部写在一个文件里，再从 `AGENTS.md` 引用。

**第三步：难的是从零建立第一份有审美的 `DESIGN.md`。**
知道规范该放在哪儿很容易，知道该往里写什么才难——尤其当你不是设计师的时候。`zero-to-design` 就是带你走过这段鸿沟的引导式对话：产品定义、参考收集、方向选择、首屏迭代、核心页面扩展、跨屏打磨、最终固化。

简言之：**去 AI 味只是起点，DESIGN.md 是容器，而 `zero-to-design` 解决的是从零建立这个容器的最后一公里。**

## 特点

- **对话式引导**——每一步都解释"为什么"，并给出具体可选项；自由输入的回答永远被接受，不会被强行映射回预设选项
- **动态发现设计约束 skill**——扫描你的环境中的 [`impeccable`](https://github.com/pbakaus/impeccable) 和 `frontend-design` 等 skill，验证可用性后由你确认使用哪套约束；优先推荐 `impeccable`
- **已有系统接入**——支持复用已有设计资产，也支持从代码和运行页面探索出设计基线；新增核心页面进入 Phase 5，局部改进进入 Phase 6
- **多候选探索**——Phase 5 可比较核心页面结构，Phase 6 可在既有 `DESIGN.md` 约束内比较各维度的打磨方案
- **活的 DESIGN.md**——从 Phase 4 起设计决策就累积进 `DESIGN.draft.md`，随你的反馈持续演进，Phase 7 固化；完成后还有扩展模式，可以基于已有设计系统继续设计新页面
- **自动语言匹配**——skill 会识别你的语言，并用它运行整个体验（对话、提问、以及每一个生成的产出物）；只有文件名、token 名和代码标识符保持英文

## 安装

### 通过 skills CLI（推荐）

```bash
npx skills add mitaraifail/zero-to-design
```

> 也可以加 `-g` 安装到全局，对所有项目生效。

### 更新

更新已经安装的 skill 时，在原来的项目目录中重新运行同一条命令：

```bash
npx skills add mitaraifail/zero-to-design
```

如果当初是全局安装，请保留 `-g`：

```bash
npx skills add mitaraifail/zero-to-design -g
```

更新后请重启 Agent 会话，让它重新加载最新的 `SKILL.md`。如果本地修改过 skill，重新安装可能覆盖这些修改，请先备份。

### 手动安装

克隆仓库并拷贝到你的 agent 的 skills 目录：

```bash
git clone https://github.com/mitaraifail/zero-to-design.git

# Claude Code
cp -r zero-to-design ~/.claude/skills/

# Kimi Code CLI
cp -r zero-to-design ~/.agents/skills/
```

### 卸载

```bash
npx skills remove zero-to-design
```

如果是全局安装，加 `-g`：

```bash
npx skills remove -g zero-to-design
```

## 使用

直接用任何语言描述你要设计的东西：

- "I want to design a landing page from scratch"
- "Help me build a design system for my SaaS dashboard"
- "在现有 Nuxt 系统里设计账户页"
- "分析这个项目现有的 UI，然后继续设计订单详情页"
- "从 0 设计一个首页"
- "帮我走一遍品牌设计流程"

skill 会先检查是否存在 `design/state.md`，被中断的 session 会从上次进度继续。

## 利用你已有的 skills

`zero-to-design` 没有硬依赖。它不会要求你安装任何东西，而是在 Phase 3 **扫描你环境中已经安装的 design 相关 skill**（比如 [`impeccable`](https://github.com/pbakaus/impeccable) 的子 skill 如 `bolder` / `typeset` / `layout`，或 [`frontend-design`](https://github.com/anthropics/skills) 作为备选），验证哪些真的可用，列出清单，**由你决定本次使用哪些**，后续 Phase 沿用你的选择。推荐首选 `impeccable` 作为约束层；当 `impeccable` 不可用时，`frontend-design` 也是不错的备选。

如果没有发现任何设计 skill，工作流会使用内置 fallback 规则（字体/配色/布局/文案禁令）继续，并告知你当前使用的约束来源。

## License

[MIT](LICENSE)
