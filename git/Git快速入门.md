# Git快速入门

## 1. 名词

- git
- github
- repository
- PR（pull request）
- issue
- add，commit，push，pull
- merge，fetch，rebase
- branch
- conflict

## 2. 操作

**准备工作**

1. [安装 **git** 客户端](git-scm.com)，下载下来的软件包括命令行界面的git bash和图形界面的git gui。一般我们都是使用git bash。
2. [创建**Github**账号](https://github.com/)。
3. 本机配置SSH，参考[廖雪峰的教程](https://www.liaoxuefeng.com/wiki/896043488029600/896954117292416)。教程中的指令可以在git bash中执行。过程分为两步：
   - 创建自己的SSH key
   - 将SSH key添加到自己的GitHub账号中

**创建仓库和提交PR**

1. fork

打开项目[LearningNotes](https://github.com/sspkusharing/LearningNotes)， 点击右上角的fork，会在你的github账号下创建一个同名的复刻仓库。你的github账号下的复刻仓库被称为远程仓库（origin），被你fork的这个仓库被称为主仓库（upstream）。

2. clone

进入f在你的账号下生成的远程仓库，在右上角的Code处复制SSH地址(git@开头，注意不要选成https地址)，在本地你需要建立本地仓库的目录下，使用git bash执行指令：

```
git clone <ssh地址>
```

这样，远程仓库会被clone到本地，使用cd指令进入clone下来的文件夹，里面的内容和远程仓库完全一致。

3. 添加文件

在本地的仓库中新增一个文件，例如我在note目录下新增一个fy.txt文件，输入指令：

```
git status
```

可以查看到当前未处理的版本变动信息：

![1602687463237](C:\Users\Young Shaw\AppData\Roaming\Typora\typora-user-images\1602687463237.png)

使用以下命令将本地修改和更新的内容提交到自己的仓库：

```
git add .
git commit -m "和提交有关的说明信息"
git push origin master
```

其中，commit指令中附加的是对当前提交的说明信息。这个信息很重要，可以帮助识别和区分不同的版本，以及不同提交实现的不同功能等等。规范的开源项目会有自己的commit规范。

4. 提交PR

执行完git push指令之后，进入自己的github仓库，点击pull request，来创建和提交一个PR。提交一个PR意味着你对仓库的内容进行了一定的修改，现在要把修改的内容上传给主仓库，所以在创建PR的界面要写清楚你修改的内容。每次提交PR不宜修改过多内容，一般应对每个独立的问题提交单独的PR。提交之后，等待仓库管理者审核。若审核通过即可merge，则你修改的内容就会被包含在主仓库中。

**绑定主仓库**

前面的步骤只能让你向远程仓库和主仓库提交代码。但一个开源项目中，你还需要和别人提交到主仓库中的内容保持同步。你的远程仓库不会自动和主仓库保持同步更新，所以需要通过绑定主仓库来及时获取主仓库中更新的内容，以及将自己修改的内容提交到主仓库。例如本项目的主仓库ssh地址为 git@github.com:sspkusharing/LearningNotes.git

```
git remote add upstream <主仓库的ssh地址>
```

事实上，将代码推送到远程仓库之前，要先同步主仓库内容到本地，随后将主仓库的更新与本地仓库的更新同时推送到远程仓库，以确保远程仓库既和主仓库保持一致，又能接收到自己在本地进行的修改。

本地修改之前，先看一下自己的远程仓库界面，如果有"This branch is N commits behind xxx"，说明源项目在这段时间已经进行了若干版本的更新，这时候我们首先要在自己的仓库同步这些更新，然后进行修改。

```
//  1 拉取主仓库的版本
git fetch upstream  

//  2 将主仓库版本和本地仓库版本进行合并
git rebase upstream/master  

//  3 将本地已经式最新版本的仓库推送到远程仓库
git push origin master
```

**总结**

回顾一下前面的操作我们都完成了哪些事情：

- 找到一个开源项目，并fork到自己的github账号下；
- 在本地clone这个项目，并进行自己的修改；
- 为了同步开源项目的实时更新，需要将该项目的主仓库地址作为upstream和你的本地仓库进行绑定；
- 每次提交修改前，先拉取一下upstream中的最新代码；
- 将自己修改的内容首先提交到自己fork的仓库中，然后在github的界面里提交PR；

## 3. 尝试一下

在仓库中提交一次PR，包括但不限于会议记录，学习笔记，刷题练习，实验室项目学习报告等。可以默认创建在Note目录下，也可以自己创建新的目录结构。这个仓库可以变得越来越完善和丰富！

PS：这个教程也写的比较简略，也可能存在很多描述不清楚甚至出错的地方。这个文档同样提交在我们的仓库里，对本教程进行修改和补充也是完全可以的！本文档中没有涉及到的也很常用的知识包括分支创建，冲突处理，版本回退等等，期待大家进行完善！有任何相关的问题都可以找我讨论~也可以直接在仓库中提issue。



## 4. 参考资料

[1] [廖雪峰的git教程](https://www.liaoxuefeng.com/wiki/896043488029600)

[2] [向开源框架提交PR的过程](https://blog.csdn.net/vim_wj/article/details/78300239)

[3] [远程仓库版本回退方法](https://blog.csdn.net/fuchaosz/article/details/52170105)

[4] [git pull与fetch的区别](https://blog.csdn.net/qq_36113598/article/details/78906882)

[5] [多个github账号的SSH key切换](http://ju.outofmemory.cn/entry/143690)

[6] [我自己使用git时记录的笔记，比较杂乱，主要是对遇到的问题的处理](https://github.com/YangShaw/LearningNotes/blob/master/notes/git.md)

