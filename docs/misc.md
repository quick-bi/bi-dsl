# 其它

> 未归类 schema。

本文件包含（3）：`PageNavListMode` / `PageNavPlacement` / `PageNavSpec`

---
<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## PageNavListMode

**枚举**（2 个取值）：`"underline"` · `"capsule"`

<!-- MANUAL: 非 object schema（picklist），字段表脚本不生成，此处按类型渲染 -->
## PageNavPlacement

**枚举**（2 个取值）：`"below_header"` · `"above_header"`

## PageNavSpec

> 页面级导航（吸顶 scroll-spy 导航条，自动锚定到页面内全部顶层 section）

<!-- DOCS:AUTO START field-table:PageNavSpec -->

| 字段 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| `enabled` | `boolean` |  | 是否启用页面导航，默认 true |
| `list_mode` | `"underline" \| "capsule"` |  | 标签样式：underline 下划线 / capsule 胶囊，默认 underline |
| `placement` | `"below_header" \| "above_header"` |  | 导航条位置：below_header 在 header 下方 / above_header 在 header 上方，默认 below_header |

<!-- DOCS:AUTO END -->
