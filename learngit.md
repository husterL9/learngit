## 1.add,commit,status,diff

- 要明白这3个概念，工作区（**working tree**），暂存区（**index /stage**），本地仓库（**repository**）
- git跟不同的参数，比较不同的区间的版本。
1. git diff：是查看working tree与index的差别的。
2. git diff --cached：是查看index与repository的差别的。
3. git diff HEAD：是查看working tree和repository的差别的。其中：HEAD代表的是最近的一次commit的信息。

### git add learngit.md出现问题

在工作目录中，我们可以通过设置eol属性控制一个文件的行尾为CRLF或LF。我们也可以通过设置core.eol属性控制当前Git库中的所有文件的行尾为CRLF或LF。我们还可以设置core.autocrlf属性以覆盖core.eol属性的设置。如果要设置工作目录中的文件的行尾总是CRLF，而Git库中的文件的行尾总是LF，可以core.autocrlf=true。

1. 查看core.autocrlf属性

默认core.autocrlf属性设置如下。

C:\Sam\works\bba-master>git config --global --get core.autocrlf

C:\Sam\works\bba-master>git config --get core.autocrlf
true

2. 设置core.autocrlf属性
   设置core.autocrlf属性为false，去除警告如下（只是眼不见心不烦罢了）。

C:\Sam\works\bba-master>git config core.autocrlf false

C:\Sam\works\bba-master>git config --get core.autocrlf
false

C:\Sam\works\bba-master>git add mywebdav.conf

## 2.remote add origin,push

把本地库的内容推送到远程，用`git push`命令，实际上是把当前分支`master`推送到远程。

由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。

## 3.branch

Git鼓励大量使用分支：

查看分支：`git branch`

创建分支：`git branch <name>`

切换分支：`git checkout <name>`或者`git switch <name>`

创建+切换分支：`git checkout -b <name>`或者`git switch -c <name>`

合并某分支到当前分支：`git merge <name>`

删除分支：`git branch -d <name>`

准备合并`dev`分支，请注意`--no-ff`参数，表示禁用`Fast forward`：

```
$ git merge --no-ff -m "merge with no-ff" dev
```

```
git log --graph --pretty=oneline --abbrev-commit
```

```
$ git pull
Auto-merging env.txt
CONFLICT (add/add): Merge conflict in env.txt
Automatic merge failed; fix conflicts and then commit the result.
```

这回`git pull`成功，但是合并有冲突，需要手动解决，解决的方法和分支管理中的[解决冲突](http://www.liaoxuefeng.com/wiki/896043488029600/900004111093344)完全一样。解决后，提交，再push：

```
$ git commit -m "fix env conflict"
[dev 57c53ab] fix env conflict

$ git push origin dev
Counting objects: 6, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 621 bytes | 621.00 KiB/s, done.
Total 6 (delta 0), reused 0 (delta 0)
To github.com:michaelliao/learngit.git
   7a5e5dd..57c53ab  dev -> dev
```

现在，你的小伙伴要在`dev`分支上开发，就必须创建远程`origin`的`dev`分支到本地，于是他用这个命令创建本地`dev`分支：

```
$ git checkout -b dev origin/dev
```

现在，他就可以在`dev`上继续修改，然后，时不时地把`dev`分支`push`到远程：

```
$ git add env.txt

$ git commit -m "add env"
[dev 7a5e5dd] add env
 1 file changed, 1 insertion(+)
 create mode 100644 env.txt

$ git push origin dev
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 308 bytes | 308.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To github.com:michaelliao/learngit.git
   f52c633..7a5e5dd  dev -> dev
```

## fork 了别人的仓库后，原作者又更新了仓库，如何将自己的代码和原仓库保持一致？

[同步一个 fork](https://gaohaoyang.github.io/2015/04/12/Syncing-a-fork/)

`git fetch upstream` `git merge upstream/master` 如果想更新到 GitHub 的 fork 上，直接 `git push origin master` 就好了。

## fork与pull request

| fork         | https://github.com/oldratlee/translations/blob/master/git-workflows-and-tutorials/workflow-forking.md#-%E5%B7%A5%E4%BD%9C%E6%96%B9%E5%BC%8F |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------- |
| pull-request | https://github.com/oldratlee/translations/blob/master/git-workflows-and-tutorials/pull-request.md                                           |
|              |                                                                                                                                             |
|              |                                                                                                                                             |

## 可参考资料

| git权威指南 | http://www.worldhello.net/gotgit/index.html |
| ------- | ------------------------------------------- |
|         |                                             |
|         |                                             |
|         |                                             |

# Git提供了一个命令`git reflog`用来记录你的每一次命令

![](D:\SE2\deep_learning\learngit\imgs\z99.png)

# 添加到远程库



关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；
