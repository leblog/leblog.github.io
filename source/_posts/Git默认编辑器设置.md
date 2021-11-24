---
title: Git默认编辑器设置
top: false
cover: false
toc: true
mathjax: true
date: 2021-07-30 22:41:23
password:
summary:
tags: [Git,编辑器]
categories: git
---

## 将Git的默认编辑器设置为VS Code

windows用户运行git bash并输入以下代码

```
git config --global core.editor "code -w"
```

操作步骤

```
1.`git reabse -i HEAD~2`合并多个提交时,会默认打开Vscode,
2.修改内容并保存,然后关闭
3.git会继续打开更改后的内容,无需修改,直接关闭就好了
```

