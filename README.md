# xd-self-market

个人 AI 工具集归档仓库，支持 Claude Code 和 OpenClaw。

## 结构

```
xd-self-market/
├── skills/      # 统一源格式（Claude Code 格式）
├── openclaw/    # OpenClaw 兼容副本
├── commands/    # slash commands
├── mcps/        # MCP server 配置
└── scripts/     # 公共脚本
```

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

## 内容

### Skills

| Skill | 描述 |
|-------|------|
| `xd-git-push` | 提交代码前二次确认 |
| `xd-blog-style` | 基于博客风格写作 |

### Commands

（待添加）

### MCPs

（待添加）
