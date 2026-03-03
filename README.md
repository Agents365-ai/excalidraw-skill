# excalidraw skill

Claude Code skill for generating Excalidraw diagrams and exporting to PNG/PDF/SVG locally.

## What it does

- Generates `.excalidraw` JSON files from natural language descriptions
- Exports diagrams to PNG, PDF, or SVG using `excalidraw-brute-export-cli`
- Triggers automatically when diagrams would help explain complex systems

## Dependencies

| Tool | Purpose |
|------|---------|
| `excalidraw-brute-export-cli` | CLI to export `.excalidraw` → PNG/PDF/SVG |
| `Playwright + Chromium` | Headless browser used by the CLI to render diagrams |

### Install

```bash
npm install -g excalidraw-brute-export-cli
npx playwright install chromium
```

> If Playwright MCP is already configured, Chromium is likely already installed.

## Usage

Just describe what you want:

```
画一个微服务架构图，包含 API Gateway、用户服务、订单服务和数据库
```

Claude will generate the `.excalidraw` file and export it to PNG automatically.

## Files

- `SKILL.md` — skill instructions loaded by Claude Code
- `README.md` — this file
