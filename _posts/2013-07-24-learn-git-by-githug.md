---
layout: post
title: "Githug通关攻略"
categories: tech
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

**Level 13** 查看提交历史

    git log

我输入的`git show`也可以看到。

**Level 14** 给当前repo加标签

    git tag new_tag

其他用法：

- `git tag tagname 1b2e1d63ff`：为指定的commit打tag


**Level 15** 修改最后一次提交

    git status
    git add forgotten_file.rb
    git commit --amend -m "add forgotten_file"

amend选项提供了最后一次commit的反悔机会，但是如果最后一次提交已经push过了，那么就不能修改了。对于历史提交，只能使用rebase了。

**Level 16** 将文件从暂存区删除

    git status
    git reset HEAD to_commit_second.rb

`git reset HEAD <file>`命令可以将文件从暂存区删除，经过我测试并不会修改工作区，网上有些文章信息错误。

`git reset [--hard|soft|mixed|merge|keep] [<commit>或HEAD]`命令有好几种模式：

- `--hard`：重设`暂存区`和`工作区`；
- `--soft`：`暂存区`和`工作区`内容不做改变，仅仅把`HEAD`指向`<commit>`，执行效果是，自从`<commit>`以来的所有改变都放入`暂存区`，相当于撤销commit；
- `--mixed`：这个是默认模式。仅重设`暂存区`，不会修改`工作区`；
- `--merge`和`--keep`暂未研究。

reset命令用法刚开始理解起来有点绕，我又找了一个解释：

- reset命令把当前分支指向另一个位置，并且有选择的变动工作区和暂存区。也用来在从历史仓库中复制文件到暂存区，而不动工作区。
- 如果不给选项，那么当前分支指向到那个提交。
- 如果用--hard选项，那么工作目录也更新。
- 如果用--soft选项，那么都不变。
- 如果不给提交号，那么默认用HEAD。例如，`git reset`等价于`git reset --mixed HEAD`。
- 如果给了文件名，效果和带文件名的checkout差不多，除了索引被更新。例如`git reset -- files`。


**Level 17** 撤销最后一次提交，保留当前暂存区不变

    git log
    git reset --soft HEAD~1

或者`git reset --soft HEAD^`，尼玛，HEAD后面加一个`^`符号是啥意思我咋没找到！

**Level 18** 撤销工作区文件的修改

    git checkout -- config.rb

尼玛，checkout命令后面加两个`--`是啥意思？

**Level 19** 查看远程repo名称

    git remote -v

可知远程repo名称为`my_remote_repo`。
	
其他用法：

查看remote url：

    git remote -v

设置remote url：

    git remote set-url origin https://github.com/user/repo2.git

git中配置参数：

    git config user.name xxx
    git config user.email xxx@xxx.com

git中获取参数值：

    git config --get user.name
    git config --get user.email

**Level 20** 查看远程repo URL

    git remote -v

**Level 21** 从远程repo中pull代码

这题有bug吧？输入`git remote -v`发现没有设置URL啊！坑爹啊，如何PULL？我只好去看了下githug此关的源代码，找到这个URL手工设置了一把：

    git remote set-url origin https://github.com/pull-this/thing-to-pull

如此一来即可pull了：

    git pull origin master

搞定！

**Level 22** 设置Remote URL

    git remote set-url origin https://github.com/githug/githug

或者

    git remote add origin https://github.com/githug/githug

**Level 23** rebase

劳资用的这githug是不是有问题啊，为毛又没有remote url！这让人怎么搞！

git rebase相关用法：

    git rebase origin
    git rebase origin/master

如果rebase的过程中有冲突，git会停止rebase并让你解决冲突，解决冲突完成后，用`git add`命令去更新暂存区，然后无需执行`git commit`，只要执行：

    git rebase --continue

如果要放弃rebase，执行：

    git rebase --abort

参考这篇[“git rebase”](http://gitbook.liuhui998.com/4_2.html)，写得比较清楚。


----

参考文献：

- 图解Git： <http://marklodato.github.io/visual-git-guide/index-zh-cn.html>
- Githug通关全攻略： <http://fancyoung.com/blog/githug-cheat-sheet/>
- Git Community Book：<http://gitbook.liuhui998.com/index.html>