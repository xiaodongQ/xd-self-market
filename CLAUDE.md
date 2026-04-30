# xd-self-market

个人 AI 工具集归档仓库，支持 Claude Code 和 OpenClaw。

## 结构

- `skills/` — 统一源格式（Claude Code SKILL.md）
- `openclaw/` — OpenClaw 兼容副本（.SKILL.md 格式）
- `commands/` — slash commands 定义
- `mcps/` — MCP server 配置
- `scripts/` — 公共脚本

## 原则

1. `skills/` 是唯一真实源，OpenClaw 副本由脚本同步或手动维护
2. 迁移时使用拷贝，不修改原始文件
