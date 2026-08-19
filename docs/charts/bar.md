# 柱图（bar）

> 分类对比；多系列可 group / stack / percent。范式：encoding。

本文件包含（3）：`BarChartOptions` / `BarChartSpec` / `BarOptions`

---
## BarChartOptions

<!-- DOCS:AUTO START field-table:BarChartOptions -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `data_zoom` | `(boolean \| { show, start_index, end_index })` |  | 底部缩略轴 / 数据缩放 |
| `column_width_ratio` | `number` |  | 柱体宽度占比（0-1） |
| `bar_radius` | `number` |  | 柱体圆角（px） |
| `dual_axis` | `{ enable, sync_mode }` |  | 双 Y 轴配置 |
| `stack_mode` | `"group" \| "stack" \| "percent"` |  | 堆叠模式（柱图子类型）：group=分组对比, stack=堆叠, percent=百分比堆叠 |

<!-- DOCS:AUTO END -->

## BarChartSpec

<!-- DOCS:AUTO START field-table:BarChartSpec -->

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
| `type` | `"bar"` | ✅ | 图表类型：柱图 |
| `options` | `{ data_zoom, column_width_ratio, bar_radius, dual_axis, stack_mode }` |  | 柱图选项配置 |

<!-- DOCS:AUTO END -->

## BarOptions

<!-- DOCS:AUTO START field-table:BarOptions -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `column_width_ratio` | `number` |  | 柱体宽度占比（0-1） |
| `bar_radius` | `number` |  | 柱体圆角（px） |

<!-- DOCS:AUTO END -->
