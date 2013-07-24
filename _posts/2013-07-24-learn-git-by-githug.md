---
layout: post
title: "Githug通关攻略"
categories:
tags: git
---

[Githug](https://github.com/Gazler/githug)是一个很棒的git学习工具，通过有趣的闯关游戏即可轻松学习各种常见的git命令。
推荐git学习者练手、巩固。

小Tip：如果想play指定的关卡，可以编辑`git_hug`目录下的`.profile.yml`文件，然后`githug reset`即可。

----

学习到的一些知识点：

1. git工作区是保存当前正在工作的文件，这个目录是一个临时目录，在切换branch时可能会被git删除或者替换。

2. 工作区、暂存区、版本库之间的关系参见这张图解：

    ![git-stage](http://www.worldhello.net/wpfiles/2010/11/git-stage.png)

3. git暂存区(叫Git Index或者Git Staging area)用于保存准备提交的改变。可通过`git status`命令查看什么内容在暂存区。

    - "Changes to be committed"中的内容是在暂存区中，可通过commit进入Git Directory；
    - "Changed but not updated"中的内容是在工作区中，可通过add进入暂存区；
    - "Untracked files"中的内容未被git跟踪，可通过add进入暂存区；

----

以下是我的闯关过程笔记：

**Level 7** 忽略某些类型的文件

修改.gitignore文件，添加*.swp

**Level 8** 查看状态

    git status   

可以看到database.yml文件是Untracked


**Level 9** 删除文件

    git status
    git rm deleteme.rb

**Level 10** 删除暂存区中的文件

    git rm --cached deleteme.rb

**Level 11** 备份当前工作区但不提交

这题折腾了很久，本来以为是要求把内容添加到暂存区，但是发现不对，原来是一个没用过的命令。

    git stash

`git stash`表示备份当前工作区的内容到git栈中，同时当前工作区恢复为最近一次提交。

其他相关用法：

- `git stash list`：查看git栈；
- `git stash pop`：把工作区恢复为git栈中最近一次保存(stash)的内容，对应的这条stash会在栈中清掉；
- `git stash clear`：清空git栈；
- `git stash apply stash@{1}`：把工作区恢复为指定的stash

**Level 12** 重命名文件

比较简便的方法：

    git mv oldfile.txt newfile.txt

我用的是笨方法：

    mv oldfile.txt newfile.txt
    git status
    git rm --cached oldfile.txt
    git add newfile.txt
