# git学习笔记

# 1月12回顾

## Git 基本概念

![](https://z3.ax1x.com/2021/12/03/odQ0HK.png)

###### **❣基本概念及原理**



- **工作区**（workplace）：工作台，就是平时存放项目代码的地方
- **暂存区**（Index/staging area）：用于临时存放改动，事实上**只是一个文件**，保存即将提交到文件列表信息
- **版本库**（local repository）：仓库。安全存放数据的位置，这里有我们提交到所有版本的数据。这里的**HEAD**指向最新放入仓库的版本
- **远程仓库**（remote repository）：托管代码的服务器，简单理解为项目组的一台电脑用于远程数据交换



###### 工作流程

- 克隆git资源作为工作目录（工作台在本地）
- 在工作目录（本地）上添加或修改文件
- 将**需要进行版本管理的文件放入暂存区域**
- 将暂存区的文件提交到git仓库
- git管理的文件有3种状态：**已修改（modified）；已暂存（staged）；已提交（committed）**



**知识点**：版本控制就是对文件进行修改，提交等操作



 **原理**：（写代码）工作区--**git add**-->(临时)暂存区--**git commit**-->(历史)版本库（本地仓库repository）



![](https://s4.ax1x.com/2022/01/12/7uLNvR.png)



**基本关系**：

使用add命令将新建的文件加入到**暂存区--->Staged**

使用commit命令将暂存区的文件提交到**本地仓库--->Unmodified**

如果对Unmodified状态的文件进行修改---> modified

如果对Unmodified状态的文件进行remove操作--->Untracked

------

##### 四个区域常用命令

###### 新建代码库（repository）

```
#在当前目录创建一个代码库
git init

#创建一个目录，将其初始化为git代码库
git init [project-name]

#下载一个项目和它的整个代码历史
git clone [url]
```

###### 查看文件状态

```
#查看指定文件状态
git status [filename]

#查看所有文件状态
git status
```

###### 创建一个空目录

```
$ mkdir 目录名
$ cd 该目录名字   //cd是进入某个文件夹的命令
$ pwd           //pwd用于显示当前目录的路径
$ git init      //把该目录变成git可以管理的仓库
```

###### 把创建的文件放到git仓库

```
//假设你已经拥有一个文本文件.txt，那就需要先把它放到-->托管在git的目录文件夹下，才能通过got命令成功上传git仓库
//第一步：
git add readme.txt
//第二步
git commit -m"备注信息"

//可以一次包含多个文件提交，在add后面直接放文件名，commit一次上交
```

## 细节补充

```
除 git init外，git命令必须在git仓库目录里面执行
```

###### pwd

pwd用于现实化当前目录，如果使用的是操作系统，确保目录名字不包含中文



###### git init

git init可以把**当前目录**变成git可以管理的**仓库**



###### 创建目录并变成可管理仓库

- mkdir 目录名字； cd（进入） 目录名字；git  init；



- 如果是已经存在的文件：

- git init； git init [project name]; git clone [url]  （下载整个项目和项目历史



###### 工作区

在电脑可以看见的目录，比如自己的文件夹`learngit`就是一个工作区



###### 版本库

工作区有一个隐藏目录`.git`,不算工作区，算**git的版本库（仓库）**



###### git分版本库

git版本库里有很多东西，最重要的称为 **stage的暂存区;**

还有git自动为我们创建的第一个分支;

以及指向`master`的一个指针叫`HEAD`.

![](https://s4.ax1x.com/2022/01/15/7JOCE4.png)



我们将文件往git版本库添加的时候，分两步进行：

- 用git add 把文件添加上去，即把文件添加到暂存区
- 第二步，用`git commit`提交更改，即把暂存区的所有内容提交到当前分支
- 我们创建git版本库的时候，git仓库自动创建了唯一一个`master`分支，所以现在 git commit就是往 master 上提交更改





###### 撤销修改

- **未git add**

手动删除+手动恢复到上一个版本的状态。

但是 `git checkout --file`可以**丢弃工作区的修改**：

命令`git checkout -- readme.txt`意思就是：把`readme.txt`文件在工作区的**修改全部撤销**，这里有两种情况：

**一种**是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

**一种**是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。



- **已经git add 但是没有git commit**

  修改后重新git add 添加到暂存区；但是可以使用命令`git reset HEAD <file>`把暂存区的修改撤销掉，重新放回工作区

```
$ git reset HEAD readme.txt
Unstaged changes after reset:
M	readme.txt
```

git reset命令可以回退版本，也可以把暂存区的修改回退到工作区。当我们使用`HEAD`表示最新版本



💝再用`git status`查看一下，现在暂存区是干净的，工作区有修改：

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   readme.txt
```

**还记得如何丢弃工作区的修改吗？**

```
$ git checkout -- readme.txt

$ git status
On branch master
nothing to commit, working tree clean
```



- **已经git commit**

可以使用版本回退，回退到上一个版本。

但是这是有条件的：还没有把自己本地版本库推送到远程。



------

###### 删除文件

在git，删除也是一个修改操作

- 假设背景：（添加一个文件到git并且提交）

```
$ git add test.txt

$ git commit -m "add test.txt"
[master b84166e] add test.txt
 1 file changed, 1 insertion(+)
 create mode 100644 test.txt
```



- 一般情况下：在文件管理器把没有的文件删除，或者使用`rm`命令删除
- 但是这个时候，git知道删除了文件，此时工作区和版本库不一致，`git status`会告诉我们哪些文件被删除



- 因此现在有两个选择，一是从版本库删除文件：使用`git rm`命令，并且使用`git commit`

```
$ git rm test.txt
rm 'test.txt'

$ git commit -m "remove test.txt"
[master d46f35e] remove test.txt
 1 file changed, 1 deletion(-)
 delete mode 100644 test.txt
```

- 一种是删除错了，因为版本库里还有，就可以轻松的把误删的文件恢复到最新的版本

```
$ git checkout -- test.txt
```

**`git checkout`其实是用版本库里的版本替换工作区的版本，无论是工作区是修改还是删除，都可以一键还原**

------



## **操作命令**

##### **git add**    

(修改或新增文件到**暂存区**)

```
添加一个或者多个文件
git add [file1][file2]...
    
添加指定目录到暂存区
git add [dir]
    
添加当前目录下所有文件到暂存区
git add.
```

```

$ touch README  #创建文件
$ touch hello.php #创建文件
$ ls //list directory contents 用来显示目录或具体文件列表
README hello.php

$ git status -s //用来查看当前项目的状态
?? README
?? hello.php
$

//然后使用 添加命令让新建的文件加上去
$ git add README hello.php
$ git status -s //用来查看当前项目的状态
 README
 hello.php
$
//文件修改后，一般需要进行 git add 操作，从而保存历史版本
```



###### 其他;

如果添加某个文件的时候报错，需检查这个文件在当前目录下是否存在。

可以使用`ls`或者`dir`命令来查看当前目录的文件

------



##### **git status**

查看上次提交之后是否对文件进行再次修改，可以帮助我们了解当前仓库的状态，一般要和  **git diff**  配合使用，查看具体的修改



```
$ git status
//使用 -s来获得简短的输出结果
$ git status -s
AM README
A gello.php

//AM状态表示在外面添加到缓存之后又有改动
```

------

git diff

**比较**文件在暂存区和工作区的差异，**显示**写入暂存区和已经被修改但是未写入存储去文件的区别

```
尚未缓存的改动：git diff 文件名字
查看已缓存的改动： git diff --cached
查看已缓存的与未缓存的所有改动： git diff HEAD
显示摘要而非
```



------

##### git log（查看提交历史）

可以查看系统的提交历史记录，配合commit时的**-m“ ”**信息

```
//查看历史提交记录
git log 

//用 --oneline 选项来查看历史记录的简洁的版本
git log --online

//也可以在后面添加 --pretty==online来简化信息

//查看历史中什么时候出现了分支、合并 git log --graph
//逆向显示所有日志 git log --reverse
//查找指定用户的提交日志 git log --author=user--online
//要指定日期，--since 和 --before，也可用 --until 和 --after

git log --online --before={3.week.ago} --after={2010-04-18}--no merges
```



###### 例子：

显示这个版本库的文件提交情况：

```
$ git log
commit e475afc93c209a690c39c13a46716e8fa000c366 (HEAD -> master)
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 21:03:36 2018 +0800

    add distributed

commit eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 20:59:18 2018 +0800

    wrote a readme file
```



------

##### **git reset**  （回退到之前的版本）

```
//语法格式
git reset [--soft | --mixed | --hard] [HEAD]

--mixed 为默认,重置暂存区的文件与上一次的提交(commit)保持一致，工作区文件内容保持不变。可以省略
//比如
$ git reset HEAD^            # 回退所有内容到上一个版本  
$ git reset HEAD^ hello.php  # 回退 hello.php 的文件版本到上一个版本  
$ git  reset  052e           # 回退到指定版本

//因为回退会将现在的信息抹掉，如果又希望回到现在的版本，就需要查找命令窗口的历史信息（只要你没关闭）
找到 commit id
然后 $ git reset --hard commit id
//版本不需要全写，前几位就行

//找不到 commit id怎么办？
git reflog记录了每一次的命令，所以可以使用 git reflog来查找id
```



```
--soft 参数用于回退到某个版本：
$ git reset --soft HEAD~3 
# 回退上上上一个版本
```



```
--hard 参数撤销工作区中所有未提交的修改内容，将暂存区与工作区都回到上一次版本，并删除之前的所有信息提交：
$ git reset –hard HEAD~3  # 回退上上上一个版本  
$ git reset –hard bae128  # 回退到某个版本回退点之前的所有信息。 
$ git reset --hard origin/master    # 将本地的状态回退到和远程的一样 
```

🔺谨慎使用 –hard 参数，它会删除回退点之前的所有信息。

**git reset HEAD**

用来取消已经缓存的内容

![](https://z3.ax1x.com/2021/12/03/oNvjmT.png)

```
//hello.php的修改并未提交，这个时候可以用commit -a将其修改提交
```

✨**HEAD 说明**

| HEAD 表示当前版本      | HEAD~0 表示当前版本   |
| :--------------------- | --------------------- |
| HEAD^ 上一个版本       | HEAD~1 上一个版本     |
| HEAD^^ 上上一个版本    | HEAD^2 上上一个版本   |
| HEAD^^^ 上上上一个版本 | HEAD^3 上上上一个版本 |
| 以此类推...            | 以此类推...           |



------

##### git reflog（查看命令历史）

作用：记录每一次命令，以便确定要回到未来的哪个版本

当使用reset回退到之前的修改版本，可以用reglog找到之前的 `commit id`

然后使用语法:

```
$ git reset --hard [commit id]
```

就可以回到这个id相对应的状态

###### 举例：

```
$ git reflog
e475afc HEAD@{1}: reset: moving to HEAD^
1094adb (HEAD -> master) HEAD@{2}: commit: append GPL
e475afc HEAD@{3}: commit: add distributed
eaadf4e HEAD@{4}: commit (initial): wrote a readme file
```



------

##### git blame

```
//以列表形式显示修改记录，
git blame <file>
```

------

##### git remote

```
git clone url//远程仓库的地址   载入
git remote -v//显示所有远程仓库的信息
git remote show url//显示某个远程仓库的信息
git remote add [shortname] [url]//shortname 为本地的版本库
git remote rm name //删除远程仓库
git remote rename olename newname//修改仓库名
```

------

##### git fetch

```
//远端仓库提取数据并尝试合并到当前分支
git meige

//first,配置好了一个远程仓库，并且你想要提取更新的数据，你可以首先执行
git fetch [alias]//以上命令告诉 Git 去获取它有你没有的数据，然后你可以执行
git merge [alias]//然后在本地更新修改
git fetch origin

```

------

##### **git pull**

用于从远程获取代码并合并本地的版本

```
git pull 
git pull origin

//把远程主机origin的A分支拉过来和本地B的分支合并
git pull origin A:B
//如果是和当前的分支合并
git pull origin A
```

------

##### **git push**

本地的分支版本上传到远程并合并

```
git push <远程主机名> <本地分支名>:<远程分支名>
//如果本地分支名与远程分支名相同，则可以省略冒号:
git push <远程主机名> <本地分支名>

//本地版本与远程版本有差异，但又要强制推送可以使用 --force 参数
git push --force origin master

//删除主机的分支可以使用 --delete 参数,以下命令表示删除 origin 主机的 master 分支
git push origin --delete master
```

------



**git commit**  

 **（快照）**从现有的**暂存区**拷贝到项目**本地仓库**

```
git commit -m[message]
// message 可以是一些备注信息

$ git commit [file1] [file2]...-m[message]
```

###### 说明

git commit命令执行成功后，会告诉你 ：

`x file changed` ：x个文件被改动；

`y insertions`: 插入y行内容



###### 相关语法

🎫**-am**参数设置修改文件后不需要执行 git add命令，直接提交

```
$ git commit -a
```

![](https://z3.ax1x.com/2021/12/02/oNXkX8.png)



也有**另外**简便的方法：

```
git commit -a

//我们先修改 hello.php文件为一下内容
<?php
echo '菜鸟教程：www.runoob.com';
echo '菜鸟教程：www.runoob.com';
?>
//再执行一下命令
$ git commit -am '修改 hello.php 文件'
[master 71ee2cb] 修改 hello.php 文件
 1 file changed, 1 insertion(+)
```



（即省略了，add提交到暂存区，commit提交到本地仓库，直接使用 commit -a实现缓存->提交

------



##### **git rm** 

（暂存区删除文件）

```
//将文件从暂存区和工作区中删除
git rm <file>  

//如果删除之前修改过并且已经放到暂存区域的话，则必须要用强制删除选项 -f
git rm -f <file>

//文件从暂存区域移除，但仍然希望保留在当前工作目录中
git rm --cashed<file>

```

------

##### git mv

```
//用于移动或重命名一个文件、目录或软连接
git mv <file><newfile>

//要重命名它，可以使用 -f 参数
git mv -f <file> <newfile>
```

------

##### **git checkout**.   

（🔺暂存区全部指定文件替换工作区文件）

##### **git clone** 

（从现有的git仓库拷贝项目）

```
命令格式
git clone <repo>
    
如果要克隆到指定的目录，可以使用命令格式
git clone <repo> <directory> 
    
参数说明
repo：git仓库
directory：本地目录
```

![](https://z3.ax1x.com/2021/12/02/oN1V9s.png)



```
git clone [url]
   url 就是我们要拷贝的项目比如拷贝github上的git仓库
   https://github.com/tianqixin/runoob-git-test

拷贝完成后，会在当前目录下生成一个runoob-git-test 目录
通常url最后一个/之后的项目名称就是移植到本地后的名称，如果想要别的名称，可以在该命令的最后加上自己想要的名称
```

------

##### **git config**

 (配置命令,在开始前需要先设置提交的用户信息)

```
$ git config --list
用来显示当前的配置信息
    
$ git config -e
针对当前的仓库
    
$ git config --global 
针对系统上所有的仓库
    
$ git config --global user.name"name"
$ git config --global user.email email@.com
设置提交代码时的用户信息

如果去掉 --global参数只对当前的仓库有效
```

------

##### **git init** 

初始化一个git仓库 ,之后git仓库会生成一个 .git目录

如果想要讲该**目录下几个文件纳入版本控制**，需要使用**git add**，让git对这些文件进行跟踪

```
$ git add *.c
$ git add README
$ git commit -m"初始化项目版本“
    windows系统下 commit说明要用 “”双引号流程
```

比如在当前目录下**创建一个叫做 new 的新项目**

```
$ mkdir new
$ cd new/
$ git init
Tnitialized empty Git repository in /users/../new/.git
    初始化空 git 仓库 完毕
```

.git 默认是隐藏的，可以使用 **ls-a** 命令查看

------

##### cat

```
cat file //把文件内容打印显示

cat file1 file2> target_file //把多个文件合并到目标文件

cat file1 file2>> target_file //把多个文件附加到目标文件
```

##### ✨vim 

打开，修改，保存文件

**一，两种模式： 命令，编辑**

**命令**

接受，执行vim操作命令时的模式，打开文件后的默认模式

**编辑**

按下 **Esc**键，回退命令模式，在命令模式下按 **i**，进入编辑模式

**二，创建，打开文件**

```
touch filename //创建文件  （git mkdir）
vim 文件路径 //打开文件 ，存在则打开，不存在则新建文件
```

**三，保存文件**

在编辑模式下编辑文件（**i**）

按（**Esc**）进入命令模式，在命令模式下键入 **“zz"** 或者 **”wq“**，保存并且退出

如果只是想保存文件 ，**“：w“**

**四，放弃文件修改**

按 “**Esc**”-->"**:q!**"-->"**Enter**"-->退出 vim

如果是放弃所有文件修改但是不退出：

**vi**(回退到文件夹最后一次保存的状态)  --->   **Esc**  --->  "**:e!**"  ---->  **Enter**

**五，查看文件内容**

```
cat 文件名 //git bash窗口实现
```

**六，创建文件夹**

```
touch 文件夹//git bash窗口实现
```

- ------

## 流程

### 创建仓库

| 命令      | 说明                             |
| :-------- | -------------------------------- |
| git init  | 初始化                           |
| git clone | 拷贝一份远程仓库（下载一个项目） |

### 操作与修改

| 命令       | 说明                                   |
| :--------- | -------------------------------------- |
| git add    | 添加文件到仓库                         |
| git status | 查看当前文件的状态，显示有变更的文件   |
| git diff   | 比较文件的不同，即暂存区和工作区的区别 |
| git commit | 提交暂存区到本地仓库                   |
| git reset  | 回退版本                               |
| git rm     | 删除工作区文件                         |
| git mv     | 移动或重命名工作区文件                 |

### 提交日志

| 命令             | 说明                                   |
| :--------------- | -------------------------------------- |
| git log          | 查看历史提交记录                       |
| git blame <file> | 以列表的形式查看指定文件的历史修改记录 |

### 远程操作

| 命令       | 说明                 |
| ---------- | -------------------- |
| git remote | 远程仓库操作         |
| git fetch  | 远程获取代码库       |
| git pull   | 下载远程代码库       |
| git push   | 上传远程代码并且合并 |

#### 远程仓库

利用github托管

## Git分支模型

###### 创建分支命令

```
git branch (branchname)
```

###### 切换分支命令

```
git checkout (branchout)
//Git会用最后提交的快照替换 （commit）替换工作目录的内容
```

###### 合并分支命令

```
git merge
```

![](https://z3.ax1x.com/2021/12/03/odCiwt.png)

###### 列出分支命令

```
git branch
//没有参数，git branch 会列出在本地的分支
```

###### 创建分支

```
//默认情况下，执行git init，系统默认创建一个 master分支
//如果要手动创建 
git branch (branchname)
```

###### 删除分支

```
git branch -d(branch)
```

###### 合并冲突

合并并不仅仅是简单的文件添加、移除的操作，Git 也会合并修改

**基本概念**： Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容

原因：某个文件的内容都被修改和提交

解决：手动修改

```
git status  //告诉我们冲突的文件
//修改
使用 vim cat等命令

//要用 git add告诉Git文件冲突已经解决
//然后 git commit
```





# 注意事项：

windows用户不要使用系统自带的文本编辑器

推荐使用：vs code
