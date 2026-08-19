# 组合图（combination）

> 柱 + 线混合、双轴。范式：encoding。

本文件包含（2）：`CombinationChartOptions` / `CombinationChartSpec`

---
## CombinationChartOptions

<!-- DOCS:AUTO START field-table:CombinationChartOptions -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `data_zoom` | `(boolean \| { show, start_index, end_index })` |  | 底部缩略轴 / 数据缩放 |
| `column_width_ratio` | `number` |  | 柱体宽度占比（0-1） |
| `bar_radius` | `number` |  | 柱体圆角（px） |
| `smooth` | `boolean` |  | 是否平滑曲线（线图默认 true 即平滑；用户要求“直线/直线段连接/非平滑曲线”时必须显式写 false，仅不写 smooth 不会变成直线） |
| `connect_nulls` | `boolean` |  | 是否连接空值：仅控制空值点连线不断开，不改变空值数据本身。“空值置为 0/空值填补为 X”类诉求无对应字段，必须拆开披露：连线不断开写本字段，置值部分判 unsupported 说明不支持空值替换，禁止只写本字段声称完成全部诉求 |
| `show_symbol` | `boolean` |  | 是否显示标记点 |
| `symbol_type` | `"circle" \| "hollow_circle" \| "rect" \| "diamond" \| "triangle" \| "none"` |  | 标记点形状：circle=实心圆, hollow_circle=空心圆, rect=小方块, diamond=菱形, triangle=三角形, none=无标记 |
| `line_width` | `number` |  | 线条宽度（px） |
| `line_type` | `"solid" \| "dashed" \| "dotted"` |  | 线型（线条花样）：solid=实线, dashed=虚线, dotted=点线。与“直线/平滑”是正交维度——“直线段连接（非平滑曲线）”诉求用 smooth=false 表达，与本字段无关 |
| `area_opacity` | `number` |  | 面积填充透明度（0-1，仅面积图生效） |
| `area_gradient` | `boolean` |  | 面积是否开启渐变填充 |
| `dual_axis` | `{ enable, sync_mode }` |  | 双 Y 轴配置 |

<!-- DOCS:AUTO END -->

## CombinationChartSpec

<!-- DOCS:AUTO START field-table:CombinationChartSpec -->

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
| `type` | `"combination"` | ✅ | 图表类型：组合图（线柱混合） |
| `options` | `{ data_zoom, column_width_ratio, bar_radius, smooth, connect_nulls, show_symbol, symbol_type, line_width, line_type, area_opacity, area_gradient, dual_axis }` |  | 组合图选项配置 |

<!-- DOCS:AUTO END -->
