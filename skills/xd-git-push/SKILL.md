---
name: xd-git-push
description: Use when user asks to push code to a remote git repository and wants to confirm commit message and files before pushing
---

# xd-git-push

## Overview

提交代码到远程仓库前与用户二次确认：确认提交文件、提炼 commit message、确认目标仓库。

## 工作流程

### 1. 检查 git 状态

```sh
git status
git diff
git log --oneline -5
```

### 2. 确认仓库

- 如果当前目录是 git 仓库，直接使用
- 如果不知道哪个仓库，问用户："要推送到哪个仓库？"

### 3. 检查与远端同步状态

```sh
git fetch origin
git status
```

如果本地落后于远端，先执行 `git pull` 同步，再继续后续流程。

### 4. 确认提交文件及 commit message

展示 `git status` 结果和 `git diff`，列出待提交文件，并根据 diff 内容提炼 commit message，一并展示给用户确认：

> **待提交文件**：
> - `file1` (状态)
> - `file2` (状态)
>
> **Commit message**：
> `xxx`
>
> 确认吗？需要增减吗？

```sh
git add <files>
git commit -m "<message>"
git push
```

展示 push 结果确认成功。

## 注意事项

- commit message 用中文，聚焦"做了什么"而非"怎么做的"
- 如果有未跟踪的新文件，明确列出让用户确认是否一起提交
- push 失败时展示错误信息，询问如何处理
