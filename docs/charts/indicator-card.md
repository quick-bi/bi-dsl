# 指标卡（indicator-card）

> KPI 单值 / 多指标卡。范式：indicator。

本文件包含（10）：`IndicatorCardMapping` / `IndicatorCardMetricRef` / `IndicatorCardOptions` / `IndicatorCardSpec` / `IndicatorFontStyle` / `IndicatorIconConfig` / `IndicatorIconItem` / `IndicatorSplit` / `MainSubPosition` / `SubIndicatorLayout`

---
## IndicatorCardMapping

<!-- DOCS:AUTO START field-table:IndicatorCardMapping -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `metrics` | `(string \| { field, alias, description, format, mark, role, conditional_format })[]` | ✅ | 指标列表（1-20 个度量） |
| `dimension` | `(string \| { field, alias, description, align })` |  | 分组维度（可选，按维度值生成多份指标卡片）；新增/更换分组维度时必须同步在 analyses[].query.dimensions 补该字段（取数结果缺该列时卡片维度标签显示为空） |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（union），字段表脚本不生成，此处按类型渲染 -->
## IndicatorCardMetricRef

> 指标看板专用度量引用（继承 MeasureRef，扩展 role：main 主指标）

**联合类型**：`string | { field, alias, description, format, mark, role, conditional_format }`

对象成员字段表：

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `field` | `string` | ✅ | 字段 id |
| `alias` | `string` |  | 显示别名（图表上实际显示的字段名/度量名）。用户说“字段描述语改为X/显示名改为X/字段重命名为X/改字段名/改度量名”等改显示文本诉求一律写本字段（alias=X）；不存在独立的“描述语”字段 |
| `description` | `string` |  | 字段描述(ui上以字段右侧 icon 呈现 , 悬停展开 tooltip 显示描述)。涉及计算字段时，默认标注计算口径 |
| `format` | `("auto" \| "raw" \| "integer" \| "decimal-1" \| "decimal-2" \| "percent" \| "percent-1" \| "percent-2" \| "currency-cny" \| "currency-usd" \| string)` |  | 数值格式化（纯显示格式，不改变数据聚合/计算——与度量本身是否为比例类型无关，用户要求百分比/小数/货币等格式时直接写入）。注意：percent 格式仅把值本身按比例展示（×100 加 %），不做 占总计/同比 换算——当度量为绝对值（金额/数量等）而 用户要求"显示为百分比/占比"时，正确做法是给度量配置 percent_of 占比高级计算（格 式会自动推导 percent-2），禁止对绝对值直接写 percent/percent-2。支持 单位\|除数  语法进行数量级换算（如 #,##0.00万元\|10000），单位用完整表述不缩写为单字（万元/亿元/千元），同时 alias 也应带上单位。alias 含比例语义（环比/同比/比率/占比/百分比/增长率等）时默认 `percent-2`。comparison 度量的 encoding 条目必须显式写入 `format`，缺省用 `percent-2`。 |
| `mark` | `"bar" \| "line" \| "area"` |  | 系列图形类型（组合图：某度量显示为折线） |
| `role` | `"main"` |  | 指标角色：main=主指标（有且仅有 1 个时启用主辅模式），缺省=并列模式。用户表达主副/主辅/主指标关系时必须给恰好 1 个度量写 role:main（本字段是主辅模式唯一开关，仅设 options.main_sub_position 不生效） |
| `conditional_format` | `{ operator, compare_with, compare_field, compare_aggregate, value, text_color, background_color, bold, italic, icon }[]` |  | 条件格式配置，根据指标值与对比目标（固定值/均值 compare_with=avg/同行字段 compare_with=field）比较结果动态改变文本颜色或图标。指标看板不支持 background_color，请勿生成该字段 |

## IndicatorCardOptions

<!-- DOCS:AUTO START field-table:IndicatorCardOptions -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `num_per_row` | `number` |  | 每行展示个数（默认 4） |
| `align` | `"left" \| "center" \| "right"` |  | 对齐方式：left=左对齐, center=居中, right=右对齐 |
| `main_sub_position` | `"vertical" \| "horizontal"` |  | 主辅助度量布局方向，仅在 indicators.metrics 中恰好 1 个度量 role:main（主辅模式）时生效——配置主副/主辅关系时必须同步设置 role，仅设本字段主辅模式不生效 |
| `name_value_position` | `"row" \| "column"` |  | 指标名称与数值排列：row=同行, column=上下 |
| `gap` | `number` |  | 指标卡间距（px） |
| `indicator_split` | `{ type, split_color, background_color, background_radius }` |  | 指标块装饰配置（分隔线/背景填充/圆角），作用于指标块整体，无主/副指标角色粒度 |
| `font_style` | `{ dimension_font, name_font, value_font, sub_name_font, sub_value_font }` |  | 指标字体样式 |
| `icon_config` | `{ show, position, align, style, gap, size, items }` |  | 修饰图标/图标配置；修改位置、对齐、样式等展示配置无需改动 items，未明确指定图标内容时省略 items |
| `sub_indicator_layout` | `{ layout_direction, name_value_position, show_split_line }` |  | 辅助度量布局配置 |

<!-- DOCS:AUTO END -->

## IndicatorCardSpec

<!-- DOCS:AUTO START field-table:IndicatorCardSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `id` | `string` | ✅ | 组件 ID |
| `title` | `string` |  | 标题（组件名称，联动浮层/组件引用处也用它显示名称）。隐藏标题展示用 card.header_show:false（title 内容保留）；禁止用 null/空串删除 title 实现隐藏——组件失去名称后引用处会回退显示组件 ID |
| `card` | `{ header_show, card_border_width, card_border_color, card_border_radius, card_box_shadow, card_padding, card_background_color, card_background_image, header_font_size, header_font_color, header_font_weight, header_font_style, header_align, header_divider_size, header_divider_color, header_background_color, header_background_image, header_remark, footer_remark, content_margin_top, content_empty_text, content_empty_image, content_empty_link }` |  | 仪表板卡片全局配置 |
| `analysis_ref` | `string` |  | 分析单元引用 |
| `analysis_text` | `string` |  | 完整分析文段 |
| `interaction` | `{ drill }` |  | 交互式分析配置（下钻等），drill 用 ComponentDrillSpec（channel + path，非 mode/on） |
| `type` | `"indicator-card"` | ✅ | 图表类型：指标看板 |
| `indicators` | `{ metrics, dimension }` | ✅ | 指标数据映射 |
| `options` | `{ num_per_row, align, main_sub_position, name_value_position, gap, indicator_split, font_style, icon_config, sub_indicator_layout }` |  | 指标看板选项配置 |

<!-- DOCS:AUTO END -->

## IndicatorFontStyle

<!-- DOCS:AUTO START field-table:IndicatorFontStyle -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `dimension_font` | `{ font_size, bold, italic, color }` |  | 维度名文字样式 |
| `name_font` | `{ font_size, bold, italic, color }` |  | 指标名文字样式 |
| `value_font` | `{ font_size, bold, italic, color }` |  | 指标值文字样式 |
| `sub_name_font` | `{ font_size, bold, italic, color }` |  | 辅助度量名文字样式 |
| `sub_value_font` | `{ font_size, bold, italic, color }` |  | 辅助度量值文字样式 |

<!-- DOCS:AUTO END -->

## IndicatorIconConfig

<!-- DOCS:AUTO START field-table:IndicatorIconConfig -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `show` | `boolean` |  | 是否显示图标 |
| `position` | `"left" \| "top" \| "right"` |  | 图标位置：left=左侧, top=上方, right=右侧 |
| `align` | `"top" \| "center" \| "bottom"` |  | 图标垂直对齐方式：top=顶对齐, center=居中, bottom=底对齐 |
| `style` | `"transparent" \| "filled"` |  | 图标样式：transparent=透明背景, filled=填充背景 |
| `gap` | `number` |  | 图标与文字的间距（px） |
| `size` | `number` |  | 图标大小（px） |
| `items` | `{ emoji, src, name, color, bg_color, bg_radius }[]` |  | 各指标图标内容数组（按 indicators.metrics 顺序匹配，越界循环复用）；未明确指定图标内容时省略 |

<!-- DOCS:AUTO END -->

## IndicatorIconItem

<!-- DOCS:AUTO START field-table:IndicatorIconItem -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `emoji` | `string` |  | emoji 或字符标识 |
| `src` | `string` |  | 图标资源 URL |
| `name` | `"icon-jiankong-outlined" \| "icon-zhichichenggong-outlined" \| "icon-money-outlined" \| "icon-shop-outlined" \| "icon-wallet-outlined" \| "icon-order-outlined" \| "icon-rankings-outlined" \| "icon-datapanel-outlined" \| "icon-clock-outlined" \| "icon-shopping-outlined"` |  | 内置图标名（枚举限定，见可选项） |
| `color` | `string` |  | 图标前景色 |
| `bg_color` | `string` |  | 图标背景色（圆/胶囊） |
| `bg_radius` | `number` |  | 图标背景圆角（px）；不填默认圆形 |

<!-- DOCS:AUTO END -->

## IndicatorSplit

<!-- DOCS:AUTO START field-table:IndicatorSplit -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `type` | `"none" \| "split" \| "background"` |  | 指标卡分隔模式：none=无分隔, split=显示分隔线, background=独立卡片背景 |
| `split_color` | `string` |  | 分隔线颜色，仅 type=split 时生效（#RRGGBB） |
| `background_color` | `(string \| string[])` |  | 卡片背景色，仅 type=background 时生效，字符串或字符串数组（按 metrics 序逐卡分配装饰色）。仅作指标块整体装饰，不支持按主/副指标角色单独着色，禁止用数组顺序模拟角色化背景，“仅给副指标配置背景色”类诉求超出能力边界 |
| `background_radius` | `number` |  | 卡片圆角 px，仅 type=background 时生效 |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## MainSubPosition

> 主指标/辅助度量布局方向：vertical / horizontal

**枚举**（2 个取值）：`"vertical"` · `"horizontal"`

## SubIndicatorLayout

<!-- DOCS:AUTO START field-table:SubIndicatorLayout -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `layout_direction` | `"vertical" \| "horizontal"` |  | 辅助度量排列方向：vertical=独占一行, horizontal=水平排成一行 |
| `name_value_position` | `"row" \| "column"` |  | 辅助度量内名称与数值排列方向：row=同行, column=上下 |
| `show_split_line` | `boolean` |  | 是否显示辅助度量间分割线，颜色取 indicator_split.split_color |

<!-- DOCS:AUTO END -->
