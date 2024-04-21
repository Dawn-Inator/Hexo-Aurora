---
title: Basic Usage of Git
categories: Tech
cover: /imgs/default.jpg
abstracts: git
tags:
 - git
---

:::tip
Git 的工作就是创建和保存你项目的快照及与之后的快照进行对比。
:::

**Git 常用的命令有**
```
git clone   克隆仓库内容

git push   推送到远程仓库

git add   向本地仓库中添加文件

git commit   提交工作区内容到版本库

git checkout   切换分支

git pull   从远程仓库拉取内容到工作台
```

它们之间的关系可以用一张图片展示出来，如下：
在这里插入图片描述

![](/imgs/Basic-Usage-of-Git/ea247cfe7da1445792e5d83469a5e2cc.png)

说明
- workspace — 工作区
- staging area — 暂存区/缓存区
- local repository — 版本库或本地仓库
- remote repository — 远程仓库

## 1、本地仓库的操作指令
简单的操作指令如下：
```
git init   初始化仓库。该命令执行完后会在当前目录生成一个 .git 目录，所有 Git 需要的数据和资源都存放在这个目录中。

git add .   添加文件到暂存区。如果当前目录下有几个文件想要纳入版本控制，需要先用 git add 命令告诉 Git 开始对这些文件进行跟踪，然后提交。

git commit   将暂存区的内容提交到本地仓库。所有的更新都会被提交，包括文件、内容更改等。
```
## 2、仓库的远程操作
### 2.1、远程仓库操作
**git remote 命令用于在远程仓库的操作。**

- 显示所有远程仓库：
  
```
git remote -v
```

- 添加远程版本库：
  
```
git remote add [别名] [url 地址]
```

- 删除远程仓库
  
```
git remote rm name
```

- 修改仓库名
  
```
git remote rename old_name new_name
```

### 2.2、从远程仓库获取项目
```
git clone [项目地址]
git pull  [项目地址]
git fetch [项目地址]
git merge [目标地址]/[分支]
```
```
git clone   从远程库中克隆项目到本地，是一个包含整个项目的版本库文件夹。该命令通常用于新用户 clone 项目，熟练之后基本都是用 git pull直接拉取项目。

git pull   从远程仓库下载代码并合并到本地仓库中。

git fetch   从远程仓库获取最新的更新内容（即本地没有的数据）。

git merge   将远程仓库上的所有更新内容（假设已经被推送到服务器了）合并到你的当前分支。
```

### 2.3、上传项目到远程仓库
- 从将本地的分支版本上传到远程并合并可以使用 git push，如下：
  
```
git push <远程主机名> <本地分支名>:<远程分支名>
```

- 如果本地分支名与远程分支名相同，可以省略冒号：
  
```
git push <远程主机名> <本地分支名>
```

- 如果本地版本与远程版本有差异，但又要强制推送可以使用 --force 参数
  
```
git push --force origin master
```

- 删除主机的分支可以使用 --delete 参数，以下命令表示删除 origin 主机的 master 分支：
  
```
git push origin --delete master
```

## 3、其他的指令
### 3.1、查看配置信息
```
git config --list
```
### 3.2、查看仓库状态
- git status 命令用于查看在你上次提交之后是否有对文件进行再次修改。
  
```
git status
```

### 3.3、删除版本库中的文件
```
git rm  xxx.txt
```
- *注意：这个命令使用了之后，要 git commit -m “xxx”之后才算是真正的删除了。*

- *如果删除之前修改过并且已经放到暂存区域的话，则必须要用强制删除选项 -f。*
  
```
git rm -f xxx
```

- 如果想把文件从暂存区域移除，但仍然希望保留在当前工作目录中，即从跟踪清单中删除，使用 --cached 选项即可：
  
```
git rm --cached <file>
```

### 3.4、查看文件中修改了的内容
```
git diff xxx.txt   比较当前工作空间与staging area,查看工作空间的变化

git diff --cached   比较staging area与本地仓库,查看暂存区中变化
  
git diff HEAD   比较当前工作空间与本地仓库
    
git diff newbranch   比较当前工作空间与newbranch分支
      
git diff tag1 tag2   比较tag1与tag2
        
git diff tag1:file1 tag2:file2   比较tag1的file1与tag2的file2
          
git diff tag1 tag2 file   比较tag1与tag2的file文件
            
git diff --stat   统计有差异的文件个数
```

### 3.5、查看历史记录

**git log**
```
git log   查看全部提交日志

git log -5   查看最近5次的提交日志

git log –p   查看所有提交日志及修改的内容

git log –p --author=“scott”   查看所有scott提交日志及修改内容

git log --since=“2011-05-24”   查看2011-05-24以后所有的提交日志

git log --graph   查看提交日志，以图形方式显示

git log --since=“2 days ago”   查看这两天的提交日志

git log --until=“2011-05-25”   查看截止2011-05-25所有的提交日志

git log --name-only   查看所有修改过的文件

git log --pretty=oneline   查看提交日志，一行显示

git log --pretty=format:%h:%s   查看提交日志，显示sha1及提交comments
```

### 3.6、还原文件（回退）

- git revert和git reset的区别
  
```
git revert   是撤销某次操作，此次操作之前的commit都会被保留

git reset   是撤销某次提交，但是此次之后的修改都会被退回到暂存区

git reset --hard   取消commit，取消add，取消源文件修改

git reset --soft   取消commit

git reset --mixed   取消commit，取消add，是默认模式

git reset --hard HEAD   恢复到HEAD状态

git reset --hard HEAD^   彻底撤销最近一次提交

git reset --hard HEAD~3   彻底撤销最近3次提交

git reset  --soft HEAD~3   撤销最近3次commit,恢复到index状态，并且工作空间文件内容不变

git reset HEAD filename   删除暂存的文件

git revert   撤销某次提交，此次操作之前的commit都会被保留，但撤销也会作为一次提交进行保存。

git commit --amend   修改最后一次提交。
如果上次提交时遗漏了文件，可以在提交后将文件加入缓存然后用该命令提交即可。
如果缓存中内容没有任何修改，只更新修改的提交注释。
```


- 回退版本之后，如果推送远程库是发生错误信息时可以用：
  
```
git push -f [ ] [ ]	强推上去
```

## 4、分支管理指令
*几乎所有的版本控制系统都可以支持分支。使用分支意味着你可以从开发主线上分离开来，然后在不影响主线的情况下继续开展你自己的工作。*

### 4.1、创建分支：
```
git branch (branchname)

git checkout -b (branchname)  //创建新分支并立即切换到该分支下

git switch -c (branchname) //git switch为新版本语句，更加推荐
```


### 4.2、切换分支:
```
git checkout (branchname)

git switch (branchname)
```

- 当你切换分支的时候，Git 会用该分支的最后提交的快照替换你的工作目录的内容， 所以多个分支不需要多个目录。

### 4.3、合并分支命令:
```
git merge 
```
- 你可以多次合并到统一分支， 也可以选择在合并之后直接删除被并入的分支。

### 4.4、列出分支
- 列出分支基本命令
  
```
git branch
```
- 没有参数时，git branch 会列出你在本地的分支。
  
```
$ git branch
* master
```

- 这里的意思是：有一个叫做 master 的分支，并且该分支是当前分支.

- 注意：当你执行 git init 的时候，默认情况下 Git 就会为你创建 master 分支。

### 4.5、分支合并
- 一旦某分支有了独立内容，你最终会希望将它合并回到你的主分支。 你可以使用以下命令将任何分支合并到当前分支中去：
  
```
git merge [分支名]
```

### 4.6、删除分支

- 合并完后就可以删除分支
  
```
$ git branch -d newtest
Deleted branch newtest (was c1501a2).
```

- 删除后， 就只剩下 master 分支了：
  
```
$ git branch
* master
```
