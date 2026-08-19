# 进度条（progress）

> 目标达成进度。范式：progress。

本文件包含（5）：`ProgressChartSpec` / `ProgressDetail` / `ProgressItem` / `ProgressMapping` / `ProgressOptions`

---
## ProgressChartSpec

<!-- DOCS:AUTO START field-table:ProgressChartSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `id` | `string` | ✅ | 组件 ID |
| `title` | `string` |  | 标题（组件名称，联动浮层/组件引用处也用它显示名称）。隐藏标题展示用 card.header_show:false（title 内容保留）；禁止用 null/空串删除 title 实现隐藏——组件失去名称后引用处会回退显示组件 ID |
| `card` | `{ header_show, card_border_width, card_border_color, card_border_radius, card_box_shadow, card_padding, card_background_color, card_background_image, header_font_size, header_font_color, header_font_weight, header_font_style, header_align, header_divider_size, header_divider_color, header_background_color, header_background_image, header_remark, footer_remark, content_margin_top, content_empty_text, content_empty_image, content_empty_link }` |  | 仪表板卡片全局配置 |
| `analysis_ref` | `string` |  | 分析单元引用 |
| `analysis_text` | `string` |  | 完整分析文段 |
| `interaction` | `{ drill }` |  | 交互式分析配置（下钻等），drill 用 ComponentDrillSpec（channel + path，非 mode/on） |
| `type` | `"progress"` | ✅ | 图表类型：进度条 |
| `progress` | `{ items }` | ✅ | 数据映射（current_field + target） |
| `color` | `{ theme, colors }` |  | 配色（复用通用色板） |
| `options` | `{ max_column_limit, border_radius, thickness, detail }` |  | 进度条私有样式配置 |

<!-- DOCS:AUTO END -->

## ProgressDetail

<!-- DOCS:AUTO START field-table:ProgressDetail -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `current_label` | `string` |  | 当前值展示名称（默认"实际"） |
| `target_label` | `string` |  | 目标值展示名称（默认"目标"） |

<!-- DOCS:AUTO END -->

## ProgressItem

<!-- DOCS:AUTO START field-table:ProgressItem -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `current` | `(string \| { field, alias, description, format, mark })` | ✅ | 当前值（度量字段引用，支持 alias/format） |
| `target` | `(number \| (string \| { field, alias, description, format, mark }))` |  | 目标值：固定数值或度量字段引用（动态），仅在用户明确给出目标时写入；未指明目标时缺省，禁止编造数值或把其它度量当作目标 |
| `conditional_format` | `{ operator, compare_with, compare_field, compare_aggregate, value, text_color, background_color, bold, italic }[]` |  | 条件格式：支持按 current 值与固定值（compare_with='value' 缺省，含 between 区间）或同行字段（compare_with='field'）对比，动态改变百分比文本颜色、进度条颜色等；不支持项仅有 compare_with='avg' 与 icon 两项，请勿生成这两项 |

<!-- DOCS:AUTO END -->

## ProgressMapping

<!-- DOCS:AUTO START field-table:ProgressMapping -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `items` | `{ current, target, conditional_format }[]` | ✅ | 系列列表（1-N 个进度条）：结合用户指令映射，多度量转进度条时每个度量各自成一个 item（current），数量与原度量一致 |

<!-- DOCS:AUTO END -->

## ProgressOptions

<!-- DOCS:AUTO START field-table:ProgressOptions -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `max_column_limit` | `number` |  | 每行最大列数（默认 1） |
| `border_radius` | `number` |  | 进度条圆角（px） |
| `thickness` | `number` |  | 进度条厚度（px） |
| `detail` | `(false \| { current_label, target_label })` |  | 当前值/目标值详情配置，false 表示隐藏 |

<!-- DOCS:AUTO END -->
