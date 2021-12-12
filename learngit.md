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

