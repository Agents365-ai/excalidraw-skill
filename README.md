# excalidraw skill

Claude Code skill for generating Excalidraw diagrams and exporting to PNG/SVG locally.

[中文文档](README_CN.md)

## What it does

- Generates `.excalidraw` JSON files from natural language descriptions
- Exports diagrams to PNG or SVG using `excalidraw-brute-export-cli` (Firefox-based)
- Triggers automatically when diagrams would help explain complex systems

## Dependencies

| Tool | Purpose |
|------|---------|
| `excalidraw-brute-export-cli` | CLI to export `.excalidraw` → PNG/SVG |
| `Playwright + Firefox` | Headless browser used by the CLI to render diagrams |

## Install

```bash
npm install -g excalidraw-brute-export-cli
npx playwright install firefox
```

### macOS patch (one-time, required)

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
