---
name: example
description: 示例 skill。当需要创建新 skill 时，参考此文件的格式和结构。
---

# Example Skill

这是一个示例 skill，用于展示 Skill 组件的完整格式。

## 使用场景

当你需要添加新的 skill 到此插件时，可以参考此格式：
- 文件路径：`plugins/<plugin-name>/skills/<skill-name>/SKILL.md`
- frontmatter 必须包含 `name` 和 `description`

## Skill 格式说明

```yaml
---
name: <skill-name>           # 必须：skill 标识符
description: <描述>          # 必须：AI 判断何时调用此 skill
license: MIT                # 可选
tags: []                    # 可选：标签数组
---

# Skill 标题

## Overview
（技能概述）

## 使用方法
（详细的使用步骤）

## 注意事项
（使用时的注意点）
```

## 示例内容

此 skill 展示了如何编写一个用于格式化代码的 skill。

### 工作流程

1. 分析代码结构
2. 应用格式化规则
3. 输出格式化后的代码

### 注意事项

- 仅格式化，不改变逻辑
- 保持代码风格一致性