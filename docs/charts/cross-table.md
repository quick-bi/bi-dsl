# 交叉表（cross-table）

> 多维交叉明细。范式：layout。

本文件包含（8）：`CrossTableDisplayMode` / `CrossTableInteractionSpec` / `CrossTableLayout` / `CrossTableOptions` / `CrossTableSpec` / `CrossTableThemeColors` / `CrossTableTotalDisplay` / `FrozenConfig`

---
<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## CrossTableDisplayMode

> 交叉表展示模式：tile 平铺 / tree 树形

**枚举**（2 个取值）：`"tile"` · `"tree"`

## CrossTableInteractionSpec

> 交叉表交互式分析配置

<!-- DOCS:AUTO START field-table:CrossTableInteractionSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `drill` | `{ channel, path }[]` |  | 交叉表下钻配置（数组，每个行维度各自一条路径，仅 cube / api 数据源支持） |

<!-- DOCS:AUTO END -->

## CrossTableLayout

<!-- DOCS:AUTO START field-table:CrossTableLayout -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `rows` | `(string \| { field, alias, description, align })[]` | ✅ | 行维度（分组/左侧行头，按先后决定层级） |
| `columns` | `(string \| { field, alias, description, align })[]` | ✅ | 列维度（顶部展开维度） |
| `measures` | `(string \| { field, alias, description, format, mark, conditional_format })[]` | ✅ | 度量字段，仅展示属性，支持 conditional_format 条件格式。**禁止写入 comparison 等高级计算字段**——交叉表/排行榜的 measures 不支持同环比类高级计算，此类诉求应判 unsupported 并在回复中披露（建议改用折线/柱图等支持高级计算的图表）；违规写入会被剥离，剥离后该度量与原度量同名同值显示（假成功）。单列文字色/加粗/斜体等列级样式应写该列 measures[].conditional_format（恒真规则），字号仅全局（正文字体字段），禁止用全局字体字段实现单列诉求 |

<!-- DOCS:AUTO END -->

## CrossTableOptions

<!-- DOCS:AUTO START field-table:CrossTableOptions -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `display_mode` | `"tile" \| "tree"` |  | 展示模式：tile=平铺, tree=树形（按行维度层级嵌套可展开） |
| `measure_position` | `"column" \| "row"` |  | 度量位置：column=度量在列区（默认）, row=度量在行区（行头右侧按度量拆行）；display_mode=tree 时忽略。注意：当用户意图为「度量放在行」时必须设置为 row，且度量字段禁止写入 layout.rows，应始终放在 layout.measures 中。用户意图为「行列互换/行列转置」时必须成对修改：交换 layout.rows↔layout.columns 且翻转本字段（column↔row） |
| `frozen` | `{ enable, mode, fix_column_num }` |  | 冻结列配置 |
| `merge_cell` | `boolean` |  | 是否合并单元格 |
| `auto_line_break` | `boolean` |  | 是否自动换行 |
| `header_auto_line_break` | `boolean` |  | 表头是否自动换行 |
| `show_index` | `boolean` |  | 是否显示序号列 |
| `index_name` | `string` |  | 序号列列头名称 |
| `total` | `{ total_alias, sub_total_alias }` |  | 汇总展示配置（仅别名，显隐/位置等取数语义在 OLAP 取数 DSL 的 total） |
| `page_size` | `number` |  | 服务端分页每页行数；layout.rows 无维度、数据源为 Excel/数据表（source_type 为 remote_excel/datatable，取数链路不支持分页，不支持设置分页）；不传代表不分页 |
| `column_width_mode` | `"auto" \| "equal"` |  | 列宽模式：auto=自动, equal=等宽 |
| `table_theme` | `{ show_zebra, zebra_color }` |  | 表格主题色配置，仅控制隔行交替色 |
| `table_font` | `{ body, header, row_header }` |  | 表格字体配置，分别控制表头和正文的字体样式 |

<!-- DOCS:AUTO END -->

## CrossTableSpec

<!-- DOCS:AUTO START field-table:CrossTableSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `id` | `string` | ✅ | 组件 ID |
| `title` | `string` |  | 标题（组件名称，联动浮层/组件引用处也用它显示名称）。隐藏标题展示用 card.header_show:false（title 内容保留）；禁止用 null/空串删除 title 实现隐藏——组件失去名称后引用处会回退显示组件 ID |
| `card` | `{ header_show, card_border_width, card_border_color, card_border_radius, card_box_shadow, card_padding, card_background_color, card_background_image, header_font_size, header_font_color, header_font_weight, header_font_style, header_align, header_divider_size, header_divider_color, header_background_color, header_background_image, header_remark, footer_remark, content_margin_top, content_empty_text, content_empty_image, content_empty_link }` |  | 仪表板卡片全局配置 |
| `analysis_ref` | `string` |  | 分析单元引用 |
| `analysis_text` | `string` |  | 完整分析文段 |
| `interaction` | `{ drill }` |  | 交叉表交互式分析配置（覆盖基类，支持多组下钻），drill 用 ComponentDrillSpec（channel + path，非 mode/on） |
| `type` | `"cross-table"` | ✅ | 图表类型：交叉表 |
| `layout` | `{ rows, columns, measures }` | ✅ | 数据布局（行维度、列维度、度量） |
| `options` | `{ display_mode, measure_position, frozen, merge_cell, auto_line_break, header_auto_line_break, show_index, index_name, total, page_size, column_width_mode, table_theme, table_font }` |  | 交叉表选项配置 |

<!-- DOCS:AUTO END -->

## CrossTableThemeColors

<!-- DOCS:AUTO START field-table:CrossTableThemeColors -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `show_zebra` | `boolean` |  | 是否显示隔行交替色 |
| `zebra_color` | `string` |  | 隔行颜色（#RRGGBB） |

<!-- DOCS:AUTO END -->

## CrossTableTotalDisplay

<!-- DOCS:AUTO START field-table:CrossTableTotalDisplay -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `total_alias` | `string` |  | 总计别名 |
| `sub_total_alias` | `string` |  | 小计别名 |

<!-- DOCS:AUTO END -->

## FrozenConfig

<!-- DOCS:AUTO START field-table:FrozenConfig -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `enable` | `boolean` |  | 是否开启冻结 |
| `mode` | `"auto_head" \| "fix_column"` |  | 冻结模式：auto_head=自动冻结表头, fix_column=固定列数 |
| `fix_column_num` | `number` |  | 固定列数（fix_column 模式） |

<!-- DOCS:AUTO END -->
