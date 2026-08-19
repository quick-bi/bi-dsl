# 排行榜（ranking-list）

> 带数据条的排名列表。范式：layout。

本文件包含（3）：`DataBarStyle` / `RankingListOptions` / `RankingListSpec`

---
## DataBarStyle

<!-- DOCS:AUTO START field-table:DataBarStyle -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `positive_color` | `string` |  | 正值填充色（#RRGGBB） |
| `negative_color` | `string` |  | 负值填充色（#RRGGBB） |
| `gradient` | `boolean` |  | 是否开启渐变（默认 false） |
| `border_radius` | `number` |  | 圆角（px，默认 2） |

<!-- DOCS:AUTO END -->

## RankingListOptions

<!-- DOCS:AUTO START field-table:RankingListOptions -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `order` | `"desc" \| "asc"` |  | 排序方向：desc=降序, asc=升序 |
| `limit` | `number` |  | 展示条数（不传则全部展示） |
| `show_rank` | `boolean` |  | 是否显示排名序号列（默认 true） |
| `data_bar` | `{ positive_color, negative_color, gradient, border_radius }` |  | 数据条样式，控制填充色、渐变、圆角等 |
| `header_font` | `{ font_size, bold, italic, color }` |  | 表头字体（全局）：作用于整行表头——含序号列头与全部度量列头，无法只隐藏某一列的列头。排行榜无列标题显隐字段，“隐藏列标题/隐藏某列列名”类诉求判 unsupported 披露，禁止用透明色/极小字号模拟隐藏（会连序号列头一起隐藏） |
| `body_font` | `{ font_size, bold, italic, color }` |  | 正文字体（全局）：作用于全表格体——含维度列与全部度量列，无法只改某一列。单列文字色/加粗等列级样式应写该列 layout.measures[].conditional_format（恒真规则）；字号无列级字段（仅全局），单列字号诉求应披露会作用于全部列 |

<!-- DOCS:AUTO END -->

## RankingListSpec

<!-- DOCS:AUTO START field-table:RankingListSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `id` | `string` | ✅ | 组件 ID |
| `title` | `string` |  | 标题（组件名称，联动浮层/组件引用处也用它显示名称）。隐藏标题展示用 card.header_show:false（title 内容保留）；禁止用 null/空串删除 title 实现隐藏——组件失去名称后引用处会回退显示组件 ID |
| `card` | `{ header_show, card_border_width, card_border_color, card_border_radius, card_box_shadow, card_padding, card_background_color, card_background_image, header_font_size, header_font_color, header_font_weight, header_font_style, header_align, header_divider_size, header_divider_color, header_background_color, header_background_image, header_remark, footer_remark, content_margin_top, content_empty_text, content_empty_image, content_empty_link }` |  | 仪表板卡片全局配置 |
| `analysis_ref` | `string` |  | 分析单元引用 |
| `analysis_text` | `string` |  | 完整分析文段 |
| `interaction` | `{ drill }` |  | 交互式分析配置（下钻等），drill 用 ComponentDrillSpec（channel + path，非 mode/on） |
| `type` | `"ranking-list"` | ✅ | 图表类型：排行榜 |
| `layout` | `{ rows, columns, measures }` | ✅ | 数据布局（复用交叉表 layout：rows=维度, columns=空, measures=度量，measures 支持 conditional_format 条件格式） |
| `color` | `{ theme, colors }` |  | 配色：colors[0]→正值填充色，colors[1]→负值填充色；options.data_bar.positive_color/negative_color 优先级更高 |
| `options` | `{ order, limit, show_rank, data_bar, header_font, body_font }` |  | 排行榜选项配置 |

<!-- DOCS:AUTO END -->
