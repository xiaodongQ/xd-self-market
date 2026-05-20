# Claude Code Plugin / Marketplace 新增插件参考规范

> 本文档为 AI 添加新插件时的参考规范。添加新插件前请先阅读 `plugins/example/` 示例。

## 完整插件布局

```
plugin-name/
├── .claude-plugin/           # 元数据目录
│   └── plugin.json             # plugin 清单
├── skills/                   # Skills
│   └── <skill-name>/
│       └── SKILL.md
├── commands/                 # 平面 .md 文件作为 slash 命令
│   └── <name>.md
├── agents/                   # Subagent 定义
│   └── <name>.md
├── hooks/                    # Hook 配置
│   └── hooks.json
├── output-styles/            # 输出样式定义
├── themes/                   # 颜色主题定义
├── monitors/                 # 后台 monitor 配置
│   └── monitors.json
├── bin/                      # 添加到 PATH 的可执行文件
├── scripts/                  # Hook 和实用脚本
├── settings.json            # plugin 默认设置
├── .mcp.json                # MCP server 定义
├── .lsp.json                # LSP server 配置
├── LICENSE                  # 许可证文件
└── README.md                # 插件说明
```

## plugin.json 完整架构

```json
{
  "name": "plugin-name",
  "displayName": "Plugin Name",
  "version": "1.2.0",
  "description": "Brief plugin description",
  "author": {
    "name": "Author Name",
    "email": "author@example.com",
    "url": "https://github.com/author"
  },
  "homepage": "https://docs.example.com/plugin",
  "repository": "https://github.com/author/plugin",
  "license": "MIT",
  "keywords": ["keyword1", "keyword2"],
  "skills": "./skills/",
  "commands": "./commands/",
  "agents": "./agents/",
  "hooks": "./hooks/hooks.json",
  "mcpServers": "./.mcp.json",
  "outputStyles": "./output-styles/",
  "lspServers": "./.lsp.json",
  "experimental": {
    "themes": "./themes/",
    "monitors": "./monitors.json"
  },
  "dependencies": [
    "helper-lib",
    { "name": "secrets-vault", "version": "~2.1.0" }
  ]
}
```

**必填字段：** `name`

**常用可选字段：**

| 字段 | 类型 | 描述 |
|------|------|------|
| `displayName` | string | UI 中显示的人类可读名称 |
| `version` | string | 语义版本，固定到此版本 |
| `description` | string | plugin 目的的简要说明 |
| `author` | object | 作者信息 `{name, email?, url?}` |
| `homepage` | string | 文档 URL |
| `repository` | string | 源代码 URL |
| `license` | string | SPDX 许可证标识符 |
| `keywords` | array | 发现标签 |
| `skills` | string\|array | 自定义 skill 目录路径 |
| `commands` | string\|array | 自定义命令文件/目录 |
| `agents` | string\|array | 自定义 agent 文件 |
| `hooks` | string\|array\|object | Hook 配置路径或内联配置 |
| `mcpServers` | string\|array\|object | MCP 配置 |
| `lspServers` | string\|array\|object | LSP 配置 |

## 新增插件流程

### Step 1：确定插件名称

- 使用 **kebab-case**（全小写，单词用连字符分隔）
- 示例：`xd-blog-style`、`prompt-optimizer`、`code-reviewer`
- 禁止使用：空格、大写字母、特殊字符

### Step 2：创建目录结构

```bash
mkdir -p plugins/<plugin-name>/.claude-plugin
mkdir -p plugins/<plugin-name>/skills/<skill-name>
```

### Step 3：编写 plugin.json

路径：`plugins/<plugin-name>/.claude-plugin/plugin.json`

```json
{
  "name": "xd-example",
  "displayName": "xd-example",
  "description": "插件简短描述",
  "author": {
    "name": "xiaodongq",
    "url": "https://github.com/xiaodongq"
  },
  "version": "1.0.0",
  "homepage": "https://github.com/xiaodongq/xd-self-market",
  "repository": "https://github.com/xiaodongq/xd-self-market",
  "license": "MIT",
  "keywords": ["example"],
  "skills": "./skills/",
  "commands": "./commands/",
  "agents": "./agents/",
  "hooks": "./hooks/hooks.json"
}
```

### Step 4：添加组件

#### Skill（技能）

**格式：** `plugins/<name>/skills/<skill-name>/SKILL.md`

```markdown
---
name: <skill-name>
description: 一句话描述技能用途（AI 判断何时调用）
license: MIT
---

# Skill 标题

## Overview
（技能概述）

## 工作流程
（详细的工作步骤）

## 注意事项
（使用时的注意点）
```

#### Command（命令）

**格式：** `plugins/<name>/commands/<command-name>.md`

```markdown
---
name: <plugin-name>:<command-name>
description: 命令的简短描述
---

# Command Title

## 说明
（命令功能描述）

## 参数
- `param1`：参数说明

## 示例输出
```
输出示例
```
```

#### Agent（代理）

**格式：** `plugins/<name>/agents/<agent-name>.md`

```markdown
---
name: <agent-name>
description: agent 的职责描述
model: sonnet
effort: medium
maxTurns: 20
tools:
  - Read
  - Write
  - Bash
---

# Agent Title

## 职责
（agent 的主要职责）

## 行为规范
（具体的行为指南）
```

#### Hook（钩子）

**格式：** `plugins/<name>/hooks/hooks.json`

```json
{
  "hooks": [
    {
      "name": "hook-name",
      "description": "钩子描述",
      "events": ["PreCommit", "PostToolUse"],
      "matcher": "Write|Edit",
      "action": {
        "type": "command",
        "command": "${CLAUDE_PLUGIN_ROOT}/scripts/check.sh"
      }
    }
  ]
}
```

**events 可选值：** `SessionStart`, `UserPromptSubmit`, `PreToolUse`, `PostToolUse`, `Stop`, `SessionEnd` 等

**action.type：** `command`, `http`, `mcp_tool`, `prompt`, `agent`

### Step 5：更新 marketplace.json

路径：`.claude-plugin/marketplace.json`

在 `plugins` 数组中添加新条目：

```json
{
  "name": "xd-self-market",
  "plugins": [
    {
      "name": "<新插件名>",
      "description": "简短描述",
      "source": "./plugins/<新插件名>",
      "version": "1.0.0",
      "author": { "name": "xiaodongq" }
    }
  ]
}
```

### Step 6：验证

```bash
claude plugin validate .
/plugin install <plugin-name>@xd-self-market
/reload-plugins
```

## 组件路径字段说明

| 字段 | 类型 | 说明 |
|------|------|------|
| `skills` | string\|array | 自定义 skill 目录，添加到默认 `skills/` |
| `commands` | string\|array | 替换默认 `commands/` 目录 |
| `agents` | string\|array | 替换默认 `agents/` 目录 |
| `hooks` | string\|array\|object | 合并到默认 hooks |
| `mcpServers` | string\|array\|object | 合并到默认 MCP servers |
| `lspServers` | string\|array\|object | 替换默认 LSP 配置 |

## 环境变量

| 变量 | 说明 |
|------|------|
| `${CLAUDE_PLUGIN_ROOT}` | plugin 安装目录绝对路径 |
| `${CLAUDE_PLUGIN_DATA}` | 持久化数据目录（版本间保留） |
| `${CLAUDE_PROJECT_DIR}` | 项目根目录 |

## 常见问题

### Q: 需要创建 `.claude-plugin/plugin.json` 吗？

**A:** 可选。省略时 Claude Code 自动发现默认位置组件，从目录名派生 plugin 名称。

### Q: source 相对路径相对于哪里？

**A:** 相对于 marketplace 根目录（包含 `.claude-plugin/` 的目录）。

### Q: 如何选择 Skill/Command/Agent？

| 类型 | 调用方式 | 适用场景 |
|------|----------|----------|
| Skill | AI 自动判断 | 根据上下文自动使用 |
| Command | 用户手动 `/plugin:command` | 明确操作 |
| Agent | 子 agent 调用 | 长任务独立上下文 |

## 参考资料

- [Plugins 参考](https://code.claude.com/docs/zh-CN/plugins-reference)
- [Skills](https://code.claude.com/docs/zh-CN/skills)
- [Subagents](https://code.claude.com/docs/zh-CN/sub-agents)
- [Hooks](https://code.claude.com/docs/zh-CN/hooks)