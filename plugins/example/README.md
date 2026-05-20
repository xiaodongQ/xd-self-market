# Example Plugin

示例插件，包含所有组件类型的参考实现，供 AI 添加新插件时参考。

## 完整结构

```
example/
├── .claude-plugin/
│   └── plugin.json          # plugin 清单（完整字段）
├── skills/
│   └── example/
│       └── SKILL.md          # Skill 示例
├── commands/
│   └── example.md            # Command 示例
├── agents/
│   └── example.md            # Agent 示例
├── hooks/
│   └── hooks.json            # Hook 配置示例
└── README.md                 # 本文件
```

## 组件类型

| 类型 | 路径 | 说明 |
|------|------|------|
| Skill | `skills/example/SKILL.md` | 带 frontmatter 的 Markdown |
| Command | `commands/example.md` | 平面 Markdown 作为 slash 命令 |
| Agent | `agents/example.md` | 自定义 agent 定义 |
| Hook | `hooks/hooks.json` | 事件处理程序配置 |

## plugin.json 示例

```json
{
  "name": "example",
  "displayName": "Example Plugin",
  "description": "示例插件，包含所有组件类型的参考实现",
  "author": {
    "name": "xiaodongq",
    "url": "https://github.com/xiaodongq"
  },
  "version": "1.0.0",
  "skills": "./skills/",
  "commands": "./commands/",
  "agents": "./agents/",
  "hooks": "./hooks/hooks.json"
}
```

## 验证

```bash
claude plugin validate .
/plugin install example@xd-self-market
```