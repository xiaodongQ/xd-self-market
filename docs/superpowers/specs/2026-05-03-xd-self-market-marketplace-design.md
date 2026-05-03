# xd-self-market Marketplace 规范化方案

2026-05-03

## 目标

将 xd-self-market 重建为符合 Claude Code marketplace 规范的仓库，可通过 `extraKnownMarketplaces` 加载。

## 当前问题

| 问题 | 状态 |
|------|------|
| 根目录缺少 `.claude-plugin/marketplace.json` | 缺失 |
| `skills/xd-git-push/` 缺少 `.claude-plugin/plugin.json` | 缺失 |
| `skills/xd-blog-style/.claude-plugin/plugin.json` | 字段不完整 |

## 目标结构

```
xd-self-market/
├── .claude-plugin/
│   └── marketplace.json          # NEW
├── skills/
│   ├── xd-blog-style/
│   │   ├── .claude-plugin/
│   │   │   └── plugin.json       # 补全 version
│   │   └── SKILL.md
│   └── xd-git-push/
│       ├── .claude-plugin/      # NEW
│       │   └── plugin.json       # NEW
│       └── SKILL.md
├── CLAUDE.md
└── README.md
```

## 操作步骤

### 1. 创建根目录 marketplace.json

创建 `.claude-plugin/marketplace.json`：

```json
{
  "name": "xd-self-market",
  "description": "个人 AI 工具集归档仓库 — skills 和工具集合",
  "owner": { "name": "xiaodongq" },
  "plugins": [
    {
      "name": "xd-blog-style",
      "description": "基于 xiaodongq 博客风格写作的 skill",
      "source": {
        "source": "directory",
        "path": "skills/xd-blog-style"
      }
    },
    {
      "name": "xd-git-push",
      "description": "提交代码到远程仓库前与用户二次确认",
      "source": {
        "source": "directory",
        "path": "skills/xd-git-push"
      }
    }
  ]
}
```

### 2. 补全 xd-blog-style plugin.json

路径：`skills/xd-blog-style/.claude-plugin/plugin.json`

在现有基础上补全 version 字段：

```json
{
  "name": "xd-blog-style",
  "description": "基于 xiaodongq 博客风格写作的 skill",
  "author": { "name": "xiaodongq" },
  "version": "1.0.0"
}
```

### 3. 新建 xd-git-push plugin.json

路径：`skills/xd-git-push/.claude-plugin/plugin.json`

```json
{
  "name": "xd-git-push",
  "description": "提交代码到远程仓库前与用户二次确认",
  "author": { "name": "xiaodongq" },
  "version": "1.0.0"
}
```

### 4. 删除归档目录

删除以下与 marketplace 无关的内容：

- `openclaw/` — OpenClaw 兼容副本
- `commands/` — slash commands
- `mcps/` — MCP server 配置
- `scripts/` — 公共脚本
- `SKILL.md` — 仓库级说明（冗余）

### 5. 更新 CLAUDE.md

更新结构说明，移除已删除的目录。

## 验证方式

```bash
# 检查 marketplace.json 存在
ls -la .claude-plugin/marketplace.json

# 检查 plugin.json 存在
ls -la skills/xd-blog-style/.claude-plugin/plugin.json
ls -la skills/xd-git-push/.claude-plugin/plugin.json

# marketplace 加载测试（Claude Code 中）
/plugin marketplace add <path-to-xd-self-market>
```