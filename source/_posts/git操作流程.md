---
title: git操作流程
top: false
cover: false
toc: true
mathjax: true
date: 2021-06-01 22:43:53
password:
summary:
tags: [Git,编辑器]
categories: git
---

先学一下git命令的含义,判断什么情况下使用

> 前置条件已安装好git环境,并有远程仓库

1. 先拉取指定远程仓库别人的提交`git fetch teamds`

2. 合并`git rebase teamds/main`

   <img src="https://ali.frist-art.cn/wx/tianyan/photo/image-20210723140007775.png" alt="image-20210723140007775" style="zoom:67%;" />

   - 出现冲突,按照提示进入产生冲突的文件中,手动判断并解决冲突

     > 当 rebase 发生冲突时，git 会停止 rebase 并让你去解决冲突，**解决完之后不能直接 commit**，**而是应该用 continue 参数继续执行 rebase**
     >
     > ```
     > # 解决冲突之后
     > # 如果是合并代码时产生的冲突，需要把修改的文件放入暂存区
     > git add <冲突的文件>
     > git rebase --continue
     > # or
     > # 不解决冲突，还原回 rebase 之前的状态
     > git rebase --abort
     > ```

3. 查看当前git所管理的文档的状态`git status`   

   - 当工作树清除时 ,此时可以提交`git push`操作，工作树干净的时候没有红绿颜色。

     ![image-20210723121532675](https://ali.frist-art.cn/wx/tianyan/photo/image-20210723121532675.png)

4. 将所有的变更提交到git本地仓库的暂存区`git add -A`
   如图所示![image-20210723123230945](https://ali.frist-art.cn/wx/tianyan/photo/image-20210723123230945.png)

5. 将添加到暂存区的内容提交`git commit -m "docs:提交723log"`,

   > ​	git commit 主要是将暂存区里的改动给提交到本地的版本库。每次使用git commit 命令我们都会在本地版本库生成一个40位的哈希值，这个哈希值也叫commit-id，
   > ​	commit-id在版本回退的时候是非常有用的，它相当于一个快照,可以在未来的任何时候通过与git reset的组合命令回到这里.

   - 提交的内容添加一段描述信息` -m "docs:提交723log"` 

   - 仅有一个commit提交的情况,可以直接`git push <仓库源别名>/<分支名>`
     ![image-20210723123617169](https://ali.frist-art.cn/wx/tianyan/photo/image-20210723123617169.png)

   - 如果本地有多个`commit`提交一定要在本地合并,

     - 查看远程和本地的log`git log --oneline --decorate --graph --all` ![image-20210723132026382](https://ali.frist-art.cn/wx/tianyan/photo/image-20210723132026382.png)

     - 退出查看log模式,在底部输入字母`q`![image-20210723132312106](https://ali.frist-art.cn/wx/tianyan/photo/image-20210723132312106.png)

     - 合并多个commit`git rebase -i HEAD~3`,看上面的log信息提示有3个commit,那么后面`HEAD~`的数字就是3,依次类推![image-20210723132906415](https://ali.frist-art.cn/wx/tianyan/photo/image-20210723132906415.png)![image-20210723132935765](https://ali.frist-art.cn/wx/tianyan/photo/image-20210723132935765.png)

     - 输入字母`i`,修改内容![image-20210723133110326](https://ali.frist-art.cn/wx/tianyan/photo/image-20210723133110326.png)

     - 合并多个commit操作以及保存退出输入`:wq`![image-20210723133625872](https://ali.frist-art.cn/wx/tianyan/photo/image-20210723133625872.png)

     - 合并的提示信息,输出合并后的描述信息,退出并保存`:wq`![image-20210723133756341](C:\Users\58387\AppData\Roaming\Typora\typora-user-images\image-20210723133756341.png)

     - 再次查看log输入`git log --oneline --decorate --graph --all`![image-20210723134928321](https://ali.frist-art.cn/wx/tianyan/photo/image-20210723134928321.png)

6.将提交的版本推送到远程仓库`git push forkds le`

> `git push forkds le`中的forkds是仓库的别名,le是仓库的分支,

![image-20210723135444133](https://ali.frist-art.cn/wx/tianyan/photo/image-20210723135444133.png)



### 简约的操作流程

```
0.查看git状态
	git status
    如果本地有修改跳到第1步，
    如果本地没有任何更改跳到第4步做到第6步。
1.添加暂存区
	git add -A
2.提交版本
	git commit -m "docs:99"
3.查看log
	git log --oneline --decorate --graph --all
	自行判断是否存在多个commit提交,多个需要合并
	git rebase -i HEAD~<合并的提交数量>
	详情参考上面的第5条步骤中多个commit的情况
4.拉取远程
	git fetch teamds
5.合并
	git rebase teamds/main
	> 出现冲突时当 rebase 发生冲突时，git 会停止 rebase 并让你去解决冲突，解决完之后不能直		接 commit，而是应该用 continue 参数继续执行 rebase
	> 解决冲突之后
	  如果是合并代码时产生的冲突，需要把修改的文件放入暂存区
      git add <冲突的文件>
      git rebase --continue
      
6.查看状态
	git status
7.推送
	git push forkds/99 -f
8.发起PR--不需要99操作,99推送完在群里讲一下,茂宏和兔兔看到会合并,合并完后按照完整流程步骤走
```

