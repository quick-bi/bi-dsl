# OLAP 取数意图

> 描述"要什么数"的查询契约：维度 / 度量 / 过滤 / 排序 / 高级计算（同环比 / 累计 / 移动 / 排名 / 占比 / TopN 等）。

本文件包含（22）：`ComparisonSpec` / `CumulativeSpec` / `DateCumulativeSpec` / `DerivedField` / `DimensionBaseRef` / `DimensionGroupSpec` / `DimensionRef` / `FilterItem` / `MeasureRef` / `MovingSpec` / `OlapAggregate` / `OlapDslSpec` / `OlapFilterOperator` / `OlapGranularity` / `OlapTotalSpec` / `PercentOfSpec` / `PercentileSpec` / `PipelineStage` / `RankSpec` / `ReferenceLine` / `SortItem` / `TopNSpec`

---
## ComparisonSpec

<!-- DOCS:AUTO START field-table:ComparisonSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `kind` | `"yoy" \| "yring" \| "moy" \| "mom" \| "qoq" \| "wow" \| "wring" \| "dod" \| "custom"` | ✅ | 同环比类型，必须与用户术语精确匹配：月环比=mom、季环比=qoq、日环比=dod、周环比=wring、年环比=yring、周同比=wow、月同比=moy、年同比=yoy、custom=自定义（需通过 period_type 指定对比周期）。kind 还须与图表时间维度粒度匹配（对齐快捷对比规则）：年粒度仅支持 yring（年环比）；月粒度支持 mom/yoy；季粒度支持 qoq/yoy；周粒度支持 wring/yoy；日粒度支持 dod/wow/moy/yoy |
| `value_type` | `"last_value" \| "increase_value" \| "increase_ratio"` | ✅ | 输出值类型：last_value=对比期原始值, increase_value=增长差值, increase_ratio=增长率，默认值为 increase_ratio |
| `period_value` | `number` |  | 对比步长（默认 1，即上一期；设为 2 表示和 2 个周期前对比） |
| `period_type` | `"year" \| "quarter" \| "month" \| "week" \| "day"` |  | 自定义对比周期（仅 kind=custom 时必填） |
| `date_field` | `string` | ✅ | 日期粒度后缀的日期字段名(name)，格式 `字段名(粒度)`，如 `report_date(month)` |

<!-- DOCS:AUTO END -->

## CumulativeSpec

<!-- DOCS:AUTO START field-table:CumulativeSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `scope` | `"total" \| "by_group"` |  | 累计范围：total=全部行，by_group=组内 |

<!-- DOCS:AUTO END -->

## DateCumulativeSpec

<!-- DOCS:AUTO START field-table:DateCumulativeSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `kind` | `"week" \| "month" \| "quarter" \| "year" \| "hyear"` | ✅ | 日期累计类型：week/month/quarter/year/hyear |
| `date_field` | `string` |  | 日期字段名（省略时自动取 dimensions 中第一个带 granularity 的时间维度） |

<!-- DOCS:AUTO END -->

## DerivedField

<!-- DOCS:AUTO START field-table:DerivedField -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `field` | `string` | ✅ | 字段标识（唯一 ID） |
| `formula` | `string` | ✅ | 计算表达式（UDF 语法） |
| `data_type` | `"number" \| "string" \| "datetime"` | ✅ | 字段数据类型 |
| `exp_type` | `"measure" \| "dimension"` | ✅ | 字段归属：度量或维度 |
| `alias` | `string` |  | 显示别名 |
| `aggregated` | `boolean` |  | 表达式是否已包含聚合函数（默认 false） |

<!-- DOCS:AUTO END -->

## DimensionBaseRef

<!-- DOCS:AUTO START field-table:DimensionBaseRef -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `field` | `string` | ✅ | 字段名（语义层名称，与数据集字段一致） |
| `granularity` | `"year" \| "year-quarter" \| "quarter" \| "year-month" \| "month" \| "year-week" \| "week" \| "year-month-day" \| "day" \| "hour" \| "minute" \| "second"` |  | 时间粒度（仅时间维度） |
| `alias` | `string` |  | 显示别名 |
| `description` | `string` |  | 字段描述(ui上以字段右侧 icon 呈现 , 悬停展开 tooltip 显示描述) |

<!-- DOCS:AUTO END -->

## DimensionGroupSpec

> 维度组：一组互斥候选维度，用户通过切换器替换当前生效维度。外层维度的 field/granularity 即默认档（首次渲染的生效维度），candidates 是包含默认档在内的全部可选项。维度组之间不要求相关：既可以是同一字段的不同时间粒度（如订单日期 年/月/日），也可以是彼此不相关的不同字段（如 地区/省份、配送方式/客户类型/商品类别）。仅 cube / api 数据源支持；datatable（物理表）/ remote_excel（远程 Excel）取数无法替换查询维度，禁止配置维度组

<!-- DOCS:AUTO START field-table:DimensionGroupSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `candidates` | `{ field, granularity, alias, description }[]` | ✅ | 候选维度列表（有序 = 切换器展示顺序），互斥单选。须包含默认维度 |

<!-- DOCS:AUTO END -->

## DimensionRef

<!-- DOCS:AUTO START field-table:DimensionRef -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `field` | `string` | ✅ | 字段名（语义层名称，与数据集字段一致） |
| `granularity` | `"year" \| "year-quarter" \| "quarter" \| "year-month" \| "month" \| "year-week" \| "week" \| "year-month-day" \| "day" \| "hour" \| "minute" \| "second"` |  | 时间粒度（仅时间维度） |
| `alias` | `string` |  | 显示别名 |
| `description` | `string` |  | 字段描述(ui上以字段右侧 icon 呈现 , 悬停展开 tooltip 显示描述) |
| `group` | `{ candidates }` |  | 维度组（可选）：可被用户切换的候选维度集合 |

<!-- DOCS:AUTO END -->

## FilterItem

<!-- DOCS:AUTO START field-table:FilterItem -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `field` | `string` | ✅ | 过滤字段名 |
| `aggregate` | `"SUM" \| "AVG" \| "COUNT" \| "COUNT_DISTINCT" \| "MAX" \| "MIN"` |  | 聚合函数（填写时表示对聚合结果过滤） |
| `granularity` | `"year" \| "year-quarter" \| "quarter" \| "year-month" \| "month" \| "year-week" \| "week" \| "year-month-day" \| "day" \| "hour" \| "minute" \| "second"` |  | 时间粒度（时间维度过滤时使用） |
| `operator` | `"eq" \| "ne" \| "gt" \| "gte" \| "lt" \| "lte" \| "in" \| "not_in" \| "between" \| "contains" \| "not_contains" \| "starts_with" \| "ends_with" \| "null" \| "not_null" \| "last" \| "relative"` |  | 操作符 |
| `value` | `unknown` |  | 过滤值 |
| `timing` | `"before_agg" \| "after_agg"` |  | 过滤时机：before_agg（默认）= 聚合前 WHERE，after_agg = 聚合后 HAVING |

<!-- DOCS:AUTO END -->

## MeasureRef

<!-- DOCS:AUTO START field-table:MeasureRef -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `field` | `string` | ✅ | 字段名（语义层名称，与数据集字段一致） |
| `aggregate` | `"SUM" \| "AVG" \| "COUNT" \| "COUNT_DISTINCT" \| "MAX" \| "MIN"` |  | 聚合函数（省略时使用数据集默认聚合） |
| `alias` | `string` |  | 显示别名（图例/标签可见文本）。携带 comparison 的度量，alias 必须为「原度量 alias + 计算类型语义后缀」（如"订单金额年环比""Order Amount YoY"），后缀语言与报表语言环境一致；禁止使用内部编码后缀（_yring/_yoy/_mom） |
| `comparison` | `{ kind, value_type, period_value, period_type, date_field }` |  | 同环比。在已有度量上追加 comparison 会将该度量的取数结果替换为对比值（如增长率），原始聚合值不再返回；需同时展示原始值与对比值时，必须新增独立度量条目（不同 alias）承载对比值，禁止在已有度量上就地追加 comparison |
| `cumulative` | `{ scope }` |  | 累计（表计算累计） |
| `date_cumulative` | `{ kind, date_field }` |  | 日期累计 |
| `moving` | `{ fn, prev, next }` |  | 移动计算 |
| `rank` | `{ scope, order }` |  | 排名 |
| `percentile` | `{ scope, order }` |  | 百分位 |
| `top_n` | `{ n, order, reference_dimension }` |  | TopN |
| `percent_of` | `{ scope, accumulate }` |  | 占比 |
| `pipeline` | `variant[]` |  | 高级计算 pipeline（有序阶段化嵌套） |

<!-- DOCS:AUTO END -->

## MovingSpec

<!-- DOCS:AUTO START field-table:MovingSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `fn` | `"avg" \| "sum" \| "max" \| "min"` | ✅ | 计算函数 |
| `prev` | `number` |  | 向前看几期（默认 1） |
| `next` | `number` |  | 向后看几期（默认 1） |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## OlapAggregate

> 聚合函数（沿用 QuickBI 原生大写形式）

**枚举**（6 个取值）：`"SUM"` · `"AVG"` · `"COUNT"` · `"COUNT_DISTINCT"` · `"MAX"` · `"MIN"`

## OlapDslSpec

> OLAP 取数 DSL

<!-- DOCS:AUTO START field-table:OlapDslSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `dataset_ref` | `string` |  | 数据集引用（通过 title 关联，运行时解析为 cube id） |
| `query_kind` | `"aggregated" \| "detail"` |  | 查询种类：aggregated（默认）= 聚合查询，detail = 明细查询 |
| `dimensions` | `{ field, granularity, alias, description, group }[]` | ✅ | 维度字段列表 |
| `measures` | `{ field, aggregate, alias, comparison, cumulative, date_cumulative, moving, rank, percentile, top_n, percent_of, pipeline }[]` | ✅ | 度量字段列表 |
| `filters` | `{ field, aggregate, granularity, operator, value, timing }[]` |  | 过滤条件禁止落到filters，应该生成查询控件承载 |
| `sort` | `{ by, dir, type }[]` |  | 排序规则（独立块，支持多字段排序） |
| `limit` | `number` |  | 结果行数限制 |
| `reference_lines` | `{ type, field }[]` |  | 辅助线列表（后端计算统计值：均值/最大/最小/中位数；source_type 为 remote_excel / datatable 时不支持动态统计值） |
| `conditional_formats` | `variant<type>: avg \| field[]` |  | 条件格式取数声明（均不允许修改 measures），仅取数不承载展示：展示规则必须同步写在目标组件度量条目的 conditional_format；remote_excel/datatable 不支持动态统计值，请勿声明 |
| `derived_fields` | `{ field, formula, data_type, exp_type, alias, aggregated }[]` |  | 计算字段定义（派生字段，运行时转为 cubeShadow 参数） |
| `total` | `{ show_total, show_sub_total, total_logic, total_position }` |  | 总计 / 小计取数配置（仅交叉表生效；source_type 为 remote_excel / datatable 时不支持） |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## OlapFilterOperator

> 过滤操作符

**枚举**（17 个取值）：`"eq"` · `"ne"` · `"gt"` · `"gte"` · `"lt"` · `"lte"` · `"in"` · `"not_in"` · `"between"` · `"contains"` · `"not_contains"` · `"starts_with"` · `"ends_with"` · `"null"` · `"not_null"` · `"last"` · `"relative"`

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## OlapGranularity

> 时间粒度（单层如 year/month，或层级如 year-month）

**枚举**（12 个取值）：`"year"` · `"year-quarter"` · `"quarter"` · `"year-month"` · `"month"` · `"year-week"` · `"week"` · `"year-month-day"` · `"day"` · `"hour"` · `"minute"` · `"second"`

## OlapTotalSpec

<!-- DOCS:AUTO START field-table:OlapTotalSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `show_total` | `boolean` |  | 是否显示总计行 |
| `show_sub_total` | `boolean` |  | 是否显示小计行（仅当行维度或列维度数量大于 1 时支持，否则不支持配置） |
| `total_logic` | `"auto" \| "sum" \| "avg"` |  | 汇总逻辑：auto 后端自动 / sum 求和 / avg 平均 |
| `total_position` | `"top" \| "bottom"` |  | 总计 / 小计行位置（top / bottom，缺省 bottom） |

<!-- DOCS:AUTO END -->

## PercentOfSpec

<!-- DOCS:AUTO START field-table:PercentOfSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `scope` | `"total" \| "by_group"` | ✅ | 占比范围：total=占总计，by_group=占组内 |
| `accumulate` | `boolean` |  | 是否累计占比（默认 false） |

<!-- DOCS:AUTO END -->

## PercentileSpec

<!-- DOCS:AUTO START field-table:PercentileSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `scope` | `"total" \| "by_group"` |  | 百分位范围：total=全局（默认），by_group=组内 |
| `order` | `"asc" \| "desc"` |  | 百分位方向：asc（默认）/desc |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（variant），字段表脚本不生成，此处按类型渲染 -->
## PipelineStage

> OLAP 后处理流水线阶段（按 stage 判别：同环比 / 累计 / 移动 / 排名 / 占比 / TopN 等）

**判别联合**（按 `stage` 区分，8 个成员）：

| stage | 成员 schema |
| --- | --- |
| `comparison` | `{ stage, kind, value_type, period_value, period_type, date_field }` |
| `cumulative` | `{ stage, scope }` |
| `date_cumulative` | `{ stage, kind, date_field }` |
| `moving` | `{ stage, fn, prev, next }` |
| `rank` | `{ stage, dense, scope, group_by, order }` |
| `top_n` | `{ stage, n, order }` |
| `percent_of` | `{ stage, scope, accumulate }` |
| `percentile` | `{ stage, scope, order }` |

`stage = comparison` 成员字段表：

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `stage` | `"comparison"` | ✅ | 阶段类型 |
| `kind` | `"yoy" \| "yring" \| "moy" \| "mom" \| "qoq" \| "wow" \| "wring" \| "dod" \| "custom"` | ✅ | 同环比类型 |
| `value_type` | `"last_value" \| "increase_value" \| "increase_ratio"` | ✅ | 输出值类型 |
| `period_value` | `number` |  | 对比步长（默认 1） |
| `period_type` | `"year" \| "quarter" \| "month" \| "week" \| "day"` |  | 自定义对比周期（仅 kind=custom 时必填） |
| `date_field` | `string` | ✅ | 日期字段名 |

`stage = cumulative` 成员字段表：

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `stage` | `"cumulative"` | ✅ | 阶段类型 |
| `scope` | `"total" \| "by_group"` |  | 累计范围：total=全部行（默认），by_group=组内 |

`stage = date_cumulative` 成员字段表：

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `stage` | `"date_cumulative"` | ✅ | 阶段类型 |
| `kind` | `"week" \| "month" \| "quarter" \| "year" \| "hyear"` | ✅ | 日期累计类型：week/month/quarter/year/hyear |
| `date_field` | `string` |  | 日期字段名（省略时自动取第一个时间维度） |

`stage = moving` 成员字段表：

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `stage` | `"moving"` | ✅ | 阶段类型 |
| `fn` | `"avg" \| "sum" \| "max" \| "min"` | ✅ | 计算函数 |
| `prev` | `number` |  | 向前看几期（默认 1） |
| `next` | `number` |  | 向后看几期（默认 1） |

`stage = rank` 成员字段表：

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `stage` | `"rank"` | ✅ | 阶段类型 |
| `dense` | `boolean` |  | 是否密集排名 |
| `scope` | `"total" \| "by_group"` |  | 排名范围 |
| `group_by` | `string` |  | 分组字段 |
| `order` | `"asc" \| "desc"` |  | 排名方向 |

`stage = top_n` 成员字段表：

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `stage` | `"top_n"` | ✅ | 阶段类型 |
| `n` | `number` | ✅ | 取前 N 条 |
| `order` | `"asc" \| "desc"` |  | 排序方向（默认 desc） |

`stage = percent_of` 成员字段表：

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `stage` | `"percent_of"` | ✅ | 阶段类型 |
| `scope` | `"total" \| "by_group"` | ✅ | 占比范围：total=占总计，by_group=占组内 |
| `accumulate` | `boolean` |  | 是否累计占比（默认 false） |

`stage = percentile` 成员字段表：

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `stage` | `"percentile"` | ✅ | 阶段类型 |
| `scope` | `"total" \| "by_group"` |  | 百分位范围：total=全局（默认），by_group=组内 |
| `order` | `"asc" \| "desc"` |  | 百分位方向：asc（默认）/desc |

## RankSpec

<!-- DOCS:AUTO START field-table:RankSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `scope` | `"total" \| "by_group"` |  | 排名范围 |
| `order` | `"asc" \| "desc"` |  | 排名方向（默认 desc） |

<!-- DOCS:AUTO END -->

## ReferenceLine

<!-- DOCS:AUTO START field-table:ReferenceLine -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `type` | `"avg" \| "max" \| "min" \| "median"` | ✅ | 辅助线类型 |
| `field` | `string` | ✅ | 度量字段名 |

<!-- DOCS:AUTO END -->

## SortItem

<!-- DOCS:AUTO START field-table:SortItem -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `by` | `string` | ✅ | 排序字段名 |
| `dir` | `"asc" \| "desc" \| "group_asc" \| "group_desc"` | ✅ | 排序方向：asc/desc=全局排序，group_asc/group_desc=组内排序 |
| `type` | `"value" \| "total"` |  | 排序类型：value=按字段值（默认），total=按堆积总和 |

<!-- DOCS:AUTO END -->

## TopNSpec

<!-- DOCS:AUTO START field-table:TopNSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `n` | `number` | ✅ | 取前 N 条 |
| `order` | `"asc" \| "desc"` |  | 排序方向（默认 desc，即取最大 N 条） |
| `reference_dimension` | `string` |  | 按固定维度排名（可选） |

<!-- DOCS:AUTO END -->
