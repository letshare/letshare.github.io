title: git简易使用指南2
date: 2013-7-14 19:20:00
categories: 工具
tags: ['git','版本']
---

##命令详解

###git remote 
`git remote`用于管理远程仓库
```bash
$ git remote add <name> <url>
#添加一个远程仓库
#添加后就可以使用git fetch 或git pull从远程仓库获取代码

$git remote -v
#查看本地配置了哪些远程仓库

$git remote show <name>
#查看远程仓库的详细信息
```

###git clone
`git clone <url> [path]`克隆一个远程仓库到本地，这条命令其实是由多条命令组成的。与下面等效
```bash
$ mkdir path && cd path
$ git init      #初始化一个本地仓库
$ git remote add origin <url>
$ git pull
```
##子树合并
在项目中难免会引用到其他项目作为主项目的一个模块，但不能同时存在两个仓库，然后都提交。有一个解决文档是，将子项目作为子树提交，新建立一个分支作为子项目，然后跟踪更新。然后切换回主分支，主分支合并读取分支的树，这时在子目录下会有子项目的文件，子项目和主分支的更新和合并都通过子树作为桥梁。

子树归并的思想是你拥有两个工程，其中一个项目映射到另外一个项目的子目录中，反过来也一样。当你指定一个子树归并，Git可以聪明地探知其中一个是另外一个的子树从而实现正确的归并——这相当神奇。

比如想要嵌入一个rack项目。首先你将 Rack 项目加入到项目中。你将 Rack 项目当作你项目中的一个远程引用，然后将它检出到它自身的分支：
```bash
$ git remote add rack_remote git@github.com:schacon/rack.git
$ git fetch rack_remote
$ git checkout -b rack_branch rack_remote/master
```

要将 Rack 项目当作子目录拉取到你的master项目中。你可以在 Git 中用git read-tree来实现。
```bash
$ git checkout master
$ git read-tree --prefix=rack/ -u rack_branch
```

当你提交master的时候，会同时提交子目录下拥有Rack的文件。你可以比较容易地归并其中一个分支的变更到另外一个。因此，如果 Rack项目更新了，你可以通过切换到那个分支并执行拉取来获得上游的变更。然后又可以切换会主分支，合并那个分支的修改。
```bash
$ git checkout rack_branch
$ git pull
$ git checkout master
$ git merge --squash -s subtree --no-commit rack_branch
Squash commit -- not updating HEAD
Automatic merge went well; stopped before committing as requested
```

为了得到rack子目录和你rack_branch分支的区别——以决定你是否需要归并它们——你不能使用一般的diff命令。而是对你想比较的分支运行git diff-tree：
```bash
$ git diff-tree -p rack_branch
```


##think in git
###git 对象
Git 是一套内容寻址文件系统。Git 从核心上来看不过是简单地存储键值对（key-value）。它允许插入任意类型的内容，并会返回一个键值，通过该键值可以在任何时候再取出该内容。

##参考
+ [https://help.github.com](https://help.github.com/)
+ [git简明教程](http://www.bootcss.com/p/git-guide/)
+ [git图解](http://marklodato.github.io/visual-git-guide/index-zh-cn.html)
+ [git手册](http://git-scm.com/docs/)
+ [git中文手册](http://git-scm.com/book/zh/)