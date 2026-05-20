# xd-self-market

个人 AI 工具集归档仓库。

## 结构

- `.claude-plugin/marketplace.json` — marketplace 清单
- `plugins/` — 插件目录（唯一真实源）
- `docs/plugin-guide.md` — 新增插件规范

## 原则

1. `plugins/` 是唯一真实源
2. 通过 `extraKnownMarketplaces` 加载

## 新增插件

按照 `docs/plugin-guide.md` 规范进行，参考 `plugins/example/` 示例。