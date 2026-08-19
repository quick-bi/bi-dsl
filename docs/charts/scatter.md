# 散点图（scatter）

> 相关性 / 分布。范式：encoding。

本文件包含（3）：`ScatterChartOptions` / `ScatterChartSpec` / `ScatterOptions`

---
## ScatterChartOptions

<!-- DOCS:AUTO START field-table:ScatterChartOptions -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `point_opacity` | `number` |  | 数据点透明度（0-1） |
| `size_range` | `tuple` |  | 气泡大小范围 [min, max]（px，仅气泡图生效） |
| `point_size` | `number` |  | 固定数据点大小（px，无 size 度量时生效） |
| `point_shape` | `"circle" \| "square" \| "diamond" \| "triangle" \| "pentagon" \| "hexagon" \| "star"` |  | 数据点形状：circle=圆形, square=方形, diamond=菱形, triangle=三角形, pentagon=五边形（非五角星）, hexagon=六边形, star=星形（即五角星）；统一修改所有数据点形状用本字段，按维度取值区分形状用 encoding.shape 通道，两者互不相关 |
| `show_border` | `boolean` |  | 是否显示描边 |

<!-- DOCS:AUTO END -->

## ScatterChartSpec

<!-- DOCS:AUTO START field-table:ScatterChartSpec -->

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
| `type` | `"scatter"` | ✅ | 图表类型：散点图/气泡图 |
| `options` | `{ point_opacity, size_range, point_size, point_shape, show_border }` |  | 散点图选项配置 |

<!-- DOCS:AUTO END -->

## ScatterOptions

<!-- DOCS:AUTO START field-table:ScatterOptions -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `point_opacity` | `number` |  | 数据点透明度（0-1） |
| `size_range` | `tuple` |  | 气泡大小范围 [min, max]（px，仅气泡图生效） |
| `point_size` | `number` |  | 固定数据点大小（px，无 size 度量时生效） |
| `point_shape` | `"circle" \| "square" \| "diamond" \| "triangle" \| "pentagon" \| "hexagon" \| "star"` |  | 数据点形状：circle=圆形, square=方形, diamond=菱形, triangle=三角形, pentagon=五边形（非五角星）, hexagon=六边形, star=星形（即五角星）；统一修改所有数据点形状用本字段，按维度取值区分形状用 encoding.shape 通道，两者互不相关 |
| `show_border` | `boolean` |  | 是否显示描边 |

<!-- DOCS:AUTO END -->
