# xd-self-market

个人 Skills / Commands / MCPs 归档仓库。

## 内容

| 目录 | 用途 |
|------|------|
| `skills/` | 统一源格式（Claude Code 格式） |
| `openclaw/` | OpenClaw 兼容副本 |
| `commands/` | slash commands |
| `mcps/` | MCP server 配置 |
| `scripts/` | 公共脚本 |

## 使用方式

### Claude Code

在 `settings.json` 中添加：

```json
"extraKnownMarketplaces": {
  "xd-self-market": {
    "source": {
      "source": "directory",
      "path": "/path/to/xd-self-market"
    }
  }
}
```

### OpenClaw

参考 OpenClaw 文档配置 `skills.load.extraDirs`。
