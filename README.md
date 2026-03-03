# excalidraw skill

Claude Code skill for generating Excalidraw diagrams and exporting to PNG/PDF/SVG locally.

[中文文档](README.zh.md)

## What it does

- Generates `.excalidraw` JSON files from natural language descriptions
- Exports diagrams to PNG, PDF, or SVG using `excalidraw-brute-export-cli`
- Triggers automatically when diagrams would help explain complex systems

## Dependencies

| Tool | Purpose |
|------|---------|
| `excalidraw-brute-export-cli` | CLI to export `.excalidraw` → PNG/PDF/SVG |
| `Playwright + Chromium` | Headless browser used by the CLI to render diagrams |

## Install

```bash
npm install -g excalidraw-brute-export-cli
npx playwright install chromium
```

> If Playwright MCP is already configured, Chromium is likely already installed.

## Usage

Just describe what you want:

```
Create a microservices architecture diagram with API Gateway, user service, order service, and database
```

Claude will generate the `.excalidraw` file and export it to PNG automatically.

## Files

- `SKILL.md` — skill instructions loaded by Claude Code
- `README.md` — this file (English)
- `README.zh.md` — Chinese documentation
