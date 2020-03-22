
<!-- TOC -->

- [安装](#安装)
- [使用](#使用)
    - [配置SSH](#配置ssh)
    - [fork-远程仓库](#fork-远程仓库)
    - [clone-本地仓库](#clone-本地仓库)
    - [add & commit](#add--commit)
    - [绑定主仓库](#绑定主仓库)
    - [推送更新](#推送更新)
    - [提交PR](#提交pr)
- [参考资料](#参考资料)

<!-- /TOC -->

## 安装

在[官网](git-scm.com)下载并安装git客户端。

## 使用

### 配置SSH
使用git实现本地和远程之间的文件传输需要每次都输入GitHub的账号密码。但配置SSH的相关信息后可以通过SSH确保加密传输。配置方法参见[廖雪峰的教程（非常详细，跟着做一遍就好）](https://www.liaoxuefeng.com/wiki/896043488029600/896954117292416)。过程分为两步：
- 创建自己的SSH key
- 将SSH key添加到自己的GitHub账号中


### fork-远程仓库
点击本仓库右上角的fork，会在你的github账号下创建一个同名的复刻仓库。你本地的仓库被称为远程仓库（origin），被你fork的这个仓库被称为主仓库（upstream）。

### clone-本地仓库
1. 进入fork后在你的账号下生成的远程仓库，在右上角的Clone or downloads处复制SSH地址(git@开头，注意不要选成https地址。若未配置第一步的SSH，则只能复制https地址)，在本地你需要建立本地仓库的位置使用git bash执行指令：
```
git clone <复制下来的ssh地址>
```

2. 远程仓库会被clone到本地，使用cd指令进入clone下来的文件夹，里面的内容和远程仓库完全一致。

### add & commit
1. 添加文件

仓库中的内容有更新后，执行如下命令来将更新的文件添加到暂存区。
```
git add <文件名>
```
如果需要将所有内容都添加：
```
git add –A (需要大写) 或 git add .
```
2. 提交文件

多次将文件add到暂存区后，可以一次性提交到分支。后面附加的是当前提交的说明信息。这个信息很重要，可以帮助识别和区分不同的版本，以及不同提交实现的不同功能等等。最好是能够有一套信息规范。
```
git commit –m "和提交有关的信息"
```
3. 查看状态

可以看到当前有待add或commit的文件信息：
```
git status
```
4. 查看日志
日志文件中保存了各个版本提交的信息，使用如下指令来查看日志：
```
git log

git log --oneline //查看简略日志
```

### 绑定主仓库
你的远程仓库不会自动和主仓库保持同步更新。通过绑定主仓库来及时获取主仓库中更新的内容，以及将自己修改的内容提交到主仓库。
```
git remote add upstream <主仓库的ssh地址>
```

### 推送更新
将本地修改的内容add和commit之后要进行推送(push)。推送到远程仓库之前，先同步主仓库内容到本地，随后将主仓库的更新与本地仓库的更新同时推送到远程仓库，以确保远程仓库既和主仓库保持一致，又能接收到自己在本地进行的修改。

```
//  1 拉取主仓库的版本
git fetch upstream  

//  2 将主仓库版本和本地仓库版本进行合并
git rebase upstream/master  

//  3 将本地已经式最新版本的仓库推送到远程仓库
git push origin master
```

### 提交PR
此时进入GitHub中你的远程仓库页面，点击pull request即可创建一个PR。提交一个PR意味着你对仓库的内容进行了一定的修改，现在要把修改的内容上传给主仓库，所以在创建PR的界面要写清楚你修改的内容。每次提交PR不宜修改过多内容，一般应对每个独立的问题提交单独的PR。提交之后，等待仓库管理者审核。若审核通过即可merge，则你修改的内容就会被包含在主仓库中。




## 参考资料
上面的步骤可以帮助你快速的上手使用GitHub并成功提交第一个PR，但这些只是最基础和常用的操作。还有一些常见问题，可以参考下面的资料。欢迎持续补充。

[1] [廖雪峰的git教程](https://www.liaoxuefeng.com/wiki/896043488029600)

[2] [向开源框架提交PR的过程](https://blog.csdn.net/vim_wj/article/details/78300239)

[3] [远程仓库版本回退方法](https://blog.csdn.net/fuchaosz/article/details/52170105)

[4] [git pull与fetch的区别](https://blog.csdn.net/qq_36113598/article/details/78906882)

[5] [多个github账号的SSH key切换](http://ju.outofmemory.cn/entry/143690)
