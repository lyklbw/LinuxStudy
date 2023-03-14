# Git 的学习
Git下载之后如何操作？（下载按照网上的教程来一般这个地方不会出错）
首先理清楚逻辑，使用git当然想要使用到远程仓库这一个红利，所以首先是要配置SSH

git config --global user.name "注册名"  （lyklbw，注意是github注册名）
git config --global user.email "注册邮箱"
ssh-keygen -t rsa -C "自己的邮箱"  （新设备需要这一步，如过已经有了就跳过此步）
这是计算机便生成了密钥，终端会指示pub密钥的位置，我的电脑是在C:/user/15129/.ssh内部
有一个地方有点傻逼，我的电脑点.pub文件无法访问，直接在终端用cd打开 （也不知道cat行不行）
在这之后进入github网站设置新的SSH
ssh -T git@github.com 检查是否成功

之后选择自己的一个文件夹（注意不要仓库套仓库容易出现问题）
git init
之后跟着github的指导操作即可
echo "# test" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:lyklbw/仓库名.git //核心步骤
git push -u origin main
 
开心 结束啦啦啦
## 题外：我的`github`！

user name: lyklbw

#### 1.如何高效上传

https://blog.csdn.net/HUASHUDEYANJING/article/details/126521798

以后只要git push啦啦啦啦！

#### 2.一定不要再在网页上改东西了！！！

马的，废了好大功夫(主要现在太垃圾了)

```
$ git pull
$ git pull origin
```

**git pull** 命令用于从远程获取代码并合并本地的版本

#### 3.不要在仓库里面套仓库！

### 1.安装

https://www.liaoxuefeng.com/wiki/896043488029600 学习路径

本人git已经事先安装,命令如下：

`sudo apt-get install git`

### 2.创建版本库

版本库又名仓库，英文名**repository**，可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”

首先创一个空目录

```
$ mkdir learngit
$ cd learngit
$ pwd
/Users/michael/learngit
```

再通过命令转变目录为仓库

```
$ git init
```





### 3.实例

在`learngit`目录下编写了一个readme.txt 文件

第一步

#### `git add readme.txt`

`git add readme.txt`

ps: gIt add . 中 `.` 表示全部文件

第二步

#### `git commit -m comment `

`git commit -m readme.txt`

之后更改`readme.txt`内容

更改文件名称：（实例）

```
git mv test rename
git commit -m rename 
git push
```



#### `git status`

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

`git status`命令可以让我们时刻掌握仓库当前的状态，上面的命令输出告诉我们，`readme.txt`被修改过了，但还没有准备提交的修改。

虽然Git告诉我们`readme.txt`被修改了，但如果能看看具体修改了什么内容，自然是很好的。比如你休假两周从国外回来，第一天上班时，已经记不清上次怎么修改的`readme.txt`，所以，需要用`git diff`这个命令看看

#### `git diff`  vscode下安装git lens 体验感更佳

```
lyk@LYKdiandong:~/lbwnb/learngit$ git diff
diff --git a/readme.txt b/readme.txt
index 46d49bf..9247db6 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
-Git is a version control system.
+Git is a distributed version control system.
 Git is free software.
```

知道了修改，提交修改和提交新文件是一样的两步

#### 小结1

- 要随时掌握工作区的状态，使用`git status`命令。
- 如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容。

#### `git log`

`git log`命令显示从最近到最远的提交日志，我们可以看到3次提交，最近的一次是`append GPL`，上一次是`add distributed`，最早的一次是`wrote a readme file`。
英文状态下键入 q 退出 log 模式

```
commit 7379d77a99e4aef9a588df37d0f86e0e713756ec (HEAD -> master)
Author: lyk <1512972802@qq.com>
Date:   Mon Jan 2 16:12:22 2023 +0800

    append GPL

commit 3e3d4d833e8d144adacbf53b086d3b6f3582c3a2
Author: lyk <1512972802@qq.com>
Date:   Mon Jan 2 16:09:53 2023 +0800

    add distributed

commit da51e0fa68b523cb1296ff5c2c06ebeb636f76bc
Author: lyk <1512972802@qq.com>
Date:   Mon Jan 2 16:00:10 2023 +0800

    wrote a readme file
```

如果嫌输出信息太多，看得眼花缭乱的，可以试试加上`--pretty=oneline`参数：

```
lyk@LYKdiandong:~/lbwnb/learngit$ git log --pretty=oneline
7379d77a99e4aef9a588df37d0f86e0e713756ec (HEAD -> master) append GPL
3e3d4d833e8d144adacbf53b086d3b6f3582c3a2 add distributed
da51e0fa68b523cb1296ff5c2c06ebeb636f76bc wrote a readme file
```

好了，现在我们启动时光穿梭机，准备把`readme.txt`回退到上一个版本，也就是`add distributed`的那个版本，怎么做呢？

首先，Git必须知道当前版本是哪个版本，在Git中，用`HEAD`表示当前版本，也就是最新的提交`1094adb...`（注意我的提交ID和你的肯定不一样），上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个`^`比较容易数不过来，所以写成`HEAD~100`。

#### `git reset`

现在，我们要把当前版本`append GPL`回退到上一个版本`add distributed`，就可以使用`git reset`命令：

```
lyk@LYKdiandong:~/lbwnb/learngit$ git reset --hard HEAD^
HEAD 现在位于 3e3d4d8 add distributed
```

最新的那个版本`append GPL`已经看不到了！好比你从21世纪坐时光穿梭机来到了19世纪，想再回去已经回不去了，肿么办？

办法其实还是有的，只要上面的命令行窗口还没有被关掉，你就可以顺着往上找啊找啊，找到那个`append GPL`的`commit id`是`1094adb...`，于是就可以指定回到未来的某个版本： (版本号没必要写全，前几位就可以了，Git会自动去找。当然也不能只写前一两位，因为Git可能会找到多个版本号，就无法确定是哪一个了。)

```
lyk@LYKdiandong:~/lbwnb/learngit$ git reset --hard 7379d
HEAD 现在位于 7379d77 append GPL
```



现在，你回退到了某个版本，关掉了电脑，第二天早上就后悔了，想恢复到新版本怎么办？找不到新版本的`commit id`怎么办？

#### `git reflog`

在Git中，总是有后悔药可以吃的。当你用`$ git reset --hard HEAD^`回退到`add distributed`版本时，再想恢复到`append GPL`，就必须找到`append GPL`的commit id。Git提供了一个命令`git reflog`用来记录你的每一次命令：

```
lyk@LYKdiandong:~/lbwnb/learngit$ git reflog
7379d77 (HEAD -> master) HEAD@{0}: reset: moving to 7379d
3e3d4d8 HEAD@{1}: reset: moving to HEAD^
7379d77 (HEAD -> master) HEAD@{2}: commit: append GPL
3e3d4d8 HEAD@{3}: commit: add distributed
da51e0f HEAD@{4}: commit (initial): wrote a readme file
```

#### 小结2

- `HEAD`指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。
- 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。
- 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。

### 4.工作区与暂存区

#### 工作区（Working Directory）

就是你在电脑里能看到的目录，比如我的`learngit`文件夹就是一个工作区：

![working-dir](https://www.liaoxuefeng.com/files/attachments/919021113952544/0)

#### 版本库（Repository）

工作区有一个隐藏目录`.git`，这个不算工作区，而是Git的版本库。

Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支`master`，以及指向`master`的一个指针叫`HEAD`。

![git-repo](https://www.liaoxuefeng.com/files/attachments/919020037470528/0)

前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：

第一步是用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区；

第二步是用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支。

因为我们创建Git版本库时，Git自动为我们创建了唯一一个`master`分支，所以，现在，`git commit`就是往`master`分支上提交更改。

你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

俗话说，实践出真知。现在，我们再练习一遍，先对`readme.txt`做个修改，比如加上一行内容：

```
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
```

然后，在工作区新增一个`LICENSE`文本文件（内容随便写）。

用`git status`查看一下状态：

```
lyk@LYKdiandong:~/lbwnb/learngit$ git status
位于分支 master
尚未暂存以备提交的变更：
  （使用 "git add <文件>..." 更新要提交的内容）
  （使用 "git restore <文件>..." 丢弃工作区的改动）
	修改：     readme.txt

未跟踪的文件:
  （使用 "git add <文件>..." 以包含要提交的内容）
	.readme.txt.swp
	LICENSE

修改尚未加入提交（使用 "git add" 和/或 "git commit -a"）

```

Git非常清楚地告诉我们，`readme.txt`被修改了，而`LICENSE`还从来没有被添加过，所以它的状态是`Untracked`。

现在，使用两次命令`git add`，把`readme.txt`和`LICENSE`都添加后，用`git status`再查看一下：

```
lyk@LYKdiandong:~/lbwnb/learngit$ git status
位于分支 master
要提交的变更：
  （使用 "git restore --staged <文件>..." 以取消暂存）
	新文件：   LICENSE
	修改：     readme.txt
```

![git-stage](https://www.liaoxuefeng.com/files/attachments/919020074026336/0)

所以，`git add`命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行`git commit`就可以一次性把暂存区的所有修改提交到分支。

提交后，工作区是干净的

```
lyk@LYKdiandong:~/lbwnb/learngit$ git status
位于分支 master
无文件要提交，干净的工作区
```

![git-stage-after-commit](https://www.liaoxuefeng.com/files/attachments/919020100829536/0)

### 5.管理修改

为什么说Git管理的是修改，而不是文件呢？我们还是做实验。第一步，对readme.txt做一个修改，比如加一行内容。

之后`add`保存

然后再次修改

`git commit`

```
lyk@LYKdiandong:~/lbwnb/learngit$ git status
位于分支 master
尚未暂存以备提交的变更：
  （使用 "git add <文件>..." 更新要提交的内容）
  （使用 "git restore <文件>..." 丢弃工作区的改动）
	修改：     readme.txt

修改尚未加入提交（使用 "git add" 和/或 "git commit -a"）
```

第一次修改 -> `git add` -> 第二次修改 -> `git commit` 

Git管理的是修改，当你用`git add`命令后，在工作区的第一次修改被放入暂存区，准备提交，但是，在工作区的第二次修改并没有放入暂存区，所以，`git commit`只负责把暂存区的修改提交了，也就是第一次的修改被提交了，第二次的修改不会被提交。

##### `git diff HEAD -- readme.txt`

提交后，用`git diff HEAD -- readme.txt`命令可以查看工作区和版本库里面最新版本的区别：

```
lyk@LYKdiandong:~/lbwnb/learngit$ git diff HEAD -- readme.txt
diff --git a/readme.txt b/readme.txt
index 539203e..d8ee326 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,4 +1,4 @@
 Git is a distributed version control system.
 Git is free software distributed under the GPL.
 Gut has a myltable index called stage
-Git tracks change 
+Git tracks change of files. 
```

那怎么提交第二次修改呢？你可以继续`git add`再`git commit`，也可以别着急提交第一次修改，先`git add`第二次修改，再`git commit`，就相当于把两次修改合并后一块提交了：

第一次修改 -> `git add` -> 第二次修改 -> `git add` -> `git commit`

#### 小结

现在，你又理解了Git是如何跟踪修改的，每次修改，如果不用`git add`到暂存区，那就不会加入到`commit`中。

### 6.撤销修改

输入`git status `发现：

```
lyk@LYKdiandong:~/lbwnb/learngit$ git status
位于分支 master
尚未暂存以备提交的变更：
  （使用 "git add <文件>..." 更新要提交的内容）
  （使用 "git restore <文件>..." 丢弃工作区的改动）
	修改：     readme.txt

修改尚未加入提交（使用 "git add" 和/或 "git commit -a"）
```

###### `git checkout --file`

`git checkout --file`可以丢弃工作区的修改：

```
$ git checkout -- readme.txt
```

命令`git checkout -- readme.txt`意思就是，把`readme.txt`文件在工作区的修改全部撤销，这里有两种情况：

一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

`git checkout -- file`命令中的`--`很重要，没有`--`，就变成了“切换到另一个分支”的命令，我们在后面的分支管理中会再次遇到`git checkout`命令。

(教材版本比较老，checkout 已经被 restore 替代了)							 															 						

自然，你是不会犯错的。不过现在是凌晨两点，你正在赶一份工作报告，你在`readme.txt`中添加了一行：

```
$ cat readme.txt
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.
My stupid boss still prefers SVN.
```

在你准备提交前，一杯咖啡起了作用，你猛然发现了`stupid boss`可能会让你丢掉这个月的奖金！

既然错误发现得很及时，就可以很容易地纠正它。你可以删掉最后一行，手动把文件恢复到上一个版本的状态。如果用`git status`查看一下：

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore -- <file>..." to discard changes in working directory)

	modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

但是

现在假定是凌晨3点，你不但写了一些胡话，还`git add`到暂存区了：

可是睡前你用cat发现了端倪

```
lyk@LYKdiandong:~/lbwnb/learngit$ cat readme.txt 
Git is a distributed version control system.
Git is free software distributed under the GPL.
Gut has a myltable index called stage
Git tracks change of files.
I love JK. 
```

显然最后一句话会影响你的高大形象

而且聪明的你使用`git status`进行了检查

```
lyk@LYKdiandong:~/lbwnb/learngit$ git status
位于分支 master
要提交的变更：
  （使用 "git restore --staged <文件>..." 以取消暂存）
	修改：     readme.txt
```

###### <u>`git reset HEAD readme.txt !!!!`</u>

先一手性感的小`git reset HEAD readme.txt`

以取消寄存区(staged)保存的 回到工作区

`git restore -- readme.txt`  取消修改 嘎

### 7.删除文件

直接实战：

```
vim test.txt(随意输入)
git add test.txt
git commit -m "add test.txt"
```

#####  `rm test.txt`

一般情况下，你通常直接在文件管理器中把没用的文件删了，或者用`rm`命令删了：

```
$ rm test.txt
```

这个时候，Git知道你删除了文件，因此，工作区和版本库就不一致了，`git status`命令会立刻告诉你哪些文件被删除了：

##### `git rm`

现在你有两个选择，一是确实要从版本库中删除该文件，那就用命令`git rm`删掉，并且`git commit`

另一种情况是删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：

```
git restore -- test.txt
```

#### 小结

命令`git rm`用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失**最近一次提交后你修改的内容**。

2023.1.2 night done

### 8.远程仓库

#### 添加远程仓库

第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：

然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容(cat 一下全部复制)

```
git branch -M main
git remote add origin https://XXX/XXX/XXX.git
git push -u origin main
```

#### 从远程库克隆

https://github.com/lyklbw/gitkills

这是我在github新建立的仓库

ps :我们勾选`Initialize this repository with a README`，这样GitHub会自动为我们创建一个`README.md`文件。创建完毕后，可以看到`README.md`文件

#### 小结

要克隆一个仓库，首先必须知道仓库的地址，然后使用`git clone`命令克隆。

Git支持多种协议，包括`https`，但`ssh`协议速度最快。

### 9.分支管理

分支就是科幻电影里面的平行宇宙，当你正在电脑前努力学习Git的时候，另一个你正在另一个平行宇宙里努力学习SVN。

如果两个平行宇宙互不干扰，那对现在的你也没啥影响。不过，在某个时间点，两个平行宇宙合并了，结果，你既学会了Git又学会了SVN！

分支在实际中有什么用呢？假设你准备开发一个新功能，但是需要两周才能完成，第一周你写了50%的代码，如果立刻提交，由于代码还没写完，不完整的代码库会导致别人不能干活了。如果等代码全部写完再一次提交，又存在丢失每天进度的巨大风险。

现在有了分支，就不用怕了。你创建了一个属于你自己的分支，别人看不到，还继续在原来的分支上正常工作，而你在自己的分支上干活，想提交就提交，直到开发完毕后，再一次性合并到原来的分支上，这样，既安全，又不影响别人工作。

其他版本控制系统如SVN等都有分支管理，但是用过之后你会发现，这些版本控制系统创建和切换分支比蜗牛还慢，简直让人无法忍受，结果分支功能成了摆设，大家都不去用。

但Git的分支是与众不同的，无论创建、切换和删除分支，Git在1秒钟之内就能完成！无论你的版本库是1个文件还是1万个文件。

#### 创建与合并

| git 操作              | 具体含义          |
| --------------------- | ----------------- |
| git checkout -b `dev` | 创建并切换到`dev` |
| git branch -d `dev`   | 删除`dev`         |

在[版本回退](https://www.liaoxuefeng.com/wiki/896043488029600/897013573512192)里，你已经知道，每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即`master`分支。`HEAD`严格来说不是指向提交，而是指向`master`，`master`才是指向提交的，所以，`HEAD`指向的就是当前分支。

一开始的时候，`master`分支是一条线，Git用`master`指向最新的提交，再用`HEAD`指向`master`，就能确定当前分支，以及当前分支的提交点：

```ascii
                  HEAD
                    │
                    │
                    ▼
                 master
                    │
                    │
                    ▼
┌───┐    ┌───┐    ┌───┐
│   │───▶│   │───▶│   │
└───┘    └───┘    └───┘
```

每次提交，`master`分支都会向前移动一步，这样，随着你不断提交，`master`分支的线也越来越长。

当我们创建新的分支，例如`dev`时，Git新建了一个指针叫`dev`，指向`master`相同的提交，再把`HEAD`指向`dev`，就表示当前分支在`dev`上：

```ascii
                 master
                    │
                    │
                    ▼
┌───┐    ┌───┐    ┌───┐
│   │───▶│   │───▶│   │
└───┘    └───┘    └───┘
                    ▲
                    │
                    │
                   dev
                    ▲
                    │
                    │
                  HEAD
```

你看，Git创建一个分支很快，因为除了增加一个`dev`指针，改改`HEAD`的指向，工作区的文件都没有任何变化！

不过，从现在开始，对工作区的修改和提交就是针对`dev`分支了，比如新提交一次后，`dev`指针往前移动一步，而`master`指针不变：

```ascii
                 master
                    │
                    │
                    ▼
┌───┐    ┌───┐    ┌───┐    ┌───┐
│   │───▶│   │───▶│   │───▶│   │
└───┘    └───┘    └───┘    └───┘
                             ▲
                             │
                             │
                            dev
                             ▲
                             │
                             │
                           HEAD
```

假如我们在`dev`上的工作完成了，就可以把`dev`合并到`master`上。Git怎么合并呢？最简单的方法，就是直接把`master`指向`dev`的当前提交，就完成了合并：

```ascii
                           HEAD
                             │
                             │
                             ▼
                          master
                             │
                             │
                             ▼
┌───┐    ┌───┐    ┌───┐    ┌───┐
│   │───▶│   │───▶│   │───▶│   │
└───┘    └───┘    └───┘    └───┘
                             ▲
                             │
                             │
                            dev
```

所以Git合并分支也很快！就改改指针，工作区内容也不变！

合并完分支后，甚至可以删除`dev`分支。删除`dev`分支就是把`dev`指针给删掉，删掉后，我们就剩下了一条`master`分支：

```ascii
                           HEAD
                             │
                             │
                             ▼
                          master
                             │
                             │
                             ▼
┌───┐    ┌───┐    ┌───┐    ┌───┐
│   │───▶│   │───▶│   │───▶│   │
└───┘    └───┘    └───┘    └───┘
```

下面进入实战部分

首先，我们创建`dev`分支，然后切换到`dev`分支：

#### checkout

> 切换分支 git checkout master

```
lyk@LYKdiandong:~/lbwnb/learngit$ git checkout -b dev
切换到一个新分支 'dev'
```

`git checkout`命令加上`-b`参数表示创建并切换

然后，用`git branch`命令查看当前分支：

```
lyk@LYKdiandong:~/lbwnb/learngit$ git branch
* dev
  master
```

`git branch`命令会列出所有分支，当前分支前面会标一个`*`号。

然后

```
lyk@LYKdiandong:~/lbwnb/learngit$ git commit -m "branch test"
[dev edefa2a] branch test
 1 file changed, 2 insertions(+), 1 deletion(-)
```

现在 分支工作完成，那我们回到master

```
git checkout master
```

切换回`master`分支后，再查看一个`readme.txt`文件，刚才添加的内容不见了！因为那个提交是在`dev`分支上，而`master`分支此刻的提交点并没有变：

![git-br-on-master](https://www.liaoxuefeng.com/files/attachments/919022533080576/0)

现在，我们把`dev`分支的工作成果合并到`master`分支上：

```
lyk@LYKdiandong:~/lbwnb/learngit$ git merge dev
更新 d004212..edefa2a
Fast-forward
 readme.txt | 3 ++-
 1 file changed, 2 insertions(+), 1 deletion(-)
```

合并完成后，就可以放心地删除`dev`分支了：

#### branch 

>git branch 查看
>
>git branch -d `dev` 删除

```
$ git branch -d dev
Deleted branch dev (was b17d20e).
```

删除后，查看`branch`，就只剩下`master`分支了：

```
$ git branch
* master
```

#### switch

我们注意到切换分支使用`git checkout <branch>`，而前面讲过的撤销修改则是`git checkout -- <file>`，同一个命令，有两种作用，确实有点令人迷惑。

实际上，切换分支这个动作，用`switch`更科学。因此，最新版本的Git提供了新的`git switch`命令来切换分支：

创建并切换到新的`dev`分支，可以使用：

```
$ git switch -c dev
```

直接切换到已有的`master`分支，可以使用：

```
$ git switch master
```

使用新的`git switch`命令，比`git checkout`要更容易理解。

#### 小结

Git鼓励大量使用分支：

查看分支：`git branch`

创建分支：`git branch <name>`

切换分支：`git checkout <name>`或者`git switch <name>`

ps : git checkout -- <file\> 是撤销修改

创建+切换分支：`git checkout -b <name>`或者`git switch -c <name>`

合并某分支到当前分支：`git merge <name>`

删除分支：`git branch -d <name>`

#### 解决冲突

本来在这节之前就已经搁笔，但是这个好像非常重要！

人生不如意之事十之八九，合并分支往往也不是一帆风顺的。

准备新的`feature1`分支，继续我们的新分支开发：

```
$ git switch -c feature1
Switched to a new branch 'feature1'
```

修改`readme.txt`最后一行，改为：

```
Creating a new branch is quick AND simple.
```

在`feature1`分支上提交：

```
lyk@LYKdiandong:~/lbwnb/about github/learngit(no remote res)$ git commit -m "add AND"
[featurel 14e9c34] add AND
 1 file changed, 1 insertion(+), 1 deletion(-)
```

切换到`master`分支：

在`master`分支上把`readme.txt`文件的最后一行改为：

```
Creating a new branch is quick & simple.
```

并提交

```
lyk@LYKdiandong:~/lbwnb/abut github/learngit(no remote res)$ git commit -m "add &"
[master 4e6b4dd] add &
 1 file changed, 1 insertion(+), 1 deletion(-)
```

现在，`master`分支和`feature1`分支各自都分别有新的提交，变成了这样：

```ascii
                            HEAD
                              │
                              │
                              ▼
                           master
                              │
                              │
                              ▼
                            ┌───┐
                         ┌─▶│   │
┌───┐    ┌───┐    ┌───┐  │  └───┘
│   │───▶│   │───▶│   │──┤
└───┘    └───┘    └───┘  │  ┌───┐
                         └─▶│   │
                            └───┘
                              ▲
                              │
                              │
                          feature1
```

这种情况下，Git无法执行“快速合并”，只能试图把各自的修改合并起来，但这种合并就可能会有冲突，我们试试看：

```
lyk@LYKdiandong:~/lbwnb/about github/learngit(no remote res)$ git merge featurel 
自动合并 readme.txt
冲突（内容）：合并冲突于 readme.txt
自动合并失败，修正冲突然后提交修正的结果。
```

使用`git status`查看当前情况

```
lyk@LYKdiandong:~/lbwnb/about github/learngit(no remote res)$ git status
位于分支 master
您有尚未合并的路径。
  （解决冲突并运行 "git commit"）
  （使用 "git merge --abort" 终止合并）

未合并的路径：
  （使用 "git add <文件>..." 标记解决方案）
	双方修改：   readme.txt

修改尚未加入提交（使用 "git add" 和/或 "git commit -a"）
```

查看一下文本内容

```
lyk@LYKdiandong:~/lbwnb/about github/learngit(no remote res)$ cat readme.txt 
Git is a distributed version control system.
Git is free software distributed under the GPL.
Gut has a myltable index called stage
Git tracks change of files.
<<<<<<< HEAD
Creating a new branch is quick & simple
=======
Creating a new branch is quick AND simple 
>>>>>>> featurel
```

Git用`<<<<<<<`，`=======`，`>>>>>>>`标记出不同分支的内容，我们修改

```
Creating a new branch is quick and simple 
```

再 `add`  `commit `保存

现在，`master`分支和`feature1`分支变成了下图所示：

```ascii
                                     HEAD
                                       │
                                       │
                                       ▼
                                    master
                                       │
                                       │
                                       ▼
                            ┌───┐    ┌───┐
                         ┌─▶│   │───▶│   │
┌───┐    ┌───┐    ┌───┐  │  └───┘    └───┘
│   │───▶│   │───▶│   │──┤             ▲
└───┘    └───┘    └───┘  │  ┌───┐      │
                         └─▶│   │──────┘
                            └───┘
                              ▲
                              │
                              │
                          feature1
```

```
lyk@LYKdiandong:~/lbwnb/about github/learngit(no remote res)$ git commit -m "conflict fixed"
[master 7c0403d] conflict fixed
lyk@LYKdiandong:~/lbwnb/about github/learngit(no remote res)$ git status
位于分支 master
无文件要提交，干净的工作区
```

用带参数的`git log`也可以看到分支的合并情况：(第一次用洪筛耶)

> <span style="color:red;">git log --graph --pretty=oneline --abbrev-commit</span>

```
yk@LYKdiandong:~/lbwnb/about github/learngit(no remote res)$ git log --graph --pretty=oneline --abbrev-commit
*   7c0403d (HEAD -> master) conflict fixed
|\  
| * 14e9c34 (featurel) add AND
* | 4e6b4dd add &
|/  
* e6f88cb delete the last row of readme.txt
* c990904 AND simple
* edefa2a branch test
* d004212 add test.txt
* 03d7333 done
* df90b20 git tracks changes1
* 23e4d20 git tracks changes
* 33b5f99 understand how stage works
* 7379d77 append GPL
* 3e3d4d8 add distributed
* da51e0f wrote a readme file
```

最后删除分支

```
lyk@LYKdiandong:~/lbwnb/about github/learngit(no remote res)$ git branch -d featurel 
已删除分支 featurel（曾为 14e9c34）。
```

























