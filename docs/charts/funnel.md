# 漏斗图（funnel）

> 转化流程。范式：encoding。

本文件包含（6）：`FunnelCategoryLabel` / `FunnelChartSpec` / `FunnelDataLabel` / `FunnelOptions` / `FunnelRatioLabel` / `FunnelTotalRatioLabel`

---
## FunnelCategoryLabel

<!-- DOCS:AUTO START field-table:FunnelCategoryLabel -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `show` | `boolean` |  | 是否显示 |
| `text_style` | `{ font_size, bold, italic, color }` |  | 文字样式 |
| `position` | `"start" \| "end"` |  | 类别标签位置：start=图形左侧, end=图形右侧 |
| `show_label_line` | `boolean` |  | 是否显示引导线 |

<!-- DOCS:AUTO END -->

## FunnelChartSpec

<!-- DOCS:AUTO START field-table:FunnelChartSpec -->

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
| `type` | `"funnel"` | ✅ | 图表类型：漏斗图 |
| `options` | `{ funnel_mode, funnel_type, edge_display, bar_width_ratio, color_mode, footer_shape, category_label, data_label, ratio_label, total_ratio_label }` |  | 漏斗图选项配置 |

<!-- DOCS:AUTO END -->

## FunnelDataLabel

<!-- DOCS:AUTO START field-table:FunnelDataLabel -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `show` | `boolean` |  | 是否显示 |
| `text_style` | `{ font_size, bold, italic, color }` |  | 文字样式 |
| `position` | `"start" \| "end" \| "inside" \| "edge-top" \| "edge-bottom" \| "category-right" \| "category-bottom" \| "outer" \| "inner"` |  | 数据标签位置：start=左侧, end=右侧, inside=内部, edge-top=上边缘, edge-bottom=下边缘, category-right=类别标签右侧, category-bottom=类别标签下方, outer=柱体外侧, inner=柱体内部 |

<!-- DOCS:AUTO END -->

## FunnelOptions

<!-- DOCS:AUTO START field-table:FunnelOptions -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `funnel_mode` | `"regular" \| "transform"` |  | 漏斗模式：regular=传统漏斗, transform=矩形转化分析 |
| `funnel_type` | `"edge" \| "trap" \| "perfect_trap"` |  | 漏斗类型（仅 regular 模式生效）：edge=标准梯形, trap=梯形, perfect_trap=完美梯形 |
| `edge_display` | `"real" \| "smooth"` |  | 边缘显示模式（完美梯形模式不支持）：real=真实尺寸, smooth=平滑 |
| `bar_width_ratio` | `number` |  | 柱宽占比（0-1，仅 transform 模式生效） |
| `color_mode` | `"category" \| "level_gradient" \| "single"` |  | 颜色模式：category=分类色, level_gradient=渐变色, single=单色 |
| `footer_shape` | `"flat" \| "sharp"` |  | 漏斗底部形状（仅 trap 类型生效）：flat=平底, sharp=尖底 |
| `category_label` | `{ show, text_style, position, show_label_line }` |  | 类别标签（漏斗层名） |
| `data_label` | `{ show, text_style, position }` |  | 数据标签（度量值） |
| `ratio_label` | `{ show, text_style, digits }` |  | 层间转化率标签 |
| `total_ratio_label` | `{ show, name, name_style, value_style, digits }` |  | 总转化率标签 |

<!-- DOCS:AUTO END -->

## FunnelRatioLabel

<!-- DOCS:AUTO START field-table:FunnelRatioLabel -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `show` | `boolean` |  | 是否显示 |
| `text_style` | `{ font_size, bold, italic, color }` |  | 文字样式 |
| `digits` | `number` |  | 小数位数 |

<!-- DOCS:AUTO END -->

## FunnelTotalRatioLabel

<!-- DOCS:AUTO START field-table:FunnelTotalRatioLabel -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `show` | `boolean` |  | 是否显示 |
| `name` | `string` |  | 标签名称（默认"总转化率"） |
| `name_style` | `{ font_size, bold, italic, color }` |  | 名称文字样式 |
| `value_style` | `{ font_size, bold, italic, color }` |  | 数值文字样式 |
| `digits` | `number` |  | 小数位数 |

<!-- DOCS:AUTO END -->
