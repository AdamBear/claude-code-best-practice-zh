---
name: time-fetcher
description: 通过 bash 命令获取迪拜当前时间的说明
user-invocable: false
---

## 迪拜时间获取器

### 命令

```bash
TZ='Asia/Dubai' date '+%Y-%m-%d %H:%M:%S %Z'
```

### 预期输出格式

`YYYY-MM-DD HH:MM:SS +04`（海湾标准时间）

### 时区详情

- Timezone: Asia/Dubai
- Offset: UTC+4
- Abbreviation: GST (Gulf Standard Time)
- 迪拜不实行夏令时

### 返回格式

请返回以下字段：
- `time`：仅时间部分（HH:MM:SS）
- `timezone`：`"GST (UTC+4)"`
- `formatted`：命令输出的完整字符串
