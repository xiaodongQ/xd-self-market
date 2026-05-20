---
name: example:hello
description: 示例命令。当用户输入 /example:hello 时触发，展示命令的格式。
---

# Hello Command

这是一个示例命令（Command），用于展示 slash 命令的格式。

## 使用方法

用户输入 `/example:hello [名字]` 时触发。

## 命令格式

```yaml
---
name: <command-name>    # 命令名称，用于 slash 调用
description: <描述>     # 命令的简短描述
---

# 命令标题

## 说明
（命令的功能描述）

## 参数
- `name`：可选参数，指定问候对象

## 示例输出

```
Hello, [name]! 欢迎使用 example 插件。
```