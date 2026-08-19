# 原子配置（跨图表共享）

> encoding 视觉通道、坐标轴 / 图例 / 标签 / 提示框 / 配色 / 数值格式化 / 条件格式 / 分析增强等跨图表复用块。

本文件包含（42）：`Alignment` / `AuxiliaryLineSpec` / `AuxiliaryLineType` / `AxisSpec` / `BaseFieldDef` / `ChartAnalysisSpec` / `ChartBaseSpec` / `ColorSpec` / `CommonOptions` / `ComponentDrillSpec` / `ComponentInteractionSpec` / `ConditionalFormat` / `ConditionalFormatBase` / `ConditionalFormatOperator` / `ConditionalFormatQuery` / `ConditionalFormatRule` / `ConditionalFormatRuleBase` / `DualAxisConfig` / `DualAxisOptions` / `Encoding` / `EncodingMeasureRef` / `FieldRef` / `FontTextStyle` / `LabelContent` / `LabelDisplayMode` / `LabelPosition` / `LabelSpec` / `LegendAlign` / `LegendPosition` / `LegendSpec` / `LineStyle` / `NumberFormat` / `NumberFormatPreset` / `SeriesType` / `StackMode` / `TextDisplay` / `TooltipExtra` / `TooltipSpec` / `TooltipTriggerMode` / `TrendIconConfig` / `TrendIconName` / `ZeroLineSpec`

---
<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## Alignment

> 通用对齐

**枚举**（3 个取值）：`"left"` · `"center"` · `"right"`

## AuxiliaryLineSpec

> 辅助线配置

<!-- DOCS:AUTO START field-table:AuxiliaryLineSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `type` | `"avg" \| "max" \| "min" \| "median" \| "fixed"` | ✅ | 辅助线类型 |
| `value` | `number` |  | 固定值（type=fixed 时必填，缺省则该条辅助线不渲染） |
| `name` | `string` |  | 显示名称：text_display 为 name / both 时必填（缺失则 name 模式标签整体空白）；用户未明确命名时按类型给标准名——计算型用 平均值/最大值/最小值/中位数，type=fixed 用「固定值」，禁止编造文案 |
| `field_id` | `string` |  | 关联的度量字段 id；type=avg/max/min/median 时必填且需与 query.reference_lines[].field 一致，缺省则该条辅助线被丢弃；type=fixed 时禁止填写。双轴图中辅助线轴归属由 field_id 决定——field_id 在 encoding.y2 的度量其辅助线自动归属右轴（数值格式跟随右轴），在 encoding.y 的度量归属左轴。计算型辅助线依赖 query 层统计声明取数，数据源为一次性查询快照（datatable/remote_excel，带 query_ref）时无统计值来源禁止配置（写入也不渲染），仅 type=fixed 可在快照源上使用 |
| `location` | `"y1" \| "y2"` |  | 辅助线关联的轴：y1=度量轴（缺省）, y2=双轴图右轴。计算型辅助线（avg/max/min/median）轴归属由 field_id 决定，location 可选显式声明且须与 field_id 所属轴一致；fixed 型必须用 location 指定轴（缺省 y1） |
| `line_style` | `"solid" \| "dashed" \| "dotted"` |  | 线型，默认 solid |
| `line_color` | `string` |  | 线颜色（#RRGGBB）；用户指定辅助线/参考线颜色时写此字段（缺省用默认色），禁止写入 color.colors（那是图表系列配色板） |
| `text_display` | `"name" \| "value" \| "both"` |  | 文本展示模式，添加辅助线时默认设置为 both；用户要求"显示名称"且未要求隐藏数值时用 both 并同时提供 name（name 模式会隐藏数值文本） |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## AuxiliaryLineType

> 辅助线类型：avg / max / min / median / fixed

**枚举**（5 个取值）：`"avg"` · `"max"` · `"min"` · `"median"` · `"fixed"`

## AxisSpec

> 坐标轴配置

<!-- DOCS:AUTO START field-table:AxisSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `title` | `string` |  | 轴标题 |
| `unit` | `string` |  | 轴单位（拼接为 `标题(单位)`；无 title 时仅展示 `(单位)`） |
| `show` | `boolean` |  | 是否显示轴 |
| `show_grid` | `boolean` |  | 是否显示网格线 |
| `show_label` | `boolean` |  | 是否显示刻度标签 |
| `label_rotate` | `number` |  | 标签旋转角度（0-90，默认自动） |
| `min` | `number` |  | 最小值；不传则自动 |
| `max` | `number` |  | 最大值；不传则自动 |
| `format` | `("auto" \| "raw" \| "integer" \| "decimal-1" \| "decimal-2" \| "percent" \| "percent-1" \| "percent-2" \| "currency-cny" \| "currency-usd" \| string)` |  | 数值格式化（仅数值轴生效） |
| `grid_color` | `string` |  | 网格线颜色（#RRGGBB） |
| `show_line` | `boolean` |  | 是否显示轴线 |
| `show_tick` | `boolean` |  | 是否显示刻度线 |
| `show_title` | `boolean` |  | 是否显示轴标题与单位区域；轴的标题与单位显隐仅由本字段控制（x/y 轴各自设置），组件标题是顶层 title 字段，两者互不相关 |
| `label_style` | `{ font_size, bold, italic, color }` |  | 轴标签文本样式 |
| `zero_line` | `{ enable, line_style, weight, color }` |  | 零基准线（仅数值轴生效） |

<!-- DOCS:AUTO END -->

## BaseFieldDef

> 字段基础定义

<!-- DOCS:AUTO START field-table:BaseFieldDef -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `field` | `string` | ✅ | 字段 id |
| `alias` | `string` |  | 显示别名（图表上实际显示的字段名/度量名）。用户说“字段描述语改为X/显示名改为X/字段重命名为X/改字段名/改度量名”等改显示文本诉求一律写本字段（alias=X）；不存在独立的“描述语”字段 |
| `description` | `string` |  | 字段描述：仅在字段名右侧渲染 icon，悬停展示 tooltip 说明——不是显示名！“描述语更改为X”类改显示文本诉求应写 alias，禁止写本字段 |
| `align` | `"left" \| "center" \| "right"` |  | 列对齐方式（表格类组件使用） |

<!-- DOCS:AUTO END -->

## ChartAnalysisSpec

> 分析增强总配置

<!-- DOCS:AUTO START field-table:ChartAnalysisSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `reference_line` | `{ type, value, name, field_id, location, line_style, line_color, text_display }[]` |  | 辅助线，ranking-list/indicator-card/progress/cross-table 无辅助线渲染能力。新增时需要添加对应的 analyses[].query.reference_lines，固定值（type=fixed 时）不需要添加 reference_lines |

<!-- DOCS:AUTO END -->

## ChartBaseSpec

> 图表通用基类（除 type 和 options 外的所有共享字段）

<!-- DOCS:AUTO START field-table:ChartBaseSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `id` | `string` | ✅ | 组件 ID |
| `title` | `string` |  | 标题（组件名称，联动浮层/组件引用处也用它显示名称）。隐藏标题展示用 card.header_show:false（title 内容保留）；禁止用 null/空串删除 title 实现隐藏——组件失去名称后引用处会回退显示组件 ID |
| `card` | `{ header_show, card_border_width, card_border_color, card_border_radius, card_box_shadow, card_padding, card_background_color, card_background_image, header_font_size, header_font_color, header_font_weight, header_font_style, header_align, header_divider_size, header_divider_color, header_background_color, header_background_image, header_remark, footer_remark, content_margin_top, content_empty_text, content_empty_image, content_empty_link }` |  | 仪表板卡片全局配置 |
| `analysis_ref` | `string` |  | 分析单元引用 |
| `analysis_text` | `string` |  | 完整分析文段 |
| `interaction` | `{ drill }` |  | 交互式分析配置（下钻等），drill 用 ComponentDrillSpec（channel + path，非 mode/on） |
| `encoding` | `{ x, y, y2, color, size, shape, category, theta }` | ✅ | 视觉通道映射（encoding 是唯一数据绑定入口） |
| `axis` | `{ x, y, y2 }` |  | 坐标轴配置（仅直角坐标系图表使用） |
| `legend` | `{ show, position, align, text_style }` |  | 图例 |
| `label` | `{ show, position, content, mode, text_style }` |  | 数据标签 |
| `tooltip` | `{ show, show_mode, extra }` |  | 提示框 |
| `color` | `{ theme, colors }` |  | 配色 |
| `analysis` | `{ reference_line }` |  | 分析增强配置， 辅助线reference_line |

<!-- DOCS:AUTO END -->

## ColorSpec

> 配色配置

<!-- DOCS:AUTO START field-table:ColorSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `theme` | `"warm" \| "cool" \| "neutral" \| "business" \| "pastel"` |  | 色板主题名：warm/cool/neutral/business/pastel；优先级低于 colors，不在内置主题中的使用 colors 进行配置 |
| `colors` | `string[]` |  | 直接给定的色板数组（十六进制颜色字符串），优先级高于 theme；如 ["#3E7BFA", "#10B5B5", ...]；仅承载图表系列/色系配色，辅助线/参考线颜色落 analysis.reference_line[].line_color 不落这里 |

<!-- DOCS:AUTO END -->

## CommonOptions

> 通用形态选项（柱 / 线 / 条形 / 散点 等直角坐标系图表共用）

<!-- DOCS:AUTO START field-table:CommonOptions -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `data_zoom` | `(boolean \| { show, start_index, end_index })` |  | 底部缩略轴 / 数据缩放 |

<!-- DOCS:AUTO END -->

## ComponentDrillSpec

> 组件级 interaction.drill 的实际类型，字段为 channel（编码通道）+ path（字段路径数组）；仅 cube / api 数据源支持，datatable / remote_excel 禁止配置

<!-- DOCS:AUTO START field-table:ComponentDrillSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `channel` | `string` |  | 所属通道（x / color / category / rows / columns），写维度实际所在的 encoding 通道名；交叉表必填，编码类图表可省略（自动推断） |
| `path` | `(string \| { field, alias, description, align })[]` | ✅ | 字段路径（从粗到细），全部来自当前组件 analysis 绑定数据集的维度（含时间粒度变体 report_date(year)→report_date(month)），禁止引用其他数据集字段或编造层级；起点=用户指定开启钻取的字段，其后追加其更细下级字段（至少两级，单级无下钻目标），禁止写上级或全量层级链；每级用数据集字段的 name（data_profile 为准，中文表述须先映射），不存在的字段会使钻取整链失效 |

<!-- DOCS:AUTO END -->

## ComponentInteractionSpec

> 组件级交互式分析配置

<!-- DOCS:AUTO START field-table:ComponentInteractionSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `drill` | `{ channel, path }` |  | 下钻配置（单条路径，仅 cube / api 数据源支持） |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（array），字段表脚本不生成，此处按类型渲染 -->
## ConditionalFormat

> 条件格式配置（含 icon）。按序匹配：同一视觉效果（文字色/背景色/加粗/斜体/图标）取首个命中规则，不同视觉效果可由不同规则分别命中并同时生效（如图标按动态字段对比、文字色按固定阈值）。能力边界元规则：各组件 conditional_format 描述中列出的不支持项即完整限制清单，未列出的对比方式/运算符/效果字段一律视为支持，禁止由个别限制项推断整个条件格式能力不可用

**数组**：`ConditionalFormatRule[]`

<!-- MANUAL: 非 object schema（array），字段表脚本不生成，此处按类型渲染 -->
## ConditionalFormatBase

> 条件格式基础配置（不含 icon 的规则数组）。按序匹配：同一视觉效果（文字色/背景色/加粗/斜体）取首个命中规则，不同视觉效果可由不同规则分别命中并同时生效。能力边界元规则：各组件 conditional_format 描述中列出的不支持项即完整限制清单，未列出的对比方式/运算符/效果字段一律视为支持，禁止由个别限制项推断整个条件格式能力不可用

**数组**：`ConditionalFormatRuleBase[]`

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## ConditionalFormatOperator

> 条件格式操作符（对齐 QBI condition-rule，当前仅数值比较）

**枚举**（7 个取值）：`"eq"` · `"neq"` · `"gt"` · `"lt"` · `"gte"` · `"lte"` · `"between"`

<!-- MANUAL: 非 object schema（variant），字段表脚本不生成，此处按类型渲染 -->
## ConditionalFormatQuery

> 条件格式取数声明：type 与组件规则 compare_with 一一对应；非 pivot 组件需与 query.measures 尾部对比度量条目双写（DSL 自含，仅声明时独立取数链路拿不到对比基准；交叉表 pivot 例外仅声明）。本声明仅负责取数、不产生展示效果：展示规则（operator/compare_with/颜色等）必须写在目标组件度量条目的 conditional_format，禁止把展示字段混入本声明

**判别联合**（按 `type` 区分，2 个成员）：

| type | 成员 schema |
| --- | --- |
| `avg` | `{ type, field }` |
| `field` | `{ type, field, aggregate }` |

`type = avg` 成员字段表：

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `type` | `"avg"` | ✅ | 与均值对比（对应UI层 compare_with='avg'） |
| `field` | `string` | ✅ | 需计算均值的度量，即组件规则所在度量的 field |

`type = field` 成员字段表：

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `type` | `"field"` | ✅ | 与动态字段对比（对应UI层 compare_with='field'） |
| `field` | `string` | ✅ | 对比字段名，同组件规则的 compare_field；写入本声明，并在 query.measures 尾部追加 { field, aggregate } 取数条目（非 pivot 组件，DSL 自含；交叉表仅声明不追加） |
| `aggregate` | `"SUM" \| "AVG" \| "COUNT" \| "COUNT_DISTINCT" \| "MAX" \| "MIN"` |  | 对比字段聚合方式，同组件规则的 compare_aggregate；缺省走 cube 默认 |

## ConditionalFormatRule

> 条件格式单条规则

<!-- DOCS:AUTO START field-table:ConditionalFormatRule -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `operator` | `"eq" \| "neq" \| "gt" \| "lt" \| "gte" \| "lte" \| "between"` | ✅ | 操作符 |
| `compare_with` | `"value" \| "avg" \| "field"` |  | 对比方式：value=固定值对比（缺省）, avg=均值对比（进度条不支持，请勿为其生成）, field=与动态字段对比（需 compare_field）；between 仅支持固定值（avg/field 下拒绝）；添加 avg/field 规则需双写（DSL 自含）：① query.conditional_formats 声明：avg → { type:'avg', field:规则所在度量 }，field → { type:'field', field:compare_field, aggregate:compare_aggregate }；② query.measures 尾部追加对比度量：avg → { field:规则所在度量, aggregate:'AVG' }，field → { field:compare_field, aggregate:compare_aggregate }（尾部条目不参与展示，渲染层自动排除）；仅写声明不追加 measures 时独立取数链路拿不到对比基准，条件格式不生效。交叉表 pivot 例外：均值由后端二次统计，仅写声明禁止追加 measures |
| `compare_field` | `string` |  | 对比字段名（compare_with='field' 时必填）。需在 query.conditional_formats 以 { type:'field', field } 声明，并在 query.measures 尾部追加 { field:对比字段, aggregate:compare_aggregate } 取数条目（非 pivot 组件，DSL 自含；交叉表仅声明不追加） |
| `compare_aggregate` | `"SUM" \| "AVG" \| "COUNT" \| "COUNT_DISTINCT" \| "MAX" \| "MIN"` |  | 对比字段聚合方式（同步写入 query.conditional_formats 声明与 query.measures 尾部取数条目；同名度量时必填，定位唯一数据列） |
| `value` | `(number \| tuple)` |  | 对比值 |
| `text_color` | `string` |  | 文字颜色（#RRGGBB）；用户明确文字颜色（非icon颜色）语义时必须逐条规则显式填写，禁止依赖渲染层缺省表现；用户未指定颜色时省略本字段与其余视觉字段 |
| `background_color` | `string` |  | 背景色（#RRGGBB；仅交叉表/进度条支持，指标看板/排行榜不支持、降级为文字色） |
| `bold` | `boolean` |  | 加粗 |
| `italic` | `boolean` |  | 斜体 |
| `icon` | `("arrow_up" \| "arrow_down" \| "arrow_right" \| { name, color })` |  | 趋势箭头图标：字符串简写 arrow_up/arrow_down/arrow_right；用户指定图标颜色时改用对象 { name, color }，color 为 #RRGGBB 且只作用于图标, 仅同环比等语义或用户明确要求图标时生成，未提及时省略本字段 |

<!-- DOCS:AUTO END -->

## ConditionalFormatRuleBase

> 条件格式基础规则（不含 icon）

<!-- DOCS:AUTO START field-table:ConditionalFormatRuleBase -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `operator` | `"eq" \| "neq" \| "gt" \| "lt" \| "gte" \| "lte" \| "between"` | ✅ | 操作符 |
| `compare_with` | `"value" \| "avg" \| "field"` |  | 对比方式：value=固定值对比（缺省）, avg=均值对比（进度条不支持，请勿为其生成）, field=与动态字段对比（需 compare_field）；between 仅支持固定值（avg/field 下拒绝）；添加 avg/field 规则需双写（DSL 自含）：① query.conditional_formats 声明：avg → { type:'avg', field:规则所在度量 }，field → { type:'field', field:compare_field, aggregate:compare_aggregate }；② query.measures 尾部追加对比度量：avg → { field:规则所在度量, aggregate:'AVG' }，field → { field:compare_field, aggregate:compare_aggregate }（尾部条目不参与展示，渲染层自动排除）；仅写声明不追加 measures 时独立取数链路拿不到对比基准，条件格式不生效。交叉表 pivot 例外：均值由后端二次统计，仅写声明禁止追加 measures |
| `compare_field` | `string` |  | 对比字段名（compare_with='field' 时必填）。需在 query.conditional_formats 以 { type:'field', field } 声明，并在 query.measures 尾部追加 { field:对比字段, aggregate:compare_aggregate } 取数条目（非 pivot 组件，DSL 自含；交叉表仅声明不追加） |
| `compare_aggregate` | `"SUM" \| "AVG" \| "COUNT" \| "COUNT_DISTINCT" \| "MAX" \| "MIN"` |  | 对比字段聚合方式（同步写入 query.conditional_formats 声明与 query.measures 尾部取数条目；同名度量时必填，定位唯一数据列） |
| `value` | `(number \| tuple)` |  | 对比值 |
| `text_color` | `string` |  | 文字颜色（#RRGGBB）；用户明确文字颜色（非icon颜色）语义时必须逐条规则显式填写，禁止依赖渲染层缺省表现；用户未指定颜色时省略本字段与其余视觉字段 |
| `background_color` | `string` |  | 背景色（#RRGGBB；仅交叉表/进度条支持，指标看板/排行榜不支持、降级为文字色） |
| `bold` | `boolean` |  | 加粗 |
| `italic` | `boolean` |  | 斜体 |

<!-- DOCS:AUTO END -->

## DualAxisConfig

> 双轴配置

<!-- DOCS:AUTO START field-table:DualAxisConfig -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `enable` | `boolean` |  | 是否启用双 Y 轴 |
| `sync_mode` | `"sync_all" \| "sync_count"` |  | 刻度同步模式 |

<!-- DOCS:AUTO END -->

## DualAxisOptions

> 双轴选项

<!-- DOCS:AUTO START field-table:DualAxisOptions -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `dual_axis` | `{ enable, sync_mode }` |  | 双 Y 轴配置 |

<!-- DOCS:AUTO END -->

## Encoding

> 视觉通道映射（encoding 是唯一数据绑定入口）

<!-- DOCS:AUTO START field-table:Encoding -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `x` | `((string \| { field, alias, description, align }) \| (string \| { field, alias, description, align })[])` |  | X 轴 / 分类维度：当前图表类型均为单字段，禁止写成多字段数组；添加拆分/系列/分组维度请用 color 通道；漏斗图无分类维度时（0 维多度量）x 应省略，度量全部写入 y，禁止从度量取字段充当 x（度量误放 x 会导致渲染层将原始数值误当类别名显示） |
| `y` | `((string \| { field, alias, description, format, mark }) \| (string \| { field, alias, description, format, mark })[])` |  | Y 轴度量（数组支持多度量） |
| `y2` | `((string \| { field, alias, description, format, mark }) \| (string \| { field, alias, description, format, mark })[])` |  | Y2 轴度量（双轴图右轴：组合图或开启 dual_axis 的线柱图，支持多度量；y、y2 的度量总数无上限，但任一轴放多度量时不得再配置 color） |
| `color` | `(string \| { field, alias, description, align })` |  | 颜色通道（区分系列的维度；饼图为扇区分类维度）；不得与 x/分类轴使用同一字段；y 或 y2 任一轴的度量数 > 1 时禁止配置——该轴多度量已用颜色区分各度量，与 color 系列维度互斥；y、y2 各 1 个度量（含双轴）时可配置 |
| `size` | `(string \| { field, alias, description, format, mark })` |  | 大小通道（散点/气泡） |
| `shape` | `(string \| { field, alias, description, align })` |  | 形状通道（散点/气泡：按维度取值区分数据点形状，不同维值分配不同形状）；统一修改所有数据点形状用 options.point_shape，用户未要求按维度区分形状时勿写本通道 |
| `category` | `(string \| { field, alias, description, align })` |  | 类别通道（散点/气泡：按维度拆分系列/图例） |
| `theta` | `(string \| { field, alias, description, format, mark })` |  | 角度通道（饼图扇区值；缺省时回退取 y 的首个度量） |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（union），字段表脚本不生成，此处按类型渲染 -->
## EncodingMeasureRef

> 度量字段引用（FieldRef 超集，扩展聚合 / 格式化 / 系列视觉属性）

**联合类型**：`string | { field, alias, description, format, mark }`

对象成员字段表：

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `field` | `string` | ✅ | 字段 id |
| `alias` | `string` |  | 显示别名（图表上实际显示的字段名/度量名）。用户说“字段描述语改为X/显示名改为X/字段重命名为X/改字段名/改度量名”等改显示文本诉求一律写本字段（alias=X）；不存在独立的“描述语”字段 |
| `description` | `string` |  | 字段描述(ui上以字段右侧 icon 呈现 , 悬停展开 tooltip 显示描述)。涉及计算字段时，默认标注计算口径 |
| `format` | `("auto" \| "raw" \| "integer" \| "decimal-1" \| "decimal-2" \| "percent" \| "percent-1" \| "percent-2" \| "currency-cny" \| "currency-usd" \| string)` |  | 数值格式化（纯显示格式，不改变数据聚合/计算——与度量本身是否为比例类型无关，用户要求百分比/小数/货币等格式时直接写入）。注意：percent 格式仅把值本身按比例展示（×100 加 %），不做 占总计/同比 换算——当度量为绝对值（金额/数量等）而 用户要求"显示为百分比/占比"时，正确做法是给度量配置 percent_of 占比高级计算（格 式会自动推导 percent-2），禁止对绝对值直接写 percent/percent-2。支持 单位\|除数  语法进行数量级换算（如 #,##0.00万元\|10000），单位用完整表述不缩写为单字（万元/亿元/千元），同时 alias 也应带上单位。alias 含比例语义（环比/同比/比率/占比/百分比/增长率等）时默认 `percent-2`。comparison 度量的 encoding 条目必须显式写入 `format`，缺省用 `percent-2`。 |
| `mark` | `"bar" \| "line" \| "area"` |  | 系列图形类型（组合图：某度量显示为折线） |

<!-- MANUAL: 非 object schema（union），字段表脚本不生成，此处按类型渲染 -->
## FieldRef

> 维度字段引用（简写：字符串=字段 id，或 BaseFieldDef 对象）

**联合类型**：`string | BaseFieldDef`

## FontTextStyle

> 文本字体样式

<!-- DOCS:AUTO START field-table:FontTextStyle -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `font_size` | `number` |  | 字号（px） |
| `bold` | `boolean` |  | 是否加粗 |
| `italic` | `boolean` |  | 是否斜体 |
| `color` | `string` |  | 字体颜色（#RRGGBB） |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## LabelContent

> 标签内容选项

**枚举**（3 个取值）：`"dimension"` · `"measure"` · `"percent"`

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## LabelDisplayMode

> 标签显示模式（重叠处理：auto 避让 / all 错开 / overlap 重叠）

**枚举**（2 个取值）：`"auto"` · `"all"`

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## LabelPosition

**枚举**（17 个取值）：`"auto"` · `"top"` · `"topOutside"` · `"topInner"` · `"centerInner"` · `"bottomInner"` · `"leftInner"` · `"right"` · `"upLine"` · `"belowLine"` · `"areaCenter"` · `"upPoint"` · `"belowPoint"` · `"pointCenter"` · `"outside"` · `"inner"` · `"spider"`

## LabelSpec

> 数据标签配置：仅控制展示层，不改变取数配置（query 度量集）

<!-- DOCS:AUTO START field-table:LabelSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `show` | `boolean` |  | 是否显示数据标签 |
| `position` | `"auto" \| "top" \| "topOutside" \| "topInner" \| "centerInner" \| "bottomInner" \| "leftInner" \| "right" \| "upLine" \| "belowLine" \| "areaCenter" \| "upPoint" \| "belowPoint" \| "pointCenter" \| "outside" \| "inner" \| "spider"` |  | 标签位置（按图表类型分组，跨组不生效）：柱/条形/组合图 top\|topOutside\|topInner\|centerInner\|bottomInner\|leftInner\|right；折线/面积图 upLine\|belowLine\|areaCenter；散点/气泡图 upPoint\|belowPoint\|pointCenter；饼图 outside\|inner\|spider；auto 除饼图外均可用；漏斗图走 options.data_label.position |
| `content` | `"dimension" \| "measure" \| "percent"[]` |  | 标签内容（完整集合、整体替换）：饼图缺省默认显示维度名+占比；在默认或已有内容上增加某项时需写出包含保留项的完整数组，只写新增项会把其余内容从标签中去掉 |
| `mode` | `"auto" \| "all"` |  | 标签显示模式：仅 auto/all 两种，不存在按最值/条件筛选标签的模式 |
| `text_style` | `{ font_size, bold, italic, color }` |  | 标签文本样式 |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## LegendAlign

> 图例对齐（方位语义，取值受 position 约束）

**枚举**（5 个取值）：`"left"` · `"center"` · `"right"` · `"top"` · `"bottom"`

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## LegendPosition

> 图例位置（对应主题 legendOrient）

**枚举**（4 个取值）：`"top"` · `"right"` · `"bottom"` · `"left"`

## LegendSpec

> 图例配置

<!-- DOCS:AUTO START field-table:LegendSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `show` | `boolean` |  | 是否显示图例；用户指令涉及图例相关配置（显示/位置/对齐/文本样式等任一）时必须显式设为 true，否则图例不渲染 |
| `position` | `"top" \| "right" \| "bottom" \| "left"` |  | 图例位置：图例整体停靠在图表的哪一条边（上/右/下/左）。 |
| `align` | `"left" \| "center" \| "right" \| "top" \| "bottom"` |  | 图例对齐方式：图例在 position 停靠边内的对齐方位（先由 position 定停靠边，再由 align 定边内方位）。position 为 top/bottom 时取 left/center/right；position 为 left/right 时取 top/center/bottom。消歧："XX显示/XX展示"修饰的方位词是停靠边 position，其余方位词为边内对齐 align——"图例位置为左，底部显示" → position: bottom + align: left；"图例在底部靠左" → position: bottom + align: left；"图例在左侧垂直靠下" → position: left + align: bottom |
| `text_style` | `{ font_size, bold, italic, color }` |  | 图例文本样式 |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## LineStyle

> 辅助线线型：solid / dashed / dotted

**枚举**（3 个取值）：`"solid"` · `"dashed"` · `"dotted"`

<!-- MANUAL: 非 object schema（union），字段表脚本不生成，此处按类型渲染 -->
## NumberFormat

> 数值格式化（预设简写 NumberFormatPreset 或自定义 DecimalFormat pattern 字符串）。表述按三要素组合解析：数值类别（整数/小数/百分比/货币）+ 小数位数 + 千分位开关——显式给出小数位数时以位数为准（"整数 N 位小数"= 带千分位 N 位小数即 decimal-N，"整数"是数值样式义不代表 0 位小数）；"不显示千分位/无千分位/不带千分位"用无分组 pattern（"0"/"0.0"/"0.00"…）；未提千分位时默认带千分位。预设小数位仅有 -1/-2，其他小数位数不存在对应预设，直接写 pattern（如 3 位小数 "#,##0.000"）——不在预设列表中的"预设样命名"（如 decimal-3）会被当作字面模板渲染出错误文本

**联合类型**：`NumberFormatPreset | string`

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## NumberFormatPreset

> 数值格式化预设名（基础类型 + 精度后缀，kebab-case；如 integer / decimal-1 / percent / currency-cny）。预设小数位仅有 -1/-2（decimal-1/decimal-2、percent-1/percent-2），不存在 decimal-3 等更多位数的预设

**枚举**（10 个取值）：`"auto"` · `"raw"` · `"integer"` · `"decimal-1"` · `"decimal-2"` · `"percent"` · `"percent-1"` · `"percent-2"` · `"currency-cny"` · `"currency-usd"`

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## SeriesType

> 系列图形类型（组合图中混合柱 / 线 / 面）

**枚举**（3 个取值）：`"bar"` · `"line"` · `"area"`

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## StackMode

> 堆叠模式：group 分组 / stack 堆叠 / percent 百分比堆叠（bar / strip / polyline 聚合层挂载）

**枚举**（3 个取值）：`"group"` · `"stack"` · `"percent"`

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## TextDisplay

> 辅助线文本展示模式：name / value / both

**枚举**（3 个取值）：`"name"` · `"value"` · `"both"`

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## TooltipExtra

> Tooltip 额外展示内容（percent=占比，目前仅饼图支持）

**枚举**（1 个取值）：`"percent"`

## TooltipSpec

> Tooltip 配置

<!-- DOCS:AUTO START field-table:TooltipSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `show` | `boolean` |  | 是否启用 tooltip |
| `show_mode` | `"Single" \| "Multiple"` |  | tooltip 展示方式 |
| `extra` | `"percent"[]` |  | tooltip 额外展示字段 |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## TooltipTriggerMode

> tooltip 展示方式（对应 popupConfig.showMode）

**枚举**（2 个取值）：`"Single"` · `"Multiple"`

## TrendIconConfig

<!-- DOCS:AUTO START field-table:TrendIconConfig -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `name` | `"arrow_up" \| "arrow_down" \| "arrow_right"` | ✅ | 图标名称 |
| `color` | `string` |  | 图标颜色（默认使用 #RRGGBB 格式，缺省语义色） |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## TrendIconName

> 趋势箭头图标：arrow_up=上升, arrow_down=下降, arrow_right=持平

**枚举**（3 个取值）：`"arrow_up"` · `"arrow_down"` · `"arrow_right"`

## ZeroLineSpec

> 零基准线配置（数值轴专属）

<!-- DOCS:AUTO START field-table:ZeroLineSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `enable` | `boolean` |  | 是否启用零基准线 |
| `line_style` | `"solid" \| "dashed" \| "dotted"` |  | 零基准线线型 |
| `weight` | `number` |  | 零基准线线宽（px） |
| `color` | `string` |  | 零基准线颜色（#RRGGBB） |

<!-- DOCS:AUTO END -->
