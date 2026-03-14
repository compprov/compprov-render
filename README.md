# compprov-render

Visualization renderer for [compprov](https://github.com/compprov) — interactive browser-based views for **Calculation Provenance Graph (CPG)** data produced by [compprov-core](https://github.com/compprov/compprov-core).

Opens directly from the local filesystem (no server required).

---

## Pages

### `graph.html` — Provenance Graph

Renders the CPG as an interactive node-edge graph.

- **Variables** shown as nodes: Input (blue ellipse), Output (green box)
- **Operations** shown as nodes (orange diamond) with labeled edges from arguments and an edge to the result
- Right sidebar: configure which fields are displayed per node type (Input Variable, Output Variable, Operation)
- Click any node → bottom panel slides up with full details
- Click the descriptor title (top-left) → shows descriptor metadata
- **Load JSON** button — paste a JSON to rebuild the graph

### `plot.html` — Provenance Plot

Plots numeric variable values across one or more datasets for side-by-side comparison.

- **Plot types**: Points, Line, Table
- **Plot tab**: configure X-axis slots — rename, reorder (drag handle), hide/show per slot
- **Data tab**: load datasets additively (JSON paste), reorder variables per dataset (drag handle), remove datasets
- Positional mapping: nth numeric variable in a dataset → nth X-axis slot; reordering variables shifts the mapping without affecting slot config
- Click a chart point → bottom panel slides up with full variable details
- Click any field name in the detail panel → sets that field as the global display label (reflected in the Data tab and chart tooltips)
- **Apply labels to X-axis** button — applies current display labels as X-axis slot names
- Each dataset gets its own color; multiple datasets can be compared on the same chart

---

## Input Format

Both pages consume the JSON output of [compprov-core](https://github.com/compprov/compprov-core).

```json
{
  "descriptor": { "name": "...", "meta": {} },
  "variables": [
    {
      "track": { "id": "i_1", "numericId": 1, "kind": "INPUT", "descriptor": { "name": "x", "meta": {} }, "valueClass": "java.math.BigDecimal" },
      "value": 3
    }
  ],
  "operations": [
    {
      "track": { "id": "op_1", "numericId": 1, "descriptor": { "name": "add", "meta": { "formula": "(a+b)mc" } } },
      "arguments": { "a": "i_2", "b": "i_3", "mc": "i_1" },
      "resultId": "o_4"
    }
  ]
}
```

---

## Dependencies

All libraries are bundled in `lib/` — no CDN, no build step, no server.

| File | Library |
|---|---|
| `lib/jquery.min.js` | jQuery 3.x |
| `lib/vis-network.min.js` | vis-network 9.x |
| `lib/vis-network.min.css` | vis-network styles |
| `lib/chart.min.js` | Chart.js 4.x |

---

## Examples

Sample CPG JSON files are in the `examples/` directory.
