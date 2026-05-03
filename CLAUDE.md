# xd-self-market

个人 AI 工具集归档仓库，支持 Claude Code marketplace 加载。

## 结构

- `.claude-plugin/` — marketplace 元数据（marketplace.json）
- `skills/` — 统一源格式（Claude Code SKILL.md）
- `docs/superpowers/specs/` — 设计文档

## 原则

1. `skills/` 是唯一真实源
2. 通过 `extraKnownMarketplaces` 加载本仓库
3. 设计文档保存在 `docs/superpowers/specs/`
