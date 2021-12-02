# git学习笔记

# 12月2

## Git 基本概念

###### 工作流程

- 克隆git资源作为工作目录
- 在克隆的资源上添加或修改文件
- 如果其他人修改了，可以更新资源
- 在提交前查看修改
- 提交修改
- 在修改完成后，如果发现错误，可以撤回提交再次修改并提交

简单说，就是可以copy出副本进行修改，还可以回溯的操作。

###### **基本概念**

- **工作区**（workplace）：在电脑看到的目录
- **暂存区**（staging area）：（ 存放在 .git 目录下的）index文件
- **版本库**（local repository）：工作区有一个隐藏目录 .git ，这个不算工作区，而是git的版本。
- **远程仓库**（remote repository）

 （写代码）工作区--**git add**-->(临时)暂存区--**git commit**-->(历史)版本库

------



## **操作命令**

###### **git add**    

(修改或新增文件到暂存区)

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

------



###### git status

查看上次提交之后是否对文件进行再次修改

```
$ git status
//使用 -s来获得简短的输出结果
$ git status -s
AM README
A gello.php

//AM状态表示在外面添加到缓存之后又有改动
```

------



###### git diff

**比较**文件在暂存区和工作区的差异，**显示**写入暂存区和已经被修改但是未写入存储去文件的区别

```
尚未缓存的改动：git diff
查看已缓存的改动： git diff --cached
查看已缓存的与未缓存的所有改动： git diff HEAD
显示摘要而非
```

------



###### **git pull**

###### **git push**

###### **git commit**  

 从现有的git仓库（暂存区）拷贝到项目（本地仓库）

```
git commit -m[message]
// message 可以是一些备注信息

$ git commit [file1] [file2]...-m[message]
```

🎫**-a**参数设置修改文件后不需要执行 git add命令，直接提交

```
$ git commit -a
```

![](https://z3.ax1x.com/2021/12/02/oNXkX8.png)

也有另外简便的方法：

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

（即省略了，add创建，commit提交，直接使用 commit -a实现缓存->提交

------



###### **git reset**  

(重写操作)

```
//语法格式
git reset [--soft | --mixed | --hard] [HEAD]

--mixed 为默认,重置暂存区的文件与上一次的提交(commit)保持一致，工作区文件内容保持不变。可以省略
//比如
$ git reset HEAD^            # 回退所有内容到上一个版本  
$ git reset HEAD^ hello.php  # 回退 hello.php 文件的版本到上一个版本  
$ git  reset  052e           # 回退到指定版本

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

###### **git rm** 

（暂存区删除文件）

###### **git checkout**.   

（🔺暂存区全部指定文件替换工作区文件）

###### **git clone** 

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



###### **git config**

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



###### **git init** 

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



###### ✨vim 

打开，修改，保存文件



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

