# 简体中文本地化说明

本仓库是 **BALL x PIT** 的粉丝伴侣站。此分支的简体中文直接取自游戏内置官方
中文（《球比伦战记》v1.308），默认中文，可切换回英文。

## 数据来源

游戏安装路径：`D:\Steam\steamapps\common\BALLxPIT`

- 官方文本位于 `Balls_Data/resources.assets` 的 **I2 Localization** 字符串表
  （`I2Languages` / `I2Languages_DLC`，Unity 资源，MonoBehaviour 内嵌）。
- 用 UnityPy 解包后按 I2 的 `TermData` 结构读出每个词条的 16 种语言；第 1 列
  为简体中文，第 9 列为繁体中文。
- 实体词条使用固定键：`Generated/hupg_<slug>_name/_desc`（弹珠）、
  `Generated/pass_<slug>_name/_desc`（被动物品）、
  `Generated/char_<slug>_name/_desc/_flavordesc`（角色）。
- 版本号：`Balls_Data/resources.assets` 内 `BuildVersion` = 1.308（2026-10-12）。

## 官方术语

| 英文 | 官方简中 |
| --- | --- |
| ball | 弹珠 |
| baby ball | 迷你弹珠 |
| passive | 被动物品 |
| fusion / Fusion Reactor | 融合 / 融合核心 |
| evolution | 进化 |
| the Pit | 深坑 |
| Risen Ballbylon（DLC） | 升天球比伦 |
| character | 角色 |

站点的“球体”“被动”等旧译已全部替换为官方术语；界面自身的新造词（如“构筑”、
“协同”）不属于游戏术语，保持站点风格。

## 覆盖范围

| 内容 | 条目 | 来源 |
| --- | --- | --- |
| 弹珠名称 | 115 | 114 条 `hupg_*_name` + 迷你弹珠（游戏 UI） |
| 弹珠一级效果 | 115 | 官方模板 + 本站数值填充（97 条自动，18 条手工补全） |
| 弹珠三阶效果（融合用） | 114 | 官方模板 + 本站三阶数值填充（113 条自动，核弹 1 条手工） |
| 被动物品名称 | 116 | `pass_*_name` |
| 被动物品效果 | 116 | 官方模板 + 数值填充（98 条自动，18 条手工） |
| 角色名称 | 31 | `char_*_name` |
| 角色特性 | 31 | `char_*_desc` 原文 |
| 界面文案 / 标签 / 判定说明 / 融合说明 | ~200 条 | 本站文案，术语对齐官方 |

官方模板中的 `{[变量]}` 用本站英文底稿里的具体数值填充（例如
`施加{[bleed_amt]}层流血` + `2` → `施加2层流血`）。当本站英文底稿省略了官方
模板的尾句（如烟花缺少燃烧伤害数值）时，保留能填满的句子，避免出现占位符。

## 实现

```
src/i18n/
  index.ts          语言状态、t()、实体访问器、静态外壳套用
  catalog.ts        展示层集合（name/effects/quirk 已本地化）
  zh/balls.ts       115 条弹珠词条（官方名称/效果）
  zh/passives.ts    116 条被动物品词条
  zh/characters.ts  31 条角色词条
  zh/level3.ts      114 条三阶文本
  zh/ui.ts          界面文案、标签、判定说明、融合说明、属性名
```

- 数据文件 `src/data/*.ts` 保持英文原文（生成物，测试会比对生成结果）；中文在
  `src/i18n/catalog.ts` 处替换后进入 `catalog` 索引。
- 融合推演的通道判定依赖英文效果文本的正则，因此 `componentText()` 仍返回英文；
  展示段落走 `level3Effect()`。中文不参与规则判定。
- 融合合成时伤害区间抽象为 `X`：中文规则匹配“数字/区间 + 伤害”（如
  `50-70伤害`）；百分比与倍率因中间夹着 `%`／`倍` 而保留。

## 验证

- `src/i18n.test.ts`：词表覆盖（缺键会回退英文）、官方术语、融合中文输出。
- 数值一致性检查：按官方模板填充后逐条比对中英文中的数字集合（容忍
  “25% less” 官方写作 “75%” 的换算）。

## 维护

游戏更新后重新解包 `resources.assets` 的 I2 字符串表，按 `slug` 更新
`src/i18n/zh/*.ts` 即可；数据管线、逻辑与测试都不需要改动。若官方修改了术语，
只需同步 `zh/ui.ts` 与静态外壳。
