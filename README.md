# excalidraw skill

Claude Code skill for generating Excalidraw diagrams and exporting to PNG/PDF/SVG locally.

用于在 Claude Code 中生成 Excalidraw 图表并本地导出为 PNG/PDF/SVG 的 skill。

---

## English

### What it does

- Generates `.excalidraw` JSON files from natural language descriptions
- Exports diagrams to PNG, PDF, or SVG using `excalidraw-brute-export-cli`
- Triggers automatically when diagrams would help explain complex systems

### Dependencies

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

### Usage

Just describe what you want:

```
Create a microservices architecture diagram with API Gateway, user service, order service, and database
```

Claude will generate the `.excalidraw` file and export it to PNG automatically.

### Files

- `SKILL.md` — skill instructions loaded by Claude Code
- `README.md` — this file

---

## 中文

### 功能说明

- 根据自然语言描述生成 `.excalidraw` JSON 文件
- 使用 `excalidraw-brute-export-cli` 将图表导出为 PNG、PDF 或 SVG
- 当图表有助于解释复杂系统时自动触发

### 依赖项

| 工具 | 用途 |
|------|------|
| `excalidraw-brute-export-cli` | 将 `.excalidraw` 导出为 PNG/PDF/SVG 的命令行工具 |
| `Playwright + Chromium` | CLI 工具使用的无头浏览器，用于渲染图表 |

### 安装

```bash
npm install -g excalidraw-brute-export-cli
npx playwright install chromium
```

> 如果已配置 Playwright MCP，Chromium 通常已经安装好，无需重复安装。

### 使用方式

直接描述你想要的图表：

```
画一个微服务架构图，包含 API Gateway、用户服务、订单服务和数据库
```

Claude 会自动生成 `.excalidraw` 文件并导出为 PNG。

### 文件说明

- `SKILL.md` — Claude Code 加载的 skill 指令文件
- `README.md` — 本文件
