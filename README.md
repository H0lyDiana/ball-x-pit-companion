# 球比伦战记 · 图鉴伴侣（BALL x PIT Companion）

**🔗 线上站点：[h0lydiana.github.io/ball-x-pit-companion](https://h0lydiana.github.io/ball-x-pit-companion/)**

**📦 仓库：[github.com/H0lyDiana/ball-x-pit-companion](https://github.com/H0lyDiana/ball-x-pit-companion)**

[English README](README.en.md)

本仓库是 **BALL x PIT**（官方简中《球比伦战记》，Kenny Sun and Friends 开发、
Devolver Digital 发行，2025 年 10 月）的粉丝伴侣站：把融合核心里的每一条弹珠进化
配方做成可搜索的图谱，并为每名角色给出协同判定；纯静态站点，离线也能用。

本站是 [tomaskir/ball-x-pit-companion](https://github.com/tomaskir/ball-x-pit-companion)
的简体中文分支，代码与数据模型沿用上游，中文文本取自游戏内置官方中文。

## 中文本地化

简体中文直接取自游戏内置官方中文（《球比伦战记》v1.308 的 I2 Localization
字符串表）：115 颗弹珠、116 件被动物品、31 名角色、114 段三阶效果文本与界面术语
均使用官方译名。站点默认中文，右上角的 **EN / 中** 按钮可切换英文（偏好写入
localStorage 后整页重载）。

官方术语：弹珠（ball）、迷你弹珠（baby ball）、被动物品（passive）、融合核心
（Fusion Reactor）、升天球比伦（Risen Ballbylon）、深坑（the Pit）。官方效果文本
中的变量占位符用本站数值填充。来源、覆盖范围与维护方式见
[`docs/localization/zh-CN.md`](docs/localization/zh-CN.md)；中文词表在
`src/i18n/zh/`，`src/data/*.ts` 保持生成物的英文原文不动。

## 功能

- **全部 115 颗弹珠**：25 颗基础弹珠、迷你弹珠，以及融合核心产出的 89 颗进化弹珠
  （75 颗二阶 + 14 颗三阶），按 基础 / 进化 / 三阶 分组。每个格子都用紧凑记号
  内联显示融合配方（如 `黑铁 + (幽灵/黑暗)`）。
- **展示进化链，而不只是两两查询。** 点击任意弹珠即可一次性高亮整条配方图谱：
  组成材料、备选配方，以及它能进化成的一切，多步链路同样覆盖
  （例如 燃烧 → 太阳 → 黑洞）。
- **全部 116 件被动物品**：77 件基础 + 39 件进化，并附进化配方。
- **角色协同检查。** 最多选择 2 名角色（共 31 名），每颗弹珠/每件被动物品都会根据
  标签重合度给出红/绿判定，悬停可看解释。两名角色意见冲突时红色优先，冲突会先
  暴露出来（例如空巢老人和残缺的西西弗斯没有迷你弹珠 → 所有依赖迷你弹珠生成或
  成长的内容都会变红）。
- **角色图鉴**：全部 31 名角色，附基础弹珠与特性文本。
- **构筑（Plan）页面**：按游戏的栏位上限组建一局的角色、弹珠、被动物品与融合组合
  （含“终局强化”开关和角色专属特性），查看逐条协同判定与超限标记，并得到一份
  需要刷取的全部材料的构建图。构筑可通过链接分享。
- **本体 / 扩展内容筛选。** 每个页面右上角有两个复选框（每个版本一个，默认只开
  本体），可在弹珠、被动物品、融合、角色与构筑页面隐藏扩展内容。隐藏内容会被
  移除而不是变暗，顶部会用提示条说明本次切换隐藏了多少条目。
- **融合页面**：任选两颗未融合的三阶弹珠，查看合成后的融合弹珠——合并后的效果
  文本、跨线互动（例如生成/范围/场地载体把伙伴的命中状态带出去）、顺序副作用与
  注意事项。游戏本身没有融合表，合成遵循社区观察到的规则，并用 370 对样本的证据
  库校验；这是本站的编辑模型，不是游戏数据（见
  [`docs/research/fusion-mechanics.md`](docs/research/fusion-mechanics.md)）。
- **逐页搜索**：按名称或效果文本搜索；切换页面时选择会保留。深色/浅色主题。
  无后端、无追踪，单页静态站点。

## 数据

本体数据于 2026-09-13 从 [ballxpit.wiki.gg](https://ballxpit.wiki.gg) 转录
（游戏 v1.301，*Naturalist* 更新），并与社区“Ultimate Guide of Evolutions”图表
交叉核对，两者一致。*升天球比伦* 扩展的数据（24 颗弹珠、45 件被动物品、8 名角色、
24 段三阶文本）来自 BALL x PIT v1.308 的解包（2026-11-13）。完整事实库（含每个
实体的效果文本）在 [`docs/research/game-mechanics.md`](docs/research/game-mechanics.md)；
站点的协同标签模型手工维护在 `scripts/editorial.ts`。

数量：115 颗弹珠、116 件被动物品、31 名角色、114 段三阶文本，以及 30 个标签的
编辑词表。媒人（Matchmaker）在 30 名可配对角色之间禁止 43 对组合
（虚假弥赛亚不与任何人配对）。

以上数字是截至上述日期的 wiki/解包结果；wiki 本身也带有未完成标记，游戏更新后
请重新核对。协同判定是本站根据角色特性文本推导的编辑模型，未经实战验证。

## 开发

```sh
npm install
npm run dev       # astro dev
npm test          # vitest run，同时是 CI 门禁（含 tsc --noEmit）
npm run build     # astro build → dist/
```

领域词表见 [`GLOSSARY.md`](GLOSSARY.md)；贡献者与 Agent 规则见
[`AGENTS.md`](AGENTS.md)。

### 架构

静态 Astro 5 页面 + 一个原生 TS 交互岛，按单一职责拆分为多个模块：

| 模块 | 职责 |
|---|---|
| `src/companion.ts` | 交互岛：组合根——启动/销毁、构筑持久化、hash 路由 |
| `src/view-state.ts` | 全部状态与派生：`dispatch(action) → ViewModel` |
| `src/renderer.ts` | 全部 DOM 绘制：一次构建、原地重绘（图标不闪烁） |
| `src/edition-gate.ts` | 内容筛选规则：版本可见性、配方/融合门控 |
| `src/passive-availability.ts` | 按角色的被动物品白名单与属性门槛规则 |
| `src/slot-limits.ts` | 构筑容量与角色专属栏位特性 |
| `src/plan-state.ts` | 构筑状态与派生 |
| `src/build-graph.ts` | 构筑的材料图派生与布局 |
| `src/fusion.ts` | 纯融合合成器：`fuse(a, b)` → 合成后的融合弹珠文本 |
| `src/graph.ts` | 纯进化图工具：深度、高亮游走、配方记号 |
| `src/catalog.ts` | 带索引的弹珠/被动物品集合；命名空间解析 |
| `src/synergy.ts` | 基于标签重合度的红/绿判定逻辑 |
| `src/icon-url.ts` | 基础 URL × 图标路径的拼接 |

`GLOSSARY.md` 是领域词表，模块头部的注释沿用同一套词汇。架构不变量（命名空间
隔离、结构深度、配方记号因式分解）记录在该文件中，并由测试套件强制执行。

### 数据管线

`src/data/` 下的数据文件是**生成物**，不要手工修改：

1. `docs/research/game-mechanics.md`，手工维护的事实库（本体的 wiki 表格、扩展的
   v1.308 解包）。
2. `node --experimental-strip-types scripts/parse-wiki.ts` → `src/data/parsed.json`。
   进化深度由配方图结构计算，不依赖 wiki 标注。
3. `node --experimental-strip-types scripts/emit-data.ts` → `src/data/*.ts`。
   协同标签与逐角色判定手工维护在 `scripts/editorial.ts`；生成器在写盘前会校验
   所有交叉引用。

融合模型是独立的：`src/fusion.ts` 依据社区观察到的规则，用两个组成弹珠的效果文本
合成融合弹珠文本，并用
[`docs/research/fusion-observations/`](docs/research/fusion-observations/) 里的
370 对证据库校验——那是一份可执行规范（`src/corpus.test.ts`）。证据库早于扩展
弹珠，因此只覆盖本体目录。提炼后的机制说明在
[`docs/research/fusion-mechanics.md`](docs/research/fusion-mechanics.md)。

### 部署

GitHub Actions（`.github/workflows/deploy.yml`）在每次推送 `main` 和每个 PR 上
运行测试套件，然后用 Astro 构建并部署到 GitHub Pages。本次部署地址：
<https://h0lydiana.github.io/ball-x-pit-companion/>。

## 致谢与许可

代码：[MIT](LICENSE) © 2026 Tomas Kirnak；简体中文本地化由
[H0lyDiana](https://github.com/H0lyDiana) 维护。

`public/icons/` 中的游戏图标（293 个 PNG）来自 [ballxpit.wiki.gg](https://ballxpit.wiki.gg)
的本体 wiki 美术，以及从 v1.308 游戏资源中提取的 *升天球比伦* 精灵；明细与各目录
数量见 [`public/icons/CREDITS.md`](public/icons/CREDITS.md)。Ball x Pit 游戏美术
版权归 Kenny Sun（Kenomi LLC）与 wiki.gg 贡献者所有；图标未经授权使用，仅用于这个
非商业粉丝工具中的识别目的，版权仍归原作者所有。本站与版权方无隶属关系。

其他资源：[ballxpit.wiki.gg](https://ballxpit.wiki.gg)（社区 wiki）·
[r/BALLxPIT](https://www.reddit.com/r/BALLxPIT/) ·
[Steam 社区指南](https://steamcommunity.com/app/2062430/guides)。
