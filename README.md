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

## License

MIT

## Support

If this skill helps you, consider supporting the author:

<table>
  <tr>
    <td align="center">
      <img src="https://raw.githubusercontent.com/Agents365-ai/images_payment/main/qrcode/wechat-pay.png" width="180" alt="WeChat Pay">
      <br>
      <b>WeChat Pay</b>
    </td>
    <td align="center">
      <img src="https://raw.githubusercontent.com/Agents365-ai/images_payment/main/qrcode/alipay.png" width="180" alt="Alipay">
      <br>
      <b>Alipay</b>
    </td>
    <td align="center">
      <img src="https://raw.githubusercontent.com/Agents365-ai/images_payment/main/qrcode/buymeacoffee.png" width="180" alt="Buy Me a Coffee">
      <br>
      <b>Buy Me a Coffee</b>
    </td>
  </tr>
</table>

## Author

**Agents365-ai**

- Bilibili: https://space.bilibili.com/441831884
- GitHub: https://github.com/Agents365-ai
