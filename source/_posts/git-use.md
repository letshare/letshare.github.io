title: git简易使用指南
date: 2013-7-12 19:20:00
categories: 工具
tags: ['git','版本']
---

##安装
[下载 git OSX 版](http://code.google.com/p/git-osx-installer/downloads/list?can=3)

[下载 git Windows 版](http://code.google.com/p/msysgit/downloads/list?can=3)

[下载 git Linux 版](http://book.git-scm.com/2_installing_git.html)

##git基础
直接记录快照，而非差异比较

**文件的三种状态：**已提交（committed），已修改（modified）和已暂存（staged）。用git管理项目的时候，文件在三个地方流转：Git 的工作目录，暂存区域，以及本地仓库。
![git三种文件流转区](/images/201307/3spaces.jpg)

如果是 Git 目录中保存着的特定版本文件，就属于已提交状态；如果作了修改并已放入暂存区域，就属于已暂存状态；如果自上次取出后，作了修改但还没有放到暂存区域，就是已修改状态。


##常用命令
创建新仓库  `git init`

检出仓库   `git clone url`

添加修改 `git add <filename>`

提交修改  `git commit - "代码提交信息"`

连接远程  `git add remote <a name> <server>`

更新远程  `git pull`

合并远程  `git merge`

推送远程  `git push <server name> <branch>`

分支管理  `git checkout` 和 `git branch`

> 关于命令的用法，强烈推荐一个[简明教程](http://www.bootcss.com/p/git-guide/)，可以让你快速掌握日常的用法。

##命令详解
有些命令比较容易混淆，稍不注意就用错了。要特别注意那些命令对三个区域操作的方向性。

文件如何在三个区域流转呢？就要用到这几个命令git add commit reset checkout 
![文件流转](/images/201307/1step-operations.png)
> `--`参数的作用是区分分支名还是文件名，加了`--`参数命令就知道后面的是文件名而不是分支名
> `git add -A `将工作目录所有修改提交
> `git checkout -- files` 把文件从暂存区域复制到工作目录，用来丢弃本地修改。files不能少，不然会无效

上面的图是分步操作，也可以一条命令同时对暂存区和工作目录操作。
![文件流转2](/images/201307/2step-operations.png)


###git checkout
checkout命令用于分支切换及文件签回。切换的时候会进行HEAD跟分支绑定，如果是存在的分支，那么所有暂存区和工作目录的文件将会变成跟仓库一样，如果是新分支会匿名分支，文件不会变。如果分支后面还带有文件参数，则不会切换分支，只是把另一个分支的文件签过来。如果不带分支名，则是从暂存区签回文件。签回就是复制，不存在于两个当前分支仓库和要切换分支仓库的文件将不会改变。举三个例子：
```bash
$ git checkout master              #(1) 切换到分支master
$ git checkout master~2 Makefile   #(2) 并不切换到另一个分支，只是签回文件
$ rm -f hello.c
$ git checkout hello.c             #(3) 从暂存区签回hello.c
```
关于HEAD指针，它指向一个分支头部，比如如果指向分支master，`HEAD^`就是master的上一个版本， `HEAD^^ `上上个版本，`HEAD^100` 上100个版本。`HEAD~`相反对应的是master的下一个版本。

###git reset
reset命令把当前分支指向另一个位置，并且有选择的变动工作目录和暂存区。也用来在从历史仓库中复制文件到暂存区，而不动工作目录。

如果不给选项，那么当前分支指向到那个提交。如果用`--hard`选项，那么工作目录也更新，如果用`--soft`选项，那么都不变。
![git reset](/images/201307/git-reset.png)
如果没有给出提交点的版本号，那么默认用HEAD。这样，分支指向不变，但是索引会回滚到最后一次提交，如果用--hard选项，工作目录也同样。

###git merge
merge 命令把不同分支合并起来。合并前，索引必须和当前提交相同。作用是将仓库中其他分支的跟索引更新的地方，down到暂存区和工作目录中。

也就是说如果另一个分支是当前提交的祖父节点，那么合并命令将什么也不做，因为没有更新的内容，而如果当前提交是另一个分支的祖父节点，就导致fast-forward合并。指向只是简单的移动，工作目录和暂存区的文件会改变但并不会生成一个新的提交。

如果当前分支和另外一个分支有共同的祖先节点而不是直接线性节点关系的话，将会进行一个文件的合并，并创建一个新的提交。如果当前分支合并的时候出现了冲突了，只要重新编辑冲突的文件，在解决了所有文件里的所有冲突后，运行 git add 将把它们标记为已解决状态（实际上就是来一次快照保存到暂存区域。）。因为一旦暂存，就表示冲突已经解决。或者使用`git merge --abort`放弃合并，工作目录和暂存区会回退。
![git merge](/images/201307/true-merge.png)

###git cherry-pick
cherry-pick命令"复制"一个提交节点并在当前分支做一次完全一样的新提交。
![git cherry-pick](/images/201307/cherry-pick.png)

###git rebase
rebase衍合是合并命令的另一种选择。合并把两个父分支合并进行一次提交，提交历史不是线性的。衍合在当前分支上重演另一个分支的历史，提交历史是线性的。 本质上，这是线性化的自动的 cherry-pick。
![git rebase](/images/201307/git-rebase.png)

上面的命令都在topic分支中进行，而不是master分支，在master分支上重演，并且把分支指向新的节点。注意旧提交没有被引用，将被回收。要限制回滚范围，使用`--onto`选项。下面的命令在master分支上重演当前分支从169a6以来的最近几个提交，即2c33a。
![git rebase onto](/images/201307/rebase-onto.png)


###其他命令
`git rm file` 用于删除已提交到暂存区的文件，从此这个文件不会出现在版本管理。

`git mv file1 file2`用于工作目录和暂存区的文件更名，相当于执行了三个命令，
```bash
$ mv file1 file2
$ git rm file1
$ git add file2
```
`git status`,用于查看工作目录的状态

`git diff`,用于比较工作目录和暂存区

`git diff --staged`,用于比较暂存区和仓库


##参考
+ [https://help.github.com](https://help.github.com/)
+ [git简明教程](http://www.bootcss.com/p/git-guide/)
+ [git手册](http://git-scm.com/docs/)