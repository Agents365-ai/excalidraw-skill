---
name: excalidraw
description: Use when user requests diagrams, flowcharts, architecture charts, or visualizations. Also use proactively when explaining systems with 3+ components, complex data flows, or relationships that benefit from visual representation. Generates .excalidraw files and exports to PNG/SVG via Kroki API or locally using excalidraw-brute-export-cli.
---

# Excalidraw Diagrams

## Overview

Generate `.excalidraw` JSON files and export to PNG/SVG.

**Two export options:**
- **Kroki API** (`curl`) — zero install, SVG output only
- **excalidraw-brute-export-cli** — local Firefox-based, PNG + SVG

**Supported formats:** PNG (local CLI only), SVG (both options). PDF is NOT supported.

## When to Use

**Explicit triggers:** user says "画图", "diagram", "visualize", "flowchart", "draw", "架构图", "流程图"

**Proactive triggers:**
- Explaining a system with 3+ interacting components
- Describing a multi-step process or decision tree
- Comparing architectures or approaches side by side

**Skip when:** a simple list or table suffices, or user is in a quick Q&A flow

## Prerequisites

### Option A: Kroki API (recommended — zero install, SVG only)

```bash
# Just needs curl (pre-installed on macOS/Linux/Windows Git Bash)
curl --version
```

No additional setup. SVG rendered via `https://kroki.io`.

### Option B: Local CLI (required for PNG)

The CLI uses **Firefox** (not Chromium). Check and install:

```bash
npm install -g excalidraw-brute-export-cli
npx playwright install firefox
```

**macOS patch (one-time, required):**
```bash
CLI_MAIN=$(npm root -g)/excalidraw-brute-export-cli/src/main.js
sed -i '' 's/keyboard.press("Control+O")/keyboard.press("Meta+O")/' "$CLI_MAIN"
sed -i '' 's/keyboard.press("Control+Shift+E")/keyboard.press("Meta+Shift+E")/' "$CLI_MAIN"
```

**Windows/Linux:** No patch needed.

## Workflow

1. **Check deps** — use Kroki (curl) for SVG; use local CLI for PNG
2. **Plan** — identify elements, relationships, layout direction (LR or TB)
3. **Generate** — write `.excalidraw` JSON file to disk
4. **Export** — run Kroki or CLI command
5. **Report** — tell user the output file path

## Excalidraw JSON Structure

### File skeleton

```json
{
  "type": "excalidraw",
  "version": 2,
  "source": "claude-code",
  "elements": [],
  "appState": { "viewBackgroundColor": "#ffffff" }
}
```

### Element types

| type      | use for                          |
|-----------|----------------------------------|
| rectangle | boxes, components, modules       |
| ellipse   | start/end nodes, databases       |
| diamond   | decision points                  |
| arrow     | directed connections             |
| line      | undirected connections           |
| text      | standalone labels                |

### Required properties (all elements)

```json
{
  "id": "<unique-string>",
  "type": "rectangle",
  "x": 100, "y": 100,
  "width": 160, "height": 60,
  "angle": 0,
  "strokeColor": "#1e1e1e",
  "backgroundColor": "#ffffff",
  "fillStyle": "solid",
  "strokeWidth": 2,
  "roughness": 1,
  "opacity": 100
}
```

For `text` elements, add: `"text": "Label", "fontSize": 16, "fontFamily": 1, "textAlign": "center"`

### Arrow binding

```json
{
  "type": "arrow",
  "points": [[0, 0], [120, 0]],
  "startBinding": { "elementId": "<source-id>", "gap": 5, "focus": 0 },
  "endBinding":   { "elementId": "<target-id>", "gap": 5, "focus": 0 }
}
```

**Layout tip:** allocate ~200px per node to avoid overlaps. Plan a grid before assigning x/y coordinates.

## Export

### Option A: Kroki API (SVG only — zero install)

```bash
# SVG via Kroki API
curl -s -X POST https://kroki.io/excalidraw/svg \
  -H "Content-Type: application/json" \
  --data-binary "@diagram.excalidraw" \
  -o diagram.svg

# Via local Kroki Docker (offline)
curl -s -X POST http://localhost:8000/excalidraw/svg \
  -H "Content-Type: application/json" \
  --data-binary "@diagram.excalidraw" \
  -o diagram.svg
```

### Option B: Local CLI (PNG + SVG)

```bash
# PNG at 2x scale (recommended)
excalidraw-brute-export-cli -i diagram.excalidraw -o diagram.png -f png -s 2

# PNG at 1x scale
excalidraw-brute-export-cli -i diagram.excalidraw -o diagram.png -f png -s 1

# SVG
excalidraw-brute-export-cli -i diagram.excalidraw -o diagram.svg -f svg -s 1
```

**Required flags:** `-f` (format: `png` or `svg`) and `-s` (scale: `1`, `2`, or `3`).

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Kroki returns error | Ensure file is valid JSON with `"type": "excalidraw"` and `"elements"` array |
| Kroki only outputs SVG | Use local CLI (`excalidraw-brute-export-cli`) for PNG |
| Export fails with "Missing required flag" | Always pass `-f png` and `-s 2` |
| Export fails with "Executable doesn't exist" | Run `npx playwright install firefox` |
| macOS: timeout waiting for file chooser | Apply the macOS Meta patch above |
| Arrow `points` not relative to origin | `points` always start at `[0,0]` |
| Missing `id` on elements | Use a short unique string per element |
| Overlapping elements | Plan a ~200px grid before assigning x/y |
