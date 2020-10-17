<center><font size=6 color='blue'>Git & Github</font></center>

[TOC]

# 1.Git

Git是目前世界上最先进的分布式版本控制系统，简单的来说就是实现文件历史管理的工具。

## 1.1.安装Git

**在Linux上安装Git**

输入`git`，可以看看系统是否安装Git:

```
$ git
The program 'git' is currently not installed. You can install it by typing:
sudo apt-get install git
```

如上，则说明Git未安装，并告知安装Git的命令。

使用Ubuntu Linux系统，通过输入命令`sudo apt-get install git`，就可以直接完成Git的安装。

**在Windows上安装Git**

在Windows上使用Git，可以从Git官网直接[下载安装程序](https://git-scm.com/downloads)，然后按默认选项安装即可。

安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！

安装完成后需要后，需要进行设置，在命令行输入：

```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

注意`git config`命令的`--global`参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

## 1.2.创建版本库

版本库又名仓库，英文名**repository**，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

**step.1**初始化

从终端（cmd）进入你想要记录内容更改的文件夹里。

输入命令：

```
git init
```

这个文件夹目录就被创建为版本库。（如果是空文件夹会提示`Initialized empty Git repository in /home/yep/code/gittest/.git/`，告诉你文件夹为空）

**step.2**添加文件

在Git仓库目录下写一个文件`readme.txt`文件。

第一步，用命令`git add`告诉Git，把文件添加到仓库：

```
$ git add readme.txt
```

执行上面的命令，没有任何显示，说明添加成功。

第二步，用命令`git commit`告诉Git，把文件提交到仓库：

```
$ git commit -m "wrote a readme file"
[master (root-commit) eaadf4e] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
```

简单解释一下`git commit`命令，`-m`后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。

`commit`可以一次提交很多文件，所以你可以多次`add`不同的文件，比如：

```
$ git add file1.txt
$ git add file2.txt file3.txt
$ git commit -m "add 3 files."
```

tips:添加某个文件时，该文件必须在当前目录下存在，用`ls`或者`dir`命令查看当前目录的文件，看看文件是否存在，或者是否写错了文件名。

## 1.3.版本回退

`git status`命令可以让我们时刻掌握仓库当前的状态。

`git diff`命令可以查看difference，修改了什么内容。

`git log`命令查看版本控制系统的历史记录，显示从最近到最远的提交日志，一大串类似`1094adb...`的是`commit id`（版本号）。提交说明是中文，使用`git log`会显示乱码，解决方法：`$ git config --global core.quotepath false`

**回到上一个版本**

```
$ git reset --hard HEAD^     "^" or ~1
```

回到上一版本后，新版本的就找不到了，只要上面的命令行窗口还没有被关掉，你就可以顺着往上找啊找啊，找到那个新版本的`commit id`是`1094adb...`，于是就可以指定回到未来的某个版本：

```
$ git reset --hard 1094a
```

版本号没必要写全，前几位就可以了，Git会自动去找。当然也不能只写前一两位，因为Git可能会找到多个版本号，就无法确定是哪一个了。

如果命令行窗口已经关闭了，想回到最新版本，Git提供了一个命令`git reflog`用来记录你的每一次命令：

```
$ git reflog
```

**管理修改**

Git是如何跟踪修改的，每次修改，如果不用`git add`到暂存区，那就不会加入到`commit`中。

多次修改可以，第一次修改 -> `git add` -> 第二次修改 -> `git add` -> `git commit`

**撤销修改**

```
$ git checkout -- readme.txt    or git restore readme.txt
```

命令`git checkout -- readme.txt`意思就是，把`readme.txt`文件在工作区的修改全部撤销，这里有两种情况：

一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

命令`git reset HEAD <file>`可以把暂存区的修改撤销掉（unstage），重新放回工作区。

**删除文件**

一般情况下，通常直接在文件管理器中把没用的文件删了，或者用`rm`命令删了：

```
$ rm test.txt
```

一是确实要从版本库中删除该文件，那就用命令`git rm`删掉，并且`git commit`：

```
$ git rm test.txt
rm 'test.txt'
```

另一种情况是删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：

```
$ git checkout -- test.txt
```

# 2.Github

## 2.1.远程库

第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

可以在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

```
$ cd ~/.ssh
$ pwd 就知道主目录的路径了
```

第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：

然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容：

![github-addkey-1](https://www.liaoxuefeng.com/files/attachments/919021379029408/0)

点“Add Key”，你就应该看到已经添加的Key：

![github-addkey-2](https://www.liaoxuefeng.com/files/attachments/919021395420160/0)

为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。

当然，GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。

最后友情提示，在GitHub上免费托管的Git仓库，任何人都可以看到喔（但只有你自己才能改）。所以，不要把敏感信息放进去。

## 2.2.远程库操作

**添加远程库**

在右上角找到“Create a new repo”按钮，创建一个新的仓库。

在本地的`learngit`仓库下运行命令：

```
$ git remote add origin git@github.com:michaelliao/learngit.git
```

请千万注意，把上面的`michaelliao`替换成你自己的GitHub账户名，否则，你在本地关联的就是我的远程库，关联没有问题，但是你以后推送是推不上去的，因为你的SSH Key公钥不在我的账户列表中。

下一步，就可以把本地库的所有内容推送到远程库上：

```
$ git push -u origin master
```

由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。

```
$ git push origin master
```

**克隆远程库**

```
$ git clone git@github.com:michaelliao/gitskills.git
```

## 2.3.标签

命令`git tag <name>`就可以打一个新标签：

```
$ git tag v1.0
```

可以用命令`git tag`查看所有标签：

```
$ git tag
v1.0
```

默认标签是打在最新提交的commit上的。有时候，如果忘了打标签。

方法是找到历史提交的commit id，然后打上就可以了：

比方说要对`add merge`这次提交打标签，它对应的commit id是`f52c633`，敲入命令：

```
$ git tag v0.9 f52c633
```

再用命令`git tag`查看标签：

```
$ git tag
v0.9
v1.0
```

注意，标签不是按时间顺序列出，而是按字母排序的。可以用`git show <tagname>`查看标签信息：

```
$ git show v0.9
```

创建带有说明的标签，用`-a`指定标签名，`-m`指定说明文字：

```
$ git tag -a v0.1 -m "version 0.1 released" 1094adb
```

# 3.参考

[廖雪峰的网站]()

[git命令整理](https://github.com/yanqiangsjz/git-study/blob/master/git.md)

