# 常量与共享 entries

> 枚举常量、能力矩阵与供 schema 展开复用的 entries。

本文件包含（16）：`AIChartType` / `DRILL_SUPPORT` / `LINKAGE_SUPPORT` / `barComponentDrillMeta` / `chartBaseEntries` / `combinationComponentDrillMeta` / `commonSpecEntries` / `componentBaseEntries` / `crossTableComponentDrillMeta` / `encodingMeasureRefEntries` / `funnelComponentDrillMeta` / `lineComponentDrillMeta` / `pieComponentDrillMeta` / `rankingListComponentDrillMeta` / `scatterComponentDrillMeta` / `stripComponentDrillMeta`

---
### AIChartType

对象（12 键）：`BAR` · `STRIP` · `LINE` · `POLYLINE` · `COMBINATION` · `FUNNEL` · `PIE` · `SCATTER` · `CROSS_TABLE` · `RANKING_LIST` · `PROGRESS` · `INDICATOR_CARD`

### barComponentDrillMeta

对象（1 键）：`channels`

### chartBaseEntries

共享 entries（13 字段）：`id` · `title` · `card` · `analysis_ref` · `analysis_text` · `interaction` · `encoding` · `axis` · `legend` · `label` · `tooltip` · `color` · `analysis`

### combinationComponentDrillMeta

对象（1 键）：`channels`

### commonSpecEntries

共享 entries（5 字段）：`id` · `title` · `description` · `intent` · `version`

### componentBaseEntries

共享 entries（6 字段）：`id` · `title` · `card` · `analysis_ref` · `analysis_text` · `interaction`

### crossTableComponentDrillMeta

对象（1 键）：`channels`

### DRILL_SUPPORT

Map（10 项）：

| key | value |
| --- | --- |
| `bar` | `{"channels":["x","color"]}` |
| `strip` | `{"channels":["x","color"]}` |
| `line` | `{"channels":["x","color"]}` |
| `polyline` | `{"channels":["x","color"]}` |
| `combination` | `{"channels":["x","color"]}` |
| `funnel` | `{"channels":["x","color"]}` |
| `pie` | `{"channels":["color"]}` |
| `scatter` | `{"channels":["color","x","category"]}` |
| `cross-table` | `{"channels":["rows"]}` |
| `ranking-list` | `{"channels":["rows"]}` |

### encodingMeasureRefEntries

共享 entries（5 字段）：`field` · `alias` · `description` · `format` · `mark`

### funnelComponentDrillMeta

对象（1 键）：`channels`

### lineComponentDrillMeta

对象（1 键）：`channels`

### LINKAGE_SUPPORT

Set（10 项）：`bar` · `strip` · `line` · `polyline` · `combination` · `funnel` · `pie` · `scatter` · `cross-table` · `ranking-list`

### pieComponentDrillMeta

对象（1 键）：`channels`

### rankingListComponentDrillMeta

对象（1 键）：`channels`

### scatterComponentDrillMeta

对象（1 键）：`channels`

### stripComponentDrillMeta

对象（1 键）：`channels`
