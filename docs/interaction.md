# 交互（下钻 / 联动）

> 看板级钻取 DrillSpec、看板级联动 LinkageRule 与字段映射。

本文件包含（4）：`DrillSpec` / `FieldMapEntry` / `FieldMapFieldRef` / `LinkageRuleSpec`

---
<!-- MANUAL: 非 object schema（variant），字段表脚本不生成，此处按类型渲染 -->
## DrillSpec

> 看板级钻取配置（variant），不用于组件 interaction.drill——组件级下钻用 ComponentDrillSpec（channel + path），本 schema 的 mode/on 结构禁止出现在组件 interaction.drill

**判别联合**（按 `mode` 区分，3 个成员）：

| mode | 成员 schema |
| --- | --- |
| `auto` | `{ mode, auto, on, trigger, allow_roll_up }` |
| `granularities` | `{ mode, granularities, on }` |
| `path` | `{ mode, path, on }` |

`mode = auto` 成员字段表：

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `mode` | `"auto"` | ✅ | _（待补 v.description）_ |
| `auto` | `"time" \| "geo"` | ✅ | 自动下钻类型 |
| `on` | `string` |  | 作用于哪个 encoding 通道，省略时为主维度 |
| `trigger` | `"click" \| "double_click"` |  | 触发方式，默认 click |
| `allow_roll_up` | `boolean` |  | 是否允许向上回钻，默认 true |

`mode = granularities` 成员字段表：

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `mode` | `"granularities"` | ✅ | _（待补 v.description）_ |
| `granularities` | `"year" \| "year-quarter" \| "quarter" \| "year-month" \| "month" \| "year-week" \| "week" \| "year-month-day" \| "day" \| "hour" \| "minute" \| "second"[]` | ✅ | 粒度链，从粗到细 |
| `on` | `string` |  | 作用于哪个 encoding 通道 |

`mode = path` 成员字段表：

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `mode` | `"path"` | ✅ | _（待补 v.description）_ |
| `path` | `string[]` | ✅ | 字段路径（从粗到细），仅作交互下钻路径，禁止加入 query.dimensions（取数分组维度独立声明，通常只含当前展示层维度，下钻时引擎动态切换；把 path 全部字段加进 dimensions 会导致数据行爆炸） |
| `on` | `string` |  | 作用于哪个 encoding 通道 |

## FieldMapEntry

> 字段映射条目，描述源→目标的字段对应关系

<!-- DOCS:AUTO START field-table:FieldMapEntry -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `source` | `{ field, granularity }` | ✅ | 源组件字段引用 |
| `target` | `{ field, granularity }` | ✅ | 目标组件字段引用 |

<!-- DOCS:AUTO END -->

## FieldMapFieldRef

> 字段映射中的字段引用

<!-- DOCS:AUTO START field-table:FieldMapFieldRef -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `field` | `string` | ✅ | 字段名，与数据集 schema 的 name/caption 一致 |
| `granularity` | `string` |  | 字段粒度，用于日期等需要粒度对齐的场景 |

<!-- DOCS:AUTO END -->

## LinkageRuleSpec

> 精确联动规则，描述源组件点击到目标组件响应的路由关系

<!-- DOCS:AUTO START field-table:LinkageRuleSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `id` | `string` | ✅ | 联动规则唯一 ID |
| `source` | `string` | ✅ | 源组件 ID，触发联动的组件 |
| `targets` | `string[]` |  | 目标组件 ID 列表，省略表示同数据集所有组件，空数组表示显式禁用 |
| `trigger` | `"click"` |  | 触发方式，默认 click |
| `mode` | `"filter"` |  | 联动模式：filter=过滤取数（默认） |
| `field_map` | `{ source, target }[]` |  | 字段映射列表，source/target 各自携带 field + 可选 granularity，省略时按同名匹配 |

<!-- DOCS:AUTO END -->
