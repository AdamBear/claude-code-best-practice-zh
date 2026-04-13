# Time SVG Creator - 参考

## SVG 模板

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 400 250" width="400" height="250">
  <defs>
    <linearGradient id="bg" x1="0%" y1="0%" x2="0%" y2="100%">
      <stop offset="0%" style="stop-color:#0a1628"/>
      <stop offset="100%" style="stop-color:#1a2744"/>
    </linearGradient>
  </defs>
  <rect width="400" height="250" rx="16" fill="url(#bg)"/>
  <text x="200" y="50" text-anchor="middle" fill="#8892b0" font-family="sans-serif" font-size="16" font-weight="600">Dubai Time</text>
  <text x="200" y="120" text-anchor="middle" fill="#ffffff" font-family="sans-serif" font-size="52" font-weight="bold">{{TIME}}</text>
  <text x="200" y="160" text-anchor="middle" fill="#64ffda" font-family="sans-serif" font-size="16">{{TIMEZONE}}</text>
  <text x="200" y="195" text-anchor="middle" fill="#ccd6f6" font-family="sans-serif" font-size="14">Dubai, UAE</text>
  <text x="200" y="225" text-anchor="middle" fill="#8892b0" font-family="sans-serif" font-size="12">{{DATE}}</text>
</svg>
```

### 占位符

| 占位符 | 替换内容 | 示例 |
|------|------|------|
| `{{TIME}}` | 输入中的 `time` | `14:30:45` |
| `{{TIMEZONE}}` | 输入中的 `timezone` | `GST (UTC+4)` |
| `{{DATE}}` | 从 `formatted` 中提取日期 | `2026-03-12` |
| `{{FORMATTED}}` | 完整的 `formatted` 字符串 | `2026-03-12 14:30:45 +04` |

## 输出路径

| 文件 | 路径 |
|------|------|
| SVG 卡片 | `agent-teams/output/dubai-time.svg` |
| Markdown 摘要 | `agent-teams/output/output.md` |
