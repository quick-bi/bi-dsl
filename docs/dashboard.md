# 看板骨架（Dashboard）

> DashboardSpec 顶层结构与其组成：UI / 布局 / 卡片 / 页头页脚 / 主题 / 组件 / 分析单元 / 查询控件。

本文件包含（48）：`AnalysisRef` / `AnalysisSpec` / `ChartSpec` / `CommonSpec` / `ContainerSpec` / `DashboardCardSpec` / `DashboardComponentBaseSpec` / `DashboardComponentSpec` / `DashboardFooterSpec` / `DashboardHeaderSpec` / `DashboardInteractionSpec` / `DashboardLayoutItemSpec` / `DashboardLayoutSpec` / `DashboardSpec` / `DashboardThemeSpec` / `DashboardUiChartSpec` / `DashboardUiDashboardSpec` / `DashboardUiSpec` / `DataSourceRef` / `DateControlConfig` / `DurationType` / `EnumControlConfig` / `FetchSourceType` / `IndicatorSpec` / `InsightSpec` / `NumberControlConfig` / `NumberOperator` / `PanelSpec` / `ProgressSpec` / `QueryControlBinding` / `QueryControlItem` / `QueryControlSpec` / `QueryControlType` / `QueryRef` / `SectionSpec` / `TabAlign` / `TabFontSpec` / `TabListMode` / `TabOptionsSpec` / `TabSpec` / `TableCellFont` / `TableFont` / `TableMeasureRef` / `TableSpec` / `TableTextVerticalAlign` / `TextControlConfig` / `TextSpec` / `TimeConfigType`

---
<!-- MANUAL: 非 object schema（union），字段表脚本不生成，此处按类型渲染 -->
## AnalysisRef

> 分析引用：字符串按 id 引用 analyses[]，或内联一个 AnalysisSpec 对象

**联合类型**：`string | AnalysisSpec`

## AnalysisSpec

> Headless 分析单元，仅描述取什么数，与渲染解耦

<!-- DOCS:AUTO START field-table:AnalysisSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `id` | `string` | ✅ | 分析单元 ID, 语义化命名, 例如 q_store_gmv_trend |
| `title` | `string` |  | 分析意图标题，用于 AI 上下文与调试 |
| `description` | `string` |  | 分析意图描述，用于 AI 上下文与调试 |
| `source_type` | `"cube" \| "datatable" \| "remote_excel" \| "api"` |  | 取数链路类型：决定走 OLAP / QueryAgent / API 哪条取数策略 |
| `query_ref` | `{ message_id }` |  | QueryAgent 取数引用，source_type 为 datatable/remote_excel 时使用 |
| `query` | `{ dataset_ref, query_kind, dimensions, measures, filters, sort, limit, reference_lines, conditional_formats, derived_fields, total }` | ✅ | OLAP 查询主体，v2 DSL：维度/度量分离，统一过滤，独立排序 |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（variant），字段表脚本不生成，此处按类型渲染 -->
## ChartSpec

> encoding 范式图表判别联合（按 type：bar / line / strip / combination / pie / scatter / funnel）

**判别联合**（按 `type` 区分，8 个成员）：

| type | 成员 schema |
| --- | --- |
| `bar` | `BarChartSpec` |
| `line` | `LineChartSpec` |
| `polyline` | `PolylineChartSpec` |
| `strip` | `StripChartSpec` |
| `combination` | `CombinationChartSpec` |
| `pie` | `PieChartSpec` |
| `scatter` | `ScatterChartSpec` |
| `funnel` | `FunnelChartSpec` |

## CommonSpec

> 仪表板 AI DSL 顶层公共字段

<!-- DOCS:AUTO START field-table:CommonSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `id` | `string` |  | 仪表板唯一 ID（语义化命名，例如 db_weekly_review） |
| `title` | `string` |  | 仪表板标题 |
| `description` | `string` |  | 仪表板描述，主要面向开发/AI 上下文；当 ui.header 启用且未设 header.subtitle 时，也会作为 banner 副标题展示，避免重复书写 |
| `intent` | `string` |  | 仪表板分析意图（描述本仪表板的生成逻辑 / 分析目标） |
| `version` | `string` |  | schema version 读 package.json 生成 |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（variant），字段表脚本不生成，此处按类型渲染 -->
## ContainerSpec

> 容器与控件组件判别联合（按 type：tab / panel / query_control 等）

**判别联合**（按 `type` 区分，6 个成员）：

| type | 成员 schema |
| --- | --- |
| `tab` | `TabSpec` |
| `panel` | `PanelSpec` |
| `section` | `SectionSpec` |
| `text` | `TextSpec` |
| `insight` | `InsightSpec` |
| `query_control` | `QueryControlSpec` |

## DashboardCardSpec

<!-- DOCS:AUTO START field-table:DashboardCardSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `header_show` | `boolean` |  | 是否显示卡片标题区域，默认 true；指标看板（indicator-card）默认 false，显式配置后按配置展示 |
| `card_border_width` | `number` |  | 卡片边框宽度 px，默认 0, 代表无边框 |
| `card_border_color` | `string` |  | 卡片边框颜色 |
| `card_border_radius` | `number` |  | 卡片边框圆角 px |
| `card_box_shadow` | `(boolean \| string)` |  | 卡片边框阴影：true=轻阴影，false=无阴影，字符串=CSS box-shadow 值 |
| `card_padding` | `number[]` |  | 卡片内边距 [top, right, bottom, left] px |
| `card_background_color` | `string` |  | 卡片背景颜色 |
| `card_background_image` | `string` |  | 卡片背景图片 |
| `header_font_size` | `number` |  | 卡片标题字体大小 |
| `header_font_color` | `string` |  | 卡片标题字体颜色 |
| `header_font_weight` | `"normal" \| "bold"` |  | 卡片标题字体粗细 |
| `header_font_style` | `"normal" \| "italic"` |  | 卡片标题字体样式 |
| `header_align` | `"left" \| "center"` |  | 卡片标题对齐方式 |
| `header_divider_size` | `number` |  | 卡片分隔线, 0 代表无分隔线 |
| `header_divider_color` | `string` |  | 卡片分隔线颜色 |
| `header_background_color` | `string` |  | 卡片标题背景颜色 |
| `header_background_image` | `string` |  | 卡片标题背景图片 |
| `header_remark` | `string` |  | 备注内容，渲染为紧跟卡片标题的信息图标，hover 弹出提示 |
| `footer_remark` | `string` |  | 尾注内容，渲染在卡片内容区下方的小字行 |
| `content_margin_top` | `number` |  | 内容区与顶部的间距 |
| `content_empty_text` | `string` |  | 空数据提示文本 |
| `content_empty_image` | `string` |  | 空数据提示图片 |
| `content_empty_link` | `string` |  | 空数据提示跳转链接 |

<!-- DOCS:AUTO END -->

## DashboardComponentBaseSpec

> 组件基础字段（所有范式共享）

<!-- DOCS:AUTO START field-table:DashboardComponentBaseSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `id` | `string` | ✅ | 组件 ID |
| `title` | `string` |  | 标题（组件名称，联动浮层/组件引用处也用它显示名称）。隐藏标题展示用 card.header_show:false（title 内容保留）；禁止用 null/空串删除 title 实现隐藏——组件失去名称后引用处会回退显示组件 ID |
| `card` | `{ header_show, card_border_width, card_border_color, card_border_radius, card_box_shadow, card_padding, card_background_color, card_background_image, header_font_size, header_font_color, header_font_weight, header_font_style, header_align, header_divider_size, header_divider_color, header_background_color, header_background_image, header_remark, footer_remark, content_margin_top, content_empty_text, content_empty_image, content_empty_link }` |  | 仪表板卡片全局配置 |
| `analysis_ref` | `string` |  | 分析单元引用 |
| `analysis_text` | `string` |  | 完整分析文段 |
| `interaction` | `{ drill }` |  | 交互式分析配置（下钻等），drill 用 ComponentDrillSpec（channel + path，非 mode/on） |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（variant），字段表脚本不生成，此处按类型渲染 -->
## DashboardComponentSpec

> 所有看板组件的顶层判别联合（按 type 推导可用数据映射：encoding→encoding / layout→layout / indicator→indicators）

**判别联合**（按 `type` 区分，18 个成员）：

| type | 成员 schema |
| --- | --- |
| `bar` | `BarChartSpec` |
| `line` | `LineChartSpec` |
| `polyline` | `PolylineChartSpec` |
| `strip` | `StripChartSpec` |
| `combination` | `CombinationChartSpec` |
| `pie` | `PieChartSpec` |
| `scatter` | `ScatterChartSpec` |
| `funnel` | `FunnelChartSpec` |
| `cross-table` | `CrossTableSpec` |
| `ranking-list` | `RankingListSpec` |
| `indicator-card` | `IndicatorCardSpec` |
| `progress` | `ProgressChartSpec` |
| `tab` | `TabSpec` |
| `panel` | `PanelSpec` |
| `section` | `SectionSpec` |
| `text` | `TextSpec` |
| `insight` | `InsightSpec` |
| `query_control` | `QueryControlSpec` |

## DashboardFooterSpec

> 仪表板底部 footer 配置

<!-- DOCS:AUTO START field-table:DashboardFooterSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `show` | `boolean` |  | 是否显示，默认 true |
| `text` | `string` |  | 页脚正文（纯文本，渲染层以 white-space: pre-wrap 保留换行） |
| `subtitle` | `string` |  | footer 副文案（小字辅助信息）；未设置时自动拼“数据来源：xxx”兜底 |
| `background_image` | `string` |  | footer 装饰图 URL（叠加在 background_color 之上，CSS object-fit: cover） |
| `background_color` | `string` |  | 背景色，可为纯色 #RRGGBB 或渐变 |
| `height` | `number` |  | footer 高度 px，默认 60 |
| `text_color` | `string` |  | 正文文字颜色；缺省跟随主题文字 token |
| `subtitle_color` | `string` |  | 副文案文字颜色；缺省跟随主题文字 token |

<!-- DOCS:AUTO END -->

## DashboardHeaderSpec

> 仪表板顶部 banner 配置

<!-- DOCS:AUTO START field-table:DashboardHeaderSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `show` | `boolean` |  | 是否显示，默认 true；传 false 时整个顶部区域隐藏 |
| `subtitle` | `string` |  | banner 副标题（纯文本，渲染层以 white-space: pre-wrap 保留换行） |
| `background_image` | `string` |  | 顶部装饰图 URL（叠加在 background_color 之上，CSS object-fit: cover） |
| `background_color` | `string` |  | 背景色，可为纯色 #RRGGBB 或渐变 |
| `max_height` | `number` |  | banner 最大高度 px，限制内容撑高时的上界；不设时高度由内容撑开 |
| `text_color` | `string` |  | 标题文字颜色；缺省跟随主题文字 token |
| `subtitle_color` | `string` |  | 副标题文字颜色；缺省跟随主题文字 token |
| `page_background` | `string` |  | 整页背景（覆盖 dashboard 外层容器，与 banner 的 background_color 解耦）。设置了 theme.template 时渲染层会展开顶部装饰背景且优先级高于本字段，纯色会被盖住不可见——需要纯色整页背景时不要设置 theme.template |
| `title_font_size` | `number` |  | 标题字体大小 px；未设置时回退到主题预设，再回退到默认 30 |
| `title_font_weight` | `("normal" \| "bold" \| number)` |  | 标题字体粗细：normal/bold/数值(100-900)；未设置时回退到主题预设，再回退到默认 500 |
| `title_font_style` | `"normal" \| "italic"` |  | 标题字体样式：normal/italic，默认 normal |

<!-- DOCS:AUTO END -->

## DashboardInteractionSpec

> 看板级交互配置，包含联动设置

<!-- DOCS:AUTO START field-table:DashboardInteractionSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `auto_linkage` | `boolean` |  | 同数据集自动联动开关，开启后相同 dataset_ref 的组件自动建立联动关系 |
| `auto_linkage_excludes` | `string[]` |  | 退出自动联动的组件 ID 列表，仅在 auto_linkage=true 时生效 |
| `linkages` | `{ id, source, targets, trigger, mode, field_map }[]` |  | 精确联动规则列表，用于非同源、指定触发方式等高级场景 |

<!-- DOCS:AUTO END -->

## DashboardLayoutItemSpec

> 单个布局项

<!-- DOCS:AUTO START field-table:DashboardLayoutItemSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `component_id` | `string` | ✅ | 关联的 UI 组件 ID（指向 ui.components[].id） |
| `parent_id` | `string` |  | 父级组件 ID（指向同数组内另一项的 component_id，最多两级） |
| `x` | `number` | ✅ | 水平起始位置（网格列下标） |
| `y` | `number` | ✅ | 垂直起始位置（网格行下标） |
| `w` | `number` | ✅ | 所占列数 |
| `h` | `number` | ✅ | 所占行数 |
| `auto_height` | `boolean` |  | 是否启用内容自适应高度（text / section 等内容驱动型组件与表格 cross-table / common-table 支持） |

<!-- DOCS:AUTO END -->

## DashboardLayoutSpec

> 仪表板布局配置

<!-- DOCS:AUTO START field-table:DashboardLayoutSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `type` | `"grid"` |  | 布局类型，当前仅支持 grid |
| `grid_column` | `4 \| 6 \| 8 \| 10 \| 12 \| 14 \| 16 \| 18 \| 20 \| 21 \| 24` |  | 网格列数，默认 24 |
| `grid_row_height` | `number` |  | 单行高度 px，默认 24 |
| `grid_row_gap` | `number` |  | 行间距（垂直）px，默认 12 |
| `grid_column_gap` | `number` |  | 列间距（水平）px，默认 12 |
| `page_width` | `(number \| "auto")` |  | 页宽宽度，默认 auto（撑满容器） |
| `page_padding` | `number[]` |  | 页边距 [top, right, bottom, left] px，缺省为四向 12 |
| `items` | `...` |  | 布局项数组（禁止写成以 id 为键的对象 map）：每项通过 component_id 关联到 ui.components[].id，通过 parent_id 表达层级关系；新增组件时向本数组追加条目 |

<!-- DOCS:AUTO END -->

## DashboardSpec

<!-- DOCS:AUTO START field-table:DashboardSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `id` | `string` |  | 仪表板唯一 ID（语义化命名，例如 db_weekly_review） |
| `title` | `string` |  | 仪表板标题 |
| `description` | `string` |  | 仪表板描述，主要面向开发/AI 上下文；当 ui.header 启用且未设 header.subtitle 时，也会作为 banner 副标题展示，避免重复书写 |
| `intent` | `string` |  | 仪表板分析意图（描述本仪表板的生成逻辑 / 分析目标） |
| `version` | `string` |  | schema version 读 package.json 生成 |
| `data_sources` | `{ kind, id, title }[]` |  | 顶层数据源池（可选），多个分析单元可共享 |
| `analyses` | `{ id, title, description, source_type, query_ref, query }[]` |  | 分析单元列表（headless 取数），供 UI 组件通过 analysis_ref 引用 |
| `ui` | `variant` |  | 可视化展示子节点（可辨识联合：dashboard 多组件仪表板 / chart 单图表） |

<!-- DOCS:AUTO END -->

## DashboardThemeSpec

> 仪表板主题配置

<!-- DOCS:AUTO START field-table:DashboardThemeSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `template` | `"gradient" \| "minimal"` |  | 主题模板预设标识，由渲染层展开为完整视觉属性；minimal=极简白板（靛紫），gradient=渐变背景图；两者均带顶部装饰背景且优先级高于 header.page_background 纯色，需要纯色整页背景时不要设置 theme.template |
| `palette` | `"blue" \| "orange" \| "green" \| "purple"` |  | 色板标识，渲染层按 (template, palette) 选择色值数组和背景图；仅 gradient 注册了多色板，其余模板使用自身默认色板（可省略本字段） |

<!-- DOCS:AUTO END -->

## DashboardUiChartSpec

<!-- DOCS:AUTO START field-table:DashboardUiChartSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `kind` | `"chart"` | ✅ | _（待补 v.description）_ |
| `layout` | `{ type, grid_column, grid_row_height, grid_row_gap, grid_column_gap, page_width, page_padding, items }` |  | 布局配置（chart 模式下忽略栅格，仅做 schema 兼容） |
| `components` | `variant<type>: bar \| line \| polyline \| strip \| combination \| pie \| scatter \| funnel \| cross-table \| ranking-list \| indicator-card \| progress \| tab \| panel \| section \| text \| insight \| query_control[]` |  | 渲染组件列表；渲染时不走栅格，组件直接铺满容器，建议只给一个组件 |

<!-- DOCS:AUTO END -->

## DashboardUiDashboardSpec

<!-- DOCS:AUTO START field-table:DashboardUiDashboardSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `kind` | `"dashboard"` | ✅ | _（待补 v.description）_ |
| `header` | `{ show, subtitle, background_image, background_color, max_height, text_color, subtitle_color, page_background, title_font_size, title_font_weight, title_font_style }` |  | 页面级顶部 banner（渐变 / 实色背景 + 装饰图 + H1 + 副标题） |
| `footer` | `{ show, text, subtitle, background_image, background_color, height, text_color, subtitle_color }` |  | 页面级底部 footer（版权 / 备注 / 装饰条） |
| `page_nav` | `{ enabled, list_mode, placement }` |  | 页面级导航（吸顶 scroll-spy 导航条，自动锚定到顶层 section） |
| `theme` | `{ template, palette }` |  | 全局主题配置（卡片样式 / 调色板 / 页面背景 / 字体 / 语义色） |
| `layout` | `{ type, grid_column, grid_row_height, grid_row_gap, grid_column_gap, page_width, page_padding, items }` | ✅ | 栅格布局配置 |
| `components` | `variant<type>: bar \| line \| polyline \| strip \| combination \| pie \| scatter \| funnel \| cross-table \| ranking-list \| indicator-card \| progress \| tab \| panel \| section \| text \| insight \| query_control[]` | ✅ | 渲染组件列表（按 id 与 layout.items.component_id 对应，含 query_control 类型） |
| `interaction` | `{ auto_linkage, auto_linkage_excludes, linkages }` |  | 看板级交互配置（联动 / 下钻回退按钮等） |
| `card` | `{ header_show, card_border_width, card_border_color, card_border_radius, card_box_shadow, card_padding, card_background_color, card_background_image, header_font_size, header_font_color, header_font_weight, header_font_style, header_align, header_divider_size, header_divider_color, header_background_color, header_background_image, header_remark, footer_remark, content_margin_top, content_empty_text, content_empty_image, content_empty_link }` |  | 仪表板卡片全局配置 |
| `layout_render` | `string` |  | 自定义布局渲染器（UMD 模块格式的 JavaScript 代码字符串） |
| `card_render` | `string` |  | 自定义卡片渲染器（UMD 模块格式的 JavaScript 代码字符串） |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（variant），字段表脚本不生成，此处按类型渲染 -->
## DashboardUiSpec

> 看板 UI 顶层结构（按类型判别的联合）

**判别联合**（按 `kind` 区分，2 个成员）：

| kind | 成员 schema |
| --- | --- |
| `dashboard` | `DashboardUiDashboardSpec` |
| `chart` | `DashboardUiChartSpec` |

## DataSourceRef

> 数据源引用，声明仪表板使用的数据集

<!-- DOCS:AUTO START field-table:DataSourceRef -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `kind` | `"dataset"` | ✅ | _（待补 v.description）_ |
| `id` | `string` | ✅ | 数据源 ID |
| `title` | `string` | ✅ | 数据集可读标题，作为 analyses[].query.dataset_ref 的引用 key，要求在 data_sources[] 内唯一 |

<!-- DOCS:AUTO END -->

## DateControlConfig

> 日期控件配置

<!-- DOCS:AUTO START field-table:DateControlConfig -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `granularity` | `"year" \| "quarter" \| "month" \| "week" \| "day"` |  | 时间粒度 |
| `time_type` | `"duration" \| "moment"` |  | 时间配置类型：duration（范围）或 moment（单点），默认 duration。duration_type 仅在 duration 时生效，moment 下不应写 |
| `duration_type` | `"between" \| "start_at" \| "end_at"` |  | duration 子类型：between=区间两端、start_at=有起始无结束（>=）、end_at=有结束无起始（<=），默认 between。仅在 time_type=duration 时生效 |
| `default_relative` | `(string \| tuple)` |  | 相对日期默认值：t-N 表示前 N 个 granularity 单位，用户指令的时间单位与 granularity 不一致时按语义换算（粒度为日、说"前 2 月"→t-60）；moment/start_at/end_at 用单字符串，between 用二元组（如 ["t-7","t-1"]）；"默认前 N 年/近 N 年"指区间，写 ["t-N","t"]；禁止 between 两端同值（如 ["t-10","t-10"] 单点区间致数据为空） |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## DurationType

> duration 子类型：between=区间, start_at=有起始无结束, end_at=有结束无起始

**枚举**（3 个取值）：`"between"` · `"start_at"` · `"end_at"`

## EnumControlConfig

> 枚举控件配置（默认值仅支持选中/包含语义，无排除、不等于操作符）

<!-- DOCS:AUTO START field-table:EnumControlConfig -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `multiple` | `boolean` |  | 是否多选 |
| `options_source` | `"field_values" \| "static"` |  | 选项来源 |
| `static_options` | `{ label, value }[]` |  | 静态选项列表（options_source=static 时必填）；元素为 { label: 选项显示文本, value: 选项值（字符串或数字） } |
| `limit` | `number` |  | 动态取数条数上限（options_source=field_values 时可选，默认 100） |
| `searchable` | `boolean` |  | 是否支持搜索, 默认值为 true |
| `display_mode` | `"dropdown" \| "tile"` |  | 渲染形态：dropdown=下拉选择器（缺省）, tile=胶囊平铺（选项铺开、点击切换）。tile 仅用于低基数枚举维度（建议选项数 ≤ 3），选项较多时用 dropdown 避免胶囊换行撑高控件栏；tile 选项数硬上限为 30，超过部分被渲染层直接截断（不分页、不折叠），高基数维度必须用 dropdown |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## FetchSourceType

> 取数链路数据源类型

**枚举**（4 个取值）：`"cube"` · `"datatable"` · `"remote_excel"` · `"api"`

<!-- MANUAL: 非 object schema（variant），字段表脚本不生成，此处按类型渲染 -->
## IndicatorSpec

> indicator 范式指标卡判别联合（按 type：indicator-card）

**判别联合**（按 `type` 区分，1 个成员）：

| type | 成员 schema |
| --- | --- |
| `indicator-card` | `IndicatorCardSpec` |

## InsightSpec

<!-- DOCS:AUTO START field-table:InsightSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `id` | `string` | ✅ | 组件唯一标识 |
| `type` | `"insight"` | ✅ | 组件类型：洞察 |
| `content` | `string` |  | 洞察文本内容 |
| `insight_prompt` | `string` |  | 自定义洞察生成 prompt |
| `data_component_refs` | `(string \| string[])` |  | 绑定图表组件 ID，自动获取其数据生成洞察；单个写字符串，多个写数组（多图表合并） |
| `attach_to` | `string` |  | 附着目标组件 ID（图表，或 section/panel 容器；禁止指向 tab）；有值时为附着形态（不占布局项），无值时为独立栅格单元 |
| `attach_position` | `"top" \| "bottom"` |  | 附着方位（top/bottom）；attach_to 存在而缺省时按 top 处理 |

<!-- DOCS:AUTO END -->

## NumberControlConfig

> 数值控件配置

<!-- DOCS:AUTO START field-table:NumberControlConfig -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `operator` | `"eq" \| "ne" \| "gt" \| "gte" \| "lt" \| "lte" \| "null" \| "not_null"` |  | 条件操作符（默认 eq）；null/not_null（为空/不为空）无需 default_value |
| `aggregate` | `"SUM" \| "AVG" \| "COUNT" \| "COUNT_DISTINCT" \| "MAX" \| "MIN"` |  | 度量聚合方式：对聚合后度量值过滤时 |
| `placeholder` | `string` |  | 占位文本 |
| `min` | `number` |  | 最小值 |
| `max` | `number` |  | 最大值 |
| `step` | `number` |  | 步长 |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## NumberOperator

> 数值条件操作符

**枚举**（8 个取值）：`"eq"` · `"ne"` · `"gt"` · `"gte"` · `"lt"` · `"lte"` · `"null"` · `"not_null"`

## PanelSpec

<!-- DOCS:AUTO START field-table:PanelSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `id` | `string` | ✅ | 组件唯一标识 |
| `type` | `"panel"` | ✅ | 组件类型：Tab 面板 |
| `title` | `string` |  | 页签显示名（tab bar 上显示）；新建 tab 时用户指定的组件名称写入本字段 |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（variant），字段表脚本不生成，此处按类型渲染 -->
## ProgressSpec

> progress 范式进度条判别联合（按 type：progress）

**判别联合**（按 `type` 区分，1 个成员）：

| type | 成员 schema |
| --- | --- |
| `progress` | `ProgressChartSpec` |

## QueryControlBinding

> 查询控件字段绑定，用于一个逻辑控件控制多个数据集字段

<!-- DOCS:AUTO START field-table:QueryControlBinding -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `field` | `string` | ✅ | 绑定字段名 |
| `dataset_ref` | `string` |  | 绑定数据集（匹配 data_sources[].title） |
| `target_ids` | `string[]` |  | 精细目标，指定本绑定受影响的组件 ID |

<!-- DOCS:AUTO END -->

## QueryControlItem

> 单个查询条件（QueryControl 内的控件）

<!-- DOCS:AUTO START field-table:QueryControlItem -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `id` | `string` | ✅ | 控件 ID |
| `title` | `string` |  | 控件标题 |
| `type` | `"date_range" \| "enum_select" \| "text_input" \| "number_input"` | ✅ | 控件类型，按 type 必填对应 config：date_range→date_config / enum_select→enum_config / text_input→text_config / number_input→number_config |
| `field` | `string` | ✅ | 绑定字段名 |
| `dataset_ref` | `string` |  | 绑定数据集（不传则匹配所有含该字段的查询） |
| `default_value` | `unknown` |  | 查询控制的默认值（选中/包含语义），仅承载静态值（具体日期、固定值、枚举选中值）；相对日期表达式（t±N、today、now）禁用本字段，须写 date_config.default_relative，写在本字段会被取数引擎当静态日期解析失败报错。日期控件的静态值精度须与 date_config.granularity 匹配，精度超出粒度（如控件粒度为年但值含月日）会被取数引擎解析失败导致数据为空。enum_select 控件不支持排除语义（default_value 只能指定选中值、不能指定排除值），用户要求排除某值时置 need_clarification 告知不支持，建议改用 text/number 控件的 operator=ne 或明确指定要包含的值 |
| `target_ids` | `string[]` |  | 精细目标，指定本条件受影响的组件 ID |
| `bindings` | `{ field, dataset_ref, target_ids }[]` |  | 多字段绑定列表 |
| `date_config` | `{ granularity, time_type, duration_type, default_relative }` |  | 日期控件配置, type=date_range 时，必填 |
| `enum_config` | `{ multiple, options_source, static_options, limit, searchable, display_mode }` |  | 枚举控件配置, type=enum_select 时，必填 |
| `text_config` | `{ placeholder, operator }` |  | 文本控件配置, type=text_input 时，必填 |
| `number_config` | `{ operator, aggregate, placeholder, min, max, step }` |  | 数值控件配置, type=number_input 时，必填 |

<!-- DOCS:AUTO END -->

## QueryControlSpec

> 查询控件（QueryControl），作为 type: query_control 的组件放在 ui.components[] 中。新增 query_control 时必须在 layout.items 数组中追加对应布局项（禁止写成以 id 为键的对象 map），图表内查询控件的 `parent_id` 为 `{目标图表ID}`、；全局查询控件不设 `parent_id`

<!-- DOCS:AUTO START field-table:QueryControlSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `id` | `string` | ✅ | 控件 ID，对应 layout.items 中的 component_id |
| `type` | `"query_control"` | ✅ | _（待补 v.description）_ |
| `title` | `string` |  | 标题（可选，用于 UI 展示） |
| `target_ids` | `string[]` |  | 容器级精细目标，作为内含条件的默认 target_ids |
| `card` | `{ header_show, card_border_width, card_border_color, card_border_radius, card_box_shadow, card_padding, card_background_color, card_background_image, header_font_size, header_font_color, header_font_weight, header_font_style, header_align, header_divider_size, header_divider_color, header_background_color, header_background_image, header_remark, footer_remark, content_margin_top, content_empty_text, content_empty_image, content_empty_link }` |  | 卡片样式（可选），控制标题显隐、边框、背景等视觉定制 |
| `controls` | `{ id, title, type, field, dataset_ref, default_value, target_ids, bindings, date_config, enum_config, text_config, number_config }[]` | ✅ | 内含的查询条件列表 |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## QueryControlType

> 查询控件类型

**枚举**（4 个取值）：`"date_range"` · `"enum_select"` · `"text_input"` · `"number_input"`

## QueryRef

> QueryAgent 取数引用

<!-- DOCS:AUTO START field-table:QueryRef -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `message_id` | `string` |  | messageId |

<!-- DOCS:AUTO END -->

## SectionSpec

<!-- DOCS:AUTO START field-table:SectionSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `id` | `string` | ✅ | 组件唯一标识 |
| `type` | `"section"` | ✅ | 组件类型：Section 区段容器 |
| `section_type` | `"summary" \| "kpi_overview" \| "analysis" \| "detail"` |  | 区段语义类型：summary/kpi_overview/analysis/detail |
| `title` | `string` |  | 区段标题 |
| `subtitle` | `string` |  | 区段副标题 |
| `header_font_color` | `string` |  | 区段标题字体颜色 |
| `accent_color` | `string` |  | 标题左侧彩色竖条颜色（#RRGGBB） |
| `insight_prompt` | `string` |  | 自定义洞察生成 prompt，控制 LLM 输出格式和内容风格 |
| `show_insight` | `boolean` |  | 是否显示洞察栏；缺省等同 true |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## TabAlign

> Tab bar（非标题区）水平对齐方式

**枚举**（3 个取值）：`"left"` · `"center"` · `"right"`

## TabFontSpec

<!-- DOCS:AUTO START field-table:TabFontSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `active` | `{ font_size, bold, italic, color }` |  | Tab 选中态字体样式 |
| `inactive` | `{ font_size, bold, italic, color }` |  | Tab 未选中态字体样式 |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## TabListMode

> Tab 标签样式模式：underline / capsule / divider / block

**枚举**（4 个取值）：`"underline"` · `"capsule"` · `"divider"` · `"block"`

## TabOptionsSpec

<!-- DOCS:AUTO START field-table:TabOptionsSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `list_mode` | `"underline" \| "capsule" \| "divider" \| "block"` |  | 标签样式模式：capsule/underline/divider/block 默认 capsule |
| `font` | `{ active, inactive }` |  | 标签字体配置（选中态/未选中态） |
| `active` | `string` |  | 选中态填充色（capsule/block 模式生效） |
| `background` | `string` |  | Tab bar 背景色（capsule/block 模式生效） |
| `border_radius` | `number` |  | 圆角（capsule/block 模式生效，px） |
| `align` | `"left" \| "center" \| "right"` |  | Tab bar 水平对齐：left/center/right |

<!-- DOCS:AUTO END -->

## TabSpec

<!-- DOCS:AUTO START field-table:TabSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `id` | `string` | ✅ | 组件唯一标识 |
| `type` | `"tab"` | ✅ | 组件类型：Tab 容器 |
| `title` | `string` |  | Tab bar 左侧标题（可选）；用户对 tab 组件的命名应写入首个 panel.title（页签名），仅当用户明确要求 tab bar 左侧标题时才写本字段 |
| `options` | `{ list_mode, font, active, background, border_radius, align }` |  | Tab 样式选项配置 |
| `active_panel_id` | `string` |  | 初始选中面板的组件 ID（panel component_id）；缺省或 ID 不存在时默认展示第一个面板 |

<!-- DOCS:AUTO END -->

## TableCellFont

<!-- DOCS:AUTO START field-table:TableCellFont -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `font_size` | `number` |  | 字号（px） |
| `bold` | `boolean` |  | 是否加粗 |
| `italic` | `boolean` |  | 是否斜体 |
| `color` | `string` |  | 字体颜色（#RRGGBB） |
| `text_align` | `"left" \| "center" \| "right"` |  | 水平对齐 |
| `vertical_align` | `"top" \| "middle" \| "bottom"` |  | 垂直对齐 |

<!-- DOCS:AUTO END -->

## TableFont

<!-- DOCS:AUTO START field-table:TableFont -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `body` | `{ font_size, bold, italic, color, text_align, vertical_align }` |  | 表格正文字体 |
| `header` | `{ font_size, bold, italic, color, text_align, vertical_align }` |  | 表头字体 |
| `row_header` | `{ font_size, bold, italic, color, text_align, vertical_align }` |  | 行表头字体 |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（union），字段表脚本不生成，此处按类型渲染 -->
## TableMeasureRef

**联合类型**：`string | { field, alias, description, format, mark, conditional_format }`

对象成员字段表：

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `field` | `string` | ✅ | 字段 id |
| `alias` | `string` |  | 显示别名（图表上实际显示的字段名/度量名）。用户说“字段描述语改为X/显示名改为X/字段重命名为X/改字段名/改度量名”等改显示文本诉求一律写本字段（alias=X）；不存在独立的“描述语”字段 |
| `description` | `string` |  | 字段描述(ui上以字段右侧 icon 呈现 , 悬停展开 tooltip 显示描述)。涉及计算字段时，默认标注计算口径 |
| `format` | `("auto" \| "raw" \| "integer" \| "decimal-1" \| "decimal-2" \| "percent" \| "percent-1" \| "percent-2" \| "currency-cny" \| "currency-usd" \| string)` |  | 数值格式化（纯显示格式，不改变数据聚合/计算——与度量本身是否为比例类型无关，用户要求百分比/小数/货币等格式时直接写入）。注意：percent 格式仅把值本身按比例展示（×100 加 %），不做 占总计/同比 换算——当度量为绝对值（金额/数量等）而 用户要求"显示为百分比/占比"时，正确做法是给度量配置 percent_of 占比高级计算（格 式会自动推导 percent-2），禁止对绝对值直接写 percent/percent-2。支持 单位\|除数  语法进行数量级换算（如 #,##0.00万元\|10000），单位用完整表述不缩写为单字（万元/亿元/千元），同时 alias 也应带上单位。alias 含比例语义（环比/同比/比率/占比/百分比/增长率等）时默认 `percent-2`。comparison 度量的 encoding 条目必须显式写入 `format`，缺省用 `percent-2`。 |
| `mark` | `"bar" \| "line" \| "area"` |  | 系列图形类型（组合图：某度量显示为折线） |
| `conditional_format` | `{ operator, compare_with, compare_field, compare_aggregate, value, text_color, background_color, bold, italic, icon }[]` |  | 条件格式（按序匹配：同一视觉效果取首个命中规则，不同视觉效果可由不同规则分别命中并同时生效） |

<!-- MANUAL: 非 object schema（variant），字段表脚本不生成，此处按类型渲染 -->
## TableSpec

> layout 范式表格判别联合（按 type：cross-table / ranking-list）

**判别联合**（按 `type` 区分，2 个成员）：

| type | 成员 schema |
| --- | --- |
| `cross-table` | `CrossTableSpec` |
| `ranking-list` | `RankingListSpec` |

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## TableTextVerticalAlign

> 单元格垂直对齐（对应 tableFont.*.textVerticalAlign）

**枚举**（3 个取值）：`"top"` · `"middle"` · `"bottom"`

## TextControlConfig

> 文本控件配置

<!-- DOCS:AUTO START field-table:TextControlConfig -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `placeholder` | `string` |  | 占位文本 |
| `operator` | `"contains" \| "not_contains" \| "ne" \| "eq" \| "starts_with" \| "ends_with" \| "null" \| "not_null"` |  | 匹配模式（取值为 OlapFilterOperator 子集）；null/not_null（为空/不为空）无需 default_value |

<!-- DOCS:AUTO END -->

## TextSpec

<!-- DOCS:AUTO START field-table:TextSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `id` | `string` | ✅ | 组件唯一标识 |
| `type` | `"text"` | ✅ | 组件类型：富文本 |
| `content` | `string` |  | 富文本内容 |

<!-- DOCS:AUTO END -->

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## TimeConfigType

> 时间配置类型：duration=时间范围, moment=单时间点

**枚举**（2 个取值）：`"duration"` · `"moment"`
