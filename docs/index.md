# bi-dsl API 文档

> 基于 [valibot](https://valibot.dev/) 的运行时 schema + 反推 TS 类型，描述图表 / 看板 / 分析单元 / OLAP 查询的契约。命名对称：`XxxSchema`（运行时校验）↔ `Xxx`（`v.InferOutput` 反推的 TS 类型）。

## 怎么读（按需加载，顺序即优先级）

- 想一次性拿全部 → [llms-full.md](llms-full.md)：所有分册拼成一份
- 选图表类型 → [charts/index.md](charts/index.md)：选型决策树 + 四范式对照
- 取数 / 查询意图 → [olap.md](olap.md)：维度 / 度量 / 过滤 / 排序 / 高级计算
- 看板骨架 → [dashboard.md](dashboard.md)：DashboardSpec / 布局 / 卡片 / 组件 / 查询控件
- 具体图表字段 → [charts/](charts/)：bar / line / pie … 共 11 份分册
- 交互 → [interaction.md](interaction.md)：下钻 / 联动
- 通用原子 → [atom-config.md](atom-config.md)：encoding / 轴 / 图例 / 标签 / 提示框 / 配色 / 格式化 / 条件格式
- 工具函数 → [functions.md](functions.md)
- 常量 / 共享 entries → [constants.md](constants.md)

## 命名与生成公约（生成 DSL 必看）

- `type` 用 kebab-case（`cross-table` / `indicator-card` / `ranking-list`；例外 `query_control`）
- 字段 key 用 `snake_case`
- `encoding.y` 是数组；饼图用 `theta` + `color`（不用 `x` + `y`）
- `version` 固定 `"1.0.0"`；布局 24 列栅格，`x + w ≤ 24`
- ID 前缀：`db_` / `cmp_` / `q_` / `lk_`，全局唯一
- 引用链：`dataset_ref` → `data_sources[].title`、`analysis_ref` → `analyses[].id`、`component_id` → `components[].id`

## 全 schema 索引

| schema | 文件 | 形态 |
| --- | --- | --- |
| `Alignment` | [atom-config.md](atom-config.md) | picklist |
| `AnalysisRef` | [dashboard.md](dashboard.md) | union |
| `AnalysisSpec` | [dashboard.md](dashboard.md) | object |
| `AuxiliaryLineSpec` | [atom-config.md](atom-config.md) | object |
| `AuxiliaryLineType` | [atom-config.md](atom-config.md) | picklist |
| `AxisSpec` | [atom-config.md](atom-config.md) | object |
| `BarChartOptions` | [charts/bar.md](charts/bar.md) | object |
| `BarChartSpec` | [charts/bar.md](charts/bar.md) | object |
| `BarOptions` | [charts/bar.md](charts/bar.md) | object |
| `BaseFieldDef` | [atom-config.md](atom-config.md) | object |
| `ChartAnalysisSpec` | [atom-config.md](atom-config.md) | object |
| `ChartBaseSpec` | [atom-config.md](atom-config.md) | object |
| `ChartSpec` | [dashboard.md](dashboard.md) | variant |
| `ColorSpec` | [atom-config.md](atom-config.md) | object |
| `CombinationChartOptions` | [charts/combination.md](charts/combination.md) | object |
| `CombinationChartSpec` | [charts/combination.md](charts/combination.md) | object |
| `CommonOptions` | [atom-config.md](atom-config.md) | object |
| `CommonSpec` | [dashboard.md](dashboard.md) | object |
| `ComparisonSpec` | [olap.md](olap.md) | object |
| `ComponentDrillSpec` | [atom-config.md](atom-config.md) | object |
| `ComponentInteractionSpec` | [atom-config.md](atom-config.md) | object |
| `ConditionalFormat` | [atom-config.md](atom-config.md) | array |
| `ConditionalFormatBase` | [atom-config.md](atom-config.md) | array |
| `ConditionalFormatOperator` | [atom-config.md](atom-config.md) | picklist |
| `ConditionalFormatQuery` | [atom-config.md](atom-config.md) | variant |
| `ConditionalFormatRule` | [atom-config.md](atom-config.md) | object |
| `ConditionalFormatRuleBase` | [atom-config.md](atom-config.md) | object |
| `ContainerSpec` | [dashboard.md](dashboard.md) | variant |
| `CrossTableDisplayMode` | [charts/cross-table.md](charts/cross-table.md) | picklist |
| `CrossTableInteractionSpec` | [charts/cross-table.md](charts/cross-table.md) | object |
| `CrossTableLayout` | [charts/cross-table.md](charts/cross-table.md) | object |
| `CrossTableOptions` | [charts/cross-table.md](charts/cross-table.md) | object |
| `CrossTableSpec` | [charts/cross-table.md](charts/cross-table.md) | object |
| `CrossTableThemeColors` | [charts/cross-table.md](charts/cross-table.md) | object |
| `CrossTableTotalDisplay` | [charts/cross-table.md](charts/cross-table.md) | object |
| `CumulativeSpec` | [olap.md](olap.md) | object |
| `DashboardCardSpec` | [dashboard.md](dashboard.md) | object |
| `DashboardComponentBaseSpec` | [dashboard.md](dashboard.md) | object |
| `DashboardComponentSpec` | [dashboard.md](dashboard.md) | variant |
| `DashboardFooterSpec` | [dashboard.md](dashboard.md) | object |
| `DashboardHeaderSpec` | [dashboard.md](dashboard.md) | object |
| `DashboardInteractionSpec` | [dashboard.md](dashboard.md) | object |
| `DashboardLayoutItemSpec` | [dashboard.md](dashboard.md) | object |
| `DashboardLayoutSpec` | [dashboard.md](dashboard.md) | object |
| `DashboardSpec` | [dashboard.md](dashboard.md) | object |
| `DashboardThemeSpec` | [dashboard.md](dashboard.md) | object |
| `DashboardUiChartSpec` | [dashboard.md](dashboard.md) | object |
| `DashboardUiDashboardSpec` | [dashboard.md](dashboard.md) | object |
| `DashboardUiSpec` | [dashboard.md](dashboard.md) | variant |
| `DataBarStyle` | [charts/ranking-list.md](charts/ranking-list.md) | object |
| `DataSourceRef` | [dashboard.md](dashboard.md) | object |
| `DateControlConfig` | [dashboard.md](dashboard.md) | object |
| `DateCumulativeSpec` | [olap.md](olap.md) | object |
| `DerivedField` | [olap.md](olap.md) | object |
| `DimensionBaseRef` | [olap.md](olap.md) | object |
| `DimensionGroupSpec` | [olap.md](olap.md) | object |
| `DimensionRef` | [olap.md](olap.md) | object |
| `DrillSpec` | [interaction.md](interaction.md) | variant |
| `DualAxisConfig` | [atom-config.md](atom-config.md) | object |
| `DualAxisOptions` | [atom-config.md](atom-config.md) | object |
| `DurationType` | [dashboard.md](dashboard.md) | picklist |
| `Encoding` | [atom-config.md](atom-config.md) | object |
| `EncodingMeasureRef` | [atom-config.md](atom-config.md) | union |
| `EnumControlConfig` | [dashboard.md](dashboard.md) | object |
| `FetchSourceType` | [dashboard.md](dashboard.md) | picklist |
| `FieldMapEntry` | [interaction.md](interaction.md) | object |
| `FieldMapFieldRef` | [interaction.md](interaction.md) | object |
| `FieldRef` | [atom-config.md](atom-config.md) | union |
| `FilterItem` | [olap.md](olap.md) | object |
| `FontTextStyle` | [atom-config.md](atom-config.md) | object |
| `FrozenConfig` | [charts/cross-table.md](charts/cross-table.md) | object |
| `FunnelCategoryLabel` | [charts/funnel.md](charts/funnel.md) | object |
| `FunnelChartSpec` | [charts/funnel.md](charts/funnel.md) | object |
| `FunnelDataLabel` | [charts/funnel.md](charts/funnel.md) | object |
| `FunnelOptions` | [charts/funnel.md](charts/funnel.md) | object |
| `FunnelRatioLabel` | [charts/funnel.md](charts/funnel.md) | object |
| `FunnelTotalRatioLabel` | [charts/funnel.md](charts/funnel.md) | object |
| `IndicatorCardMapping` | [charts/indicator-card.md](charts/indicator-card.md) | object |
| `IndicatorCardMetricRef` | [charts/indicator-card.md](charts/indicator-card.md) | union |
| `IndicatorCardOptions` | [charts/indicator-card.md](charts/indicator-card.md) | object |
| `IndicatorCardSpec` | [charts/indicator-card.md](charts/indicator-card.md) | object |
| `IndicatorFontStyle` | [charts/indicator-card.md](charts/indicator-card.md) | object |
| `IndicatorIconConfig` | [charts/indicator-card.md](charts/indicator-card.md) | object |
| `IndicatorIconItem` | [charts/indicator-card.md](charts/indicator-card.md) | object |
| `IndicatorSpec` | [dashboard.md](dashboard.md) | variant |
| `IndicatorSplit` | [charts/indicator-card.md](charts/indicator-card.md) | object |
| `InsightSpec` | [dashboard.md](dashboard.md) | object |
| `LabelContent` | [atom-config.md](atom-config.md) | picklist |
| `LabelDisplayMode` | [atom-config.md](atom-config.md) | picklist |
| `LabelPosition` | [atom-config.md](atom-config.md) | picklist |
| `LabelSpec` | [atom-config.md](atom-config.md) | object |
| `LegendAlign` | [atom-config.md](atom-config.md) | picklist |
| `LegendPosition` | [atom-config.md](atom-config.md) | picklist |
| `LegendSpec` | [atom-config.md](atom-config.md) | object |
| `LineChartOptions` | [charts/line.md](charts/line.md) | object |
| `LineChartSpec` | [charts/line.md](charts/line.md) | object |
| `LineOptions` | [charts/line.md](charts/line.md) | object |
| `LineStyle` | [atom-config.md](atom-config.md) | picklist |
| `LinkageRuleSpec` | [interaction.md](interaction.md) | object |
| `MainSubPosition` | [charts/indicator-card.md](charts/indicator-card.md) | picklist |
| `MeasureRef` | [olap.md](olap.md) | object |
| `MovingSpec` | [olap.md](olap.md) | object |
| `NumberControlConfig` | [dashboard.md](dashboard.md) | object |
| `NumberFormat` | [atom-config.md](atom-config.md) | union |
| `NumberFormatPreset` | [atom-config.md](atom-config.md) | picklist |
| `NumberOperator` | [dashboard.md](dashboard.md) | picklist |
| `OlapAggregate` | [olap.md](olap.md) | picklist |
| `OlapDslSpec` | [olap.md](olap.md) | object |
| `OlapFilterOperator` | [olap.md](olap.md) | picklist |
| `OlapGranularity` | [olap.md](olap.md) | picklist |
| `OlapTotalSpec` | [olap.md](olap.md) | object |
| `PageNavListMode` | [misc.md](misc.md) | picklist |
| `PageNavPlacement` | [misc.md](misc.md) | picklist |
| `PageNavSpec` | [misc.md](misc.md) | object |
| `PanelSpec` | [dashboard.md](dashboard.md) | object |
| `PercentOfSpec` | [olap.md](olap.md) | object |
| `PercentileSpec` | [olap.md](olap.md) | object |
| `PieChartSpec` | [charts/pie.md](charts/pie.md) | object |
| `PieMergeConfig` | [charts/pie.md](charts/pie.md) | object |
| `PieOptions` | [charts/pie.md](charts/pie.md) | object |
| `PieTotalConfig` | [charts/pie.md](charts/pie.md) | object |
| `PipelineStage` | [olap.md](olap.md) | variant |
| `PolylineChartOptions` | [charts/line.md](charts/line.md) | object |
| `PolylineChartSpec` | [charts/line.md](charts/line.md) | object |
| `ProgressChartSpec` | [charts/progress.md](charts/progress.md) | object |
| `ProgressDetail` | [charts/progress.md](charts/progress.md) | object |
| `ProgressItem` | [charts/progress.md](charts/progress.md) | object |
| `ProgressMapping` | [charts/progress.md](charts/progress.md) | object |
| `ProgressOptions` | [charts/progress.md](charts/progress.md) | object |
| `ProgressSpec` | [dashboard.md](dashboard.md) | variant |
| `QueryControlBinding` | [dashboard.md](dashboard.md) | object |
| `QueryControlItem` | [dashboard.md](dashboard.md) | object |
| `QueryControlSpec` | [dashboard.md](dashboard.md) | object |
| `QueryControlType` | [dashboard.md](dashboard.md) | picklist |
| `QueryRef` | [dashboard.md](dashboard.md) | object |
| `RankSpec` | [olap.md](olap.md) | object |
| `RankingListOptions` | [charts/ranking-list.md](charts/ranking-list.md) | object |
| `RankingListSpec` | [charts/ranking-list.md](charts/ranking-list.md) | object |
| `ReferenceLine` | [olap.md](olap.md) | object |
| `ScatterChartOptions` | [charts/scatter.md](charts/scatter.md) | object |
| `ScatterChartSpec` | [charts/scatter.md](charts/scatter.md) | object |
| `ScatterOptions` | [charts/scatter.md](charts/scatter.md) | object |
| `SectionSpec` | [dashboard.md](dashboard.md) | object |
| `SeriesType` | [atom-config.md](atom-config.md) | picklist |
| `SortItem` | [olap.md](olap.md) | object |
| `StackMode` | [atom-config.md](atom-config.md) | picklist |
| `StripChartOptions` | [charts/strip.md](charts/strip.md) | object |
| `StripChartSpec` | [charts/strip.md](charts/strip.md) | object |
| `SubIndicatorLayout` | [charts/indicator-card.md](charts/indicator-card.md) | object |
| `TabAlign` | [dashboard.md](dashboard.md) | picklist |
| `TabFontSpec` | [dashboard.md](dashboard.md) | object |
| `TabListMode` | [dashboard.md](dashboard.md) | picklist |
| `TabOptionsSpec` | [dashboard.md](dashboard.md) | object |
| `TabSpec` | [dashboard.md](dashboard.md) | object |
| `TableCellFont` | [dashboard.md](dashboard.md) | object |
| `TableFont` | [dashboard.md](dashboard.md) | object |
| `TableMeasureRef` | [dashboard.md](dashboard.md) | union |
| `TableSpec` | [dashboard.md](dashboard.md) | variant |
| `TableTextVerticalAlign` | [dashboard.md](dashboard.md) | picklist |
| `TextControlConfig` | [dashboard.md](dashboard.md) | object |
| `TextDisplay` | [atom-config.md](atom-config.md) | picklist |
| `TextSpec` | [dashboard.md](dashboard.md) | object |
| `TimeConfigType` | [dashboard.md](dashboard.md) | picklist |
| `TooltipExtra` | [atom-config.md](atom-config.md) | picklist |
| `TooltipSpec` | [atom-config.md](atom-config.md) | object |
| `TooltipTriggerMode` | [atom-config.md](atom-config.md) | picklist |
| `TopNSpec` | [olap.md](olap.md) | object |
| `TrendIconConfig` | [atom-config.md](atom-config.md) | object |
| `TrendIconName` | [atom-config.md](atom-config.md) | picklist |
| `ZeroLineSpec` | [atom-config.md](atom-config.md) | object |

## 总计

schema 170 · 函数 11 · 常量 16

文件顺序：olap.md → dashboard.md → charts/bar.md → charts/line.md → charts/strip.md → charts/combination.md → charts/pie.md → charts/scatter.md → charts/funnel.md → charts/cross-table.md → charts/ranking-list.md → charts/indicator-card.md → charts/progress.md → interaction.md → atom-config.md → misc.md → functions.md → constants.md
