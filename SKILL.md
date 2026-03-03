---
name: excalidraw
description: Use when user requests diagrams, flowcharts, architecture charts, or visualizations. Also use proactively when explaining systems with 3+ components, complex data flows, or relationships that benefit from visual representation. Generates .excalidraw files and exports to PNG/PDF locally.
---

# Excalidraw Diagrams

## Overview

Generate `.excalidraw` JSON files and export to PNG/PDF/SVG locally using `excalidraw-brute-export-cli` (Playwright-based, no Docker needed).

## When to Use

**Explicit triggers:** user says "画图", "diagram", "visualize", "flowchart", "draw", "架构图", "流程图"

**Proactive triggers:**
- Explaining a system with 3+ interacting components
- Describing a multi-step process or decision tree
- Comparing architectures or approaches side by side

**Skip when:** a simple list or table suffices, or user is in a quick Q&A flow

## Prerequisites

Before exporting, verify both tools are available:

```bash
# Check excalidraw-brute-export-cli
excalidraw-brute-export-cli --version

# Check Playwright chromium
ls ~/Library/Caches/ms-playwright/ 2>/dev/null | grep chromium
```

If missing, install:

```bash
# Install CLI (if not found)
npm install -g excalidraw-brute-export-cli

# Install Playwright chromium (if not found)
npx playwright install chromium
```

Note: If Playwright MCP is already configured, chromium is likely already installed — skip that step.

## Workflow

1. **Check deps** — verify excalidraw-brute-export-cli and Playwright chromium are present; install if missing
2. **Plan** — identify elements, relationships, layout direction (LR or TB)
3. **Generate** — write `.excalidraw` JSON file to disk
4. **Export** — run CLI to produce PNG, PDF, or SVG
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

### Install (first time only)

```bash
npm install -g excalidraw-brute-export-cli
npx playwright install chromium
```

### Commands

```bash
# PNG (default 2x scale)
excalidraw-brute-export-cli -i diagram.excalidraw -o diagram.png

# PDF (vector)
excalidraw-brute-export-cli -i diagram.excalidraw -o diagram.pdf

# SVG
excalidraw-brute-export-cli -i diagram.excalidraw -o diagram.svg

# Smaller PNG
excalidraw-brute-export-cli -i diagram.excalidraw -o diagram.png --scale 1
```

Format is inferred from the output file extension.

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Arrow `points` not relative to origin | `points` always start at `[0,0]` |
| Missing `id` on elements | Use a short unique string per element |
| Arrow binding without `points` array | Always include `points` |
| Overlapping elements | Plan a ~200px grid before assigning x/y |
| Export fails silently | Run `npx playwright install chromium` |
