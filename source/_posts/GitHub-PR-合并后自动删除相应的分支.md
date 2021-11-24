---
title: GitHub PR 合并后自动删除相应的分支
top: false
cover: false
toc: true
mathjax: true
date: 2021-05-26 16:20:54
password:
summary:
tags: [git，github]
categories: git
---
# GitHub PR 合并后自动删除相应的分支

GitHub 默认不会删除和 PR 关连的 remote 分支，久而久之，随着 PR 的数量的增加，remote 分支也越来越多。合并后的 PR 相关的修改内容在 GitHub 面板里能够查看到，所以即使删除了和 PR 相关的分支也没有太大影响，但是这样对整个工作流来说就增加了一步额外的操作。

有两种手动删除 GitHub remote 分支的方式：

1. GitHub branches 页面可以删除 remote 分支，删除后 local 的 remote branch 缓存需要手动清理一下

   ```
   git remote prune <remote-name>
   ```

2. 命令行删除 remote 分支

   ```
   git push origin :<branch-name>
   ```

   如果需要清理 local 的 remote branch 缓存，同上

   ## 自动删除 remote 分支

   拥有仓库管理员权限的用户可以配置 PR 合并后自动删除相应的分支。

   1. 打开仓库主页面
   2. 打开 **Settings**
   3. 在 **Merge button** 下面，勾选 **Automatically delete head branches**

   ## 参考

   - [Managing the automatic deletion of branches](https://help.github.com/en/github/administering-a-repository/managing-the-automatic-deletion-of-branches), GitHub