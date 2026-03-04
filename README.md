# excalidraw skill

Claude Code skill for generating Excalidraw diagrams and exporting to PNG/SVG via Kroki API or locally.

[中文文档](README_CN.md)

## What it does

- Generates `.excalidraw` JSON files from natural language descriptions
- Exports SVG via **Kroki** API — zero install, just `curl`
- Exports PNG/SVG locally using `excalidraw-brute-export-cli` (Firefox-based)
- Triggers automatically when diagrams would help explain complex systems

## Dependencies

| Tool | Purpose |
|------|---------|
| `curl` | Send `.excalidraw` to Kroki API for SVG rendering |
| `excalidraw-brute-export-cli` | Local CLI to export `.excalidraw` → PNG/SVG |
| `Playwright + Firefox` | Headless browser used by the local CLI |

`curl` is pre-installed on macOS, Linux, and Windows (Git Bash / WSL).

## Install

### Option A: Kroki API (recommended — zero install, SVG only)

```bash
# curl is already available — just verify:
curl --version
```

No additional setup. SVG rendered via `https://kroki.io`.

### Option B: Local CLI (required for PNG)

```bash
npm install -g excalidraw-brute-export-cli
npx playwright install firefox
```

### Platform notes

| Platform | Extra step |
|----------|------------|
| **macOS** | Apply one-time patch (see below) |
| **Windows** | No extra steps needed |
| **Linux** | No extra steps needed |

### macOS patch (one-time, required for local CLI)

The CLI uses `Control+O` / `Control+Shift+E` but macOS requires `Meta` (Cmd):

```bash
CLI_MAIN=$(npm root -g)/excalidraw-brute-export-cli/src/main.js
sed -i '' 's/keyboard.press("Control+O")/keyboard.press("Meta+O")/' "$CLI_MAIN"
sed -i '' 's/keyboard.press("Control+Shift+E")/keyboard.press("Meta+Shift+E")/' "$CLI_MAIN"
```

## Usage

Just describe what you want:

```
Create a microservices e-commerce architecture with API Gateway, auth/user/order/product/payment services,
Kafka message queue, notification service, and separate databases for each service
```

Claude will generate the `.excalidraw` file and export it to PNG automatically.

## Example

**Prompt:**
> Create a microservices e-commerce architecture with Mobile/Web/Admin clients, API Gateway,
> Auth/User/Order/Product/Payment services, Kafka message queue, Notification service,
> and User DB / Order DB / Product DB / Redis Cache / Stripe API

**Output:**

![Microservices Architecture](assets/microservices-example.png)

## Files

- `SKILL.md` — skill instructions loaded by Claude Code
- `README.md` — this file (English)
- `README_CN.md` — Chinese documentation
- `assets/` — example diagrams

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
