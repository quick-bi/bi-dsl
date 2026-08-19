# 饼图（pie）

> 占比构成；用 theta + color，不用 x + y。范式：encoding。

本文件包含（4）：`PieChartSpec` / `PieMergeConfig` / `PieOptions` / `PieTotalConfig`

---
## PieChartSpec

<!-- DOCS:AUTO START field-table:PieChartSpec -->

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
| `type` | `"pie"` | ✅ | 图表类型：饼图 |
| `options` | `{ radius, inner_radius, merge, total }` |  | 饼图选项配置 |

<!-- DOCS:AUTO END -->

## PieMergeConfig

<!-- DOCS:AUTO START field-table:PieMergeConfig -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `enable` | `boolean` |  | 是否开启合并 |
| `count` | `number` |  | 保留扇区数量，超过部分合并为"其他" |
| `name` | `string` |  | 合并项显示名称 |

<!-- DOCS:AUTO END -->

## PieOptions

<!-- DOCS:AUTO START field-table:PieOptions -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `radius` | `number` |  | 外半径占比（0-1） |
| `inner_radius` | `number` |  | 内半径占比（0-1，>0 即环图） |
| `merge` | `{ enable, count, name }` |  | 合并小扇区配置，不传则不合并 |
| `total` | `{ show, name, name_style, value_style }` |  | 总计配置：环图在中心显示，普通饼图在图表上方显示 |

<!-- DOCS:AUTO END -->

## PieTotalConfig

<!-- DOCS:AUTO START field-table:PieTotalConfig -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `show` | `boolean` |  | 是否显示总计 |
| `name` | `string` |  | 自定义总计名称 |
| `name_style` | `{ font_size, bold, italic, color }` |  | 总计名称文字样式 |
| `value_style` | `{ font_size, bold, italic, color }` |  | 总计数值文字样式 |

<!-- DOCS:AUTO END -->
