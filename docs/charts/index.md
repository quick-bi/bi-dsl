# 图表选型（how-to）

> reference（字段契约）见各分册；本页只讲"选哪个 type / 怎么组合"，遵循 Diátaxis 将 how-to 与 reference 分离。

## 场景 → type → 范式

| 场景 | type | 范式 |
| --- | --- | --- |
| 时间趋势 | `line` | encoding |
| 分类对比 | `bar` | encoding |
| 横向排名 | `strip` | encoding |
| 占比构成 | `pie` | encoding |
| 柱 + 线混合 | `combination` | encoding |
| 相关性 / 分布 | `scatter` | encoding |
| 转化流程 | `funnel` | encoding |
| 多维交叉明细 | `cross-table` | layout |
| 排行榜 | `ranking-list` | layout |
| KPI 单值 / 多指标 | `indicator-card` | indicator |
| 目标达成进度 | `progress` | progress |

## 四范式（决定 encoding 怎么写）

- **encoding**：bar / line / strip / combination / pie / scatter / funnel —— 通过视觉通道（x / y / color / theta …）绑定字段
- **layout（table）**：cross-table / ranking-list —— 行列 / 明细结构
- **indicator**：indicator-card —— indicators 数组
- **progress**：progress —— 进度项 + 目标

## 聚合速记

金额 → SUM · 比率 → AVG · UV → COUNT_DISTINCT · 条数 → COUNT · 极值 → MAX / MIN

## 分册

- [bar.md](bar.md)：分类对比；多系列可 group / stack / percent。范式：encoding。
- [line.md](line.md)：时间趋势 / 连续变化。范式：encoding。
- [strip.md](strip.md)：横向排名 / 长类目。范式：encoding。
- [combination.md](combination.md)：柱 + 线混合、双轴。范式：encoding。
- [pie.md](pie.md)：占比构成；用 theta + color，不用 x + y。范式：encoding。
- [scatter.md](scatter.md)：相关性 / 分布。范式：encoding。
- [funnel.md](funnel.md)：转化流程。范式：encoding。
- [cross-table.md](cross-table.md)：多维交叉明细。范式：layout。
- [ranking-list.md](ranking-list.md)：带数据条的排名列表。范式：layout。
- [indicator-card.md](indicator-card.md)：KPI 单值 / 多指标卡。范式：indicator。
- [progress.md](progress.md)：目标达成进度。范式：progress。
