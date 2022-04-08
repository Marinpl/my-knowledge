>
>
>## **Linux基础指令**
>

## Linux

```bash
#清屏 
$ clear

#初始化终端
$ reset

#退出 
$ exit

#历史
$ history

#改变目录
$ cd (~/./../路径)

#显示当前路径
$ pwd

#创建文件
$ touch xxx.html /  xxx.xxx

#删除文件
$ rm xxx.xxx

#移动文件
$ mv 相关文件 至相关文件夹 ...   (保证在同一目录下)

#创建文件夹
$ mkdir xxx

#删除文件夹
$ rm -r  / rm -r xxx
```

>
>
>## git基础指令
>

## Git

#### 0.基础知识

git仓库拥有四个区域（工作区、暂存区、本地仓库区[HEAD指向最新放入仓库的版本]、远程仓库区）

上传命令 : add、commit 、push、commit -a	

下载命令 : pull、fetch

合并命令 : merge、rebase

切换命令 : checkout

#### 1.新建git项目

[init,clone]

```bash
# 本地创建或新建一个目录，初始化git库
$ git init or git init [project-name]

# 从远程仓库下载
$ git clone [url]
```

#### 2.查询配置

[config]

```bash
# 显示当前配置
$ git config --list

# 编辑git配置文件(.gitconfig)
$ git config [--global]

# 设置提交代码的用户信息
$ git config [--global] user.name "[name]"
$ git config [--global] user.email "[email address]"
```

#### 3.添加、删除文件

[add,rm,mv]

```bash
# 添加指定文件到暂存区
$ git add [file1] [file2] ...

# 添加指定目录到暂存区，包括子目录
$ git add [dir]

# 添加当前目录的所有文件到暂存区
$ git add .

# 添加每个变化前，都会要求确认
# 对于同一个文件的多处变化，可以实现分次提交
$ git add -p

# 删除工作区文件，并且将这次删除放入暂存区【或】停止追踪指定文件，但该文件会保留在工作区
$ git rm [file1] [file2] ... 【or】git rm --cached [file]

# 改名文件，并且将这个改名放入暂存区
$ git mv [file-original] [file-renamed]
```

#### 4.代码本地提交

[commit]

```bash
# 提交暂存区文件【或】指定文件至仓库区  [直接commit启动文本编辑器以便输入本次提交的说明,i = insert ,ESC,:wq]
$ git commit -m[message] 【or】 git commit [file1] [file2] ... -m[message] 

# 提交工作区自上次commit之后的变化，直接到仓库区
$ git commit -a

# 提交时显示所有diff信息
$ git commit -v

# 重做上一次commit，并包括指定文件的新变化
$ git commit --amend [file1] [file2] ...

```

#### 5.分支(新建，删除，切换，合并)

[branch,checkout]

```bash
# 列出分支(远程分支、本地分支、本地和远程分支、最后一次提交)
$ git branch -r/ /-a/-v

# 查看本地分支对应的远程分支 以及版本是否提前或落后(查看一个分支的最后一次提交)
$ git branch -vv

# 新建一个分支，但依然停留在当前分支【或】切换到该分支【或】指向指定commit
$ git branch [branch-name] 【or】 git checkout -b [branch] 【or】 git branch [branch] [commit]

# 删除分支【或】删除远程分支
$ git branch -d [branch-name] 【or】git branch -dr [remote-branch]

# 切换到指定分支，并更新工作区
$ git checkout [branch-name]

# 切换到上一个分支
$ git checkout -

# 合并指定分支到当前分支【或】选择一个commit，合并进当前分支
$ git merge [branch] 【or】 git cherry-pick [commit]
$ git rebase [startpoint] [endpoint] --onto [branchName]

# 查看哪些分支合并或没合并到当前分支
$ git branch --merged 【or】git branch --no--merged
```

#### 6.远程同步本地

[fetch,remote,push,pull = fetch + merge]

```bash
# 下载远程仓库的所有变动
$ git fetch [remote]

# 将远程分支更新到本地【或】将远程分支更新到本地，删除远程已删除的分支
$ git fetch【or】git fetch -p

# 显示所有远程仓库【或】某个仓库信息
$ git remote -v 【or】git remote show [remote]

# 新建远程仓库
$ git remote add [shortName] [url]

# 获取远程仓库的变化，并与本地分支合并
$ git pull [remote] [branch]
#ex: git pull origin master 

# 推送到远程仓库
# 强制推送 在push后使用 --force 参数
# 删除主机的分支 在push后使用使用 --delete 参数
# 如果本地分支名与远程分支名相同，则可以只写一个，省去冒号
$ git push [remote] [local-branch]:[remote-branch]

```

#### 7. 标签tag

[tag]

```bash
# 列出所有tag【或】新建tag在指定commit
$ git tag 【or】git tag [tag-name] [commit]

# 删除本地tag
$ git tag -d [tag]

# 删除远程tag
$ git push origin :refs/tags/[tag-name]

# 提交指定tag【或】提交所有tag
$ git push [remote] [tag] 【or】git push [remote] --tags

# 新建分支，指向tag
$ git checkout -b [branch] [tag]

```

#### 8. 撤销操作

[reset,revert]

```bash
# 本地撤销
$ git reset HEAD^[~1]

# 多人情况下的撤销，告知他人有撤销(就是新提交一次，与撤销前完全相同)
$ git revert HEAD^^
```



#### 9.实际操作中的问题

##### 1、 理解本地仓库和远程仓库

​	即使你更改了本地文件，但你并没有提交最新版本至本地仓库，push也是原先版本。

##### 2、分支与标签区别

​	tag用于版本控制，tag对应某次commit, 是一个点，是不可移动的。

​	commit用于代码改变，branch 对应一系列commit，是很多点连成的一根线，有一个HEAD 指针，是可以依靠 HEAD 指针移动的。
