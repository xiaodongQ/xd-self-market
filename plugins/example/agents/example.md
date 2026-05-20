---
name: example-agent
description: 示例 agent。当需要处理特定任务时作为子 agent 调用。
---

# Example Agent

这是一个示例 agent，用于展示自定义 agent 的格式。

## Agent 格式说明

```yaml
---
name: <agent-name>      # agent 标识符
description: <描述>     # agent 的职责描述
model: claude-sonnet-4-6  # 可选：指定模型
tools:                  # 可选：限制可用工具
  - Read
  - Edit
  - Bash
---

# Agent 标题

## 职责
（agent 的主要职责）

## 行为规范
（具体的行为指南）

## 输出格式
（期望的输出格式）
```

## 示例内容

此 agent 用于处理日常文档整理任务。

### 职责

- 整理文档结构
- 修正格式问题
- 生成目录

### 行为规范

1. 先阅读文档内容
2. 分析结构问题
3. 提出改进建议
4. 执行整理操作

### 输出格式

整理完成后，输出：
- 发现的问题列表
- 已做的修改列表
- 建议的后续操作