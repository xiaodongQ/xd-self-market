# xd-self-market

个人 AI 工具集归档仓库，支持 Claude Code marketplace 加载。

## 结构

```
xd-self-market/
├── .claude-plugin/
│   └── marketplace.json      # marketplace 清单
├── skills/                   # skills 源文件
│   ├── xd-blog-style/
│   └── xd-git-push/
└── docs/                     # 设计文档
```

## 使用方式

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

## Skills

| Skill | 描述 |
|-------|------|
| `xd-git-push` | 提交代码前二次确认 |
| `xd-blog-style` | 基于博客风格写作 |