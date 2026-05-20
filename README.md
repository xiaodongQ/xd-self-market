# xd-self-market

个人 AI 工具集归档仓库，支持 Claude Code marketplace 加载。

## 安装

在 Claude Code `settings.json` 中添加：

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

## 插件列表

| 插件 | 描述 |
|------|------|
| `xd-blog-style` | 基于 xiaodongq 博客风格写作 |
| `xd-git-push` | 提交代码前与用户二次确认 |
| `prompt-optimizer` | 通用提示词优化器 |
| `example` | 示例插件（参考规范） |

## 开发

新增插件参考 `docs/plugin-guide.md`。