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



## Git

 <img alt="Relative date" src="https://img.shields.io/date/1651828182?color=green&label=Update&style=for-the-badge">

#### 本次更改重点：

- rebase 与 cherry-pick区别
- push与fetch后的一些参数
- 完善一些模糊概念

#### 0.基础知识

git仓库拥有四个区域（工作区、暂存区、本地仓库区[HEAD指向最新放入仓库的版本]、远程仓库区）

上传命令 : add、commit 、push、commit -a	

下载命令 : pull、fetch

合并命令 : merge、rebase

切换分支、向下复制命令 : checkout

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

# 特殊，有版本号的文件可以直接进行提交
$ git checkout <commit> filename 
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

#### 5.分支(新建，删除，切换，合并，移动)

[branch,checkout]

```bash
# 列出分支(远程分支、本地分支、本地和远程分支、最后一次提交)
$ git branch -r/ /-a/-v

# 查看本地分支对应的远程分支 以及版本是否提前或落后(查看一个分支的最后一次提交)
$ git branch -vv

# 新建一个分支，但依然停留在当前分支【或】新建分支，切换到该分支【或】新建分支，指向指定commit,但依然停留在当前分支
$ git branch [branch-name] 【or】 git checkout -b [branch] 【or】 git branch [branch] [commit]

# 新建分支，指向tag
$ git checkout -b [branch] [tag]

# 分支重命名
$ git branch -m [old-branch-name] [new-branch-name] 

# 删除分支【或】删除远程分支
$ git branch -d [branch-name] 【or】git branch -dr [remote-branch]

# 切换到指定分支，并更新工作区
$ git checkout [branch-name]

# 切换到上一个分支
$ git checkout -

# 合并指定分支到当前分支【或】选择一个commit，合并进当前分支
$ git merge [branch] 【or】 git cherry-pick [commit]

# 使用rebase合并(合并前HEAD指针指向后面的分支)
$ git rebase [start-branch] [end-branch]
#ex1: 将test分支合并至master
$ git rebase master test 

# 查看哪些分支合并或没合并到当前分支
$ git branch --merged 【or】git branch --no--merged

# 移动分支
$ git branch -f [branch] <commit>
```

#### 6.远程同步

[fetch,remote,push,pull]

```bash
# 下载远程仓库的所有变动，不会更新本地的非远程分支
$ git fetch [remote]

# 将远程分支更新到本地【或】将远程分支更新到本地，删除远程已删除的分支
$ git fetch【or】git fetch -p

# 显示当前文件的所有远程仓库【或】某个仓库信息
$ git remote -v 【or】git remote show [remote]

# 新建远程仓库连接
$ git remote add [remote-name] [url]

# 获取远程仓库的变化，并与本地分支合并
# pull 相当于 fetch + (merge/rebase)
$ git pull [remote] [branch]
#ex1: 
$ git pull origin master === git fetch origin master ; git merge origin master
#ex2: 
$ git pull --rebase origin master === git fetch origin master ; git rebase origin master

# 推送到远程仓库
# 强制推送 在push后使用 --force 参数
# 删除主机的分支 在push后使用使用 --delete 参数
# 如果本地分支名与远程分支名相同，则可以只写一个，省去冒号
# push其实分为两步，第一步是确认本地仓库中的分支名，第二步是对比远程仓库的分支名中文件，将没有或更改的上传,可以使用相对引用。
$ git push [remote] [source]:[destination]

```

#### 7. 标签tag

[tag]

```bash
# 列出所有tag【或】在指定commit新建tag
$ git tag 【or】git tag [tag-name] [commit]
#ex: 
$ git tag v1.0 [commit]

# 删除本地tag
$ git tag -d [tag]

# 删除远程tag
$ git push origin :refs/tags/[tag-name]

# 提交指定tag【或】提交所有tag
$ git push [remote] [tag] 【or】git push [remote] --tags

```

#### 8. 撤销操作

[reset,revert]

```bash
# 本地撤销
# 在reset后添加--hard/--soft 会使工作区也更新/都不更新
$ git reset HEAD^[~1] 

# 没有分支名和文件名，只使用HEAD或什么都不写，分支指向不变，但是索引会回滚到最后一次提交，也可使用--hard
$ git reset

# 切换至当前文件，只有暂存区复制索引被更新
$ git reset [file-name]

# 多人情况下的撤销，告知他人有撤销(就是新提交一次，与撤销前完全相同)
$ git revert HEAD^^
```

#### 9. 其他操作

[移动提交记录,查看当前状态]

```bash
# 在当前head指针下复制其他分支提交
$ git cherry-pick [other-branch-name] [other-branch-name]...

# 当不知道提交记录的hash值时，使用交互式 rebase -i 
$ git rebase -i HEAD~3

# 查看状态
$ git status
```

#### 10.实际操作中的问题

##### 0、checkout与分离HEAD

- ​	checkout可用于切换分支.

  ​	如切换到分支**test** :`git checkout test`

- ​	当用于没有版本号的文件时，会将工作区的指定文件的内容恢复到暂存区的状态。

  ​	如：`git checkout test.txt`以及`git checkout . `

- ​	当用于有版本号的文件时，表示将工作区和暂存区都恢复到版本库指定提交版本的指定文件的状态，此时HEAD指针不变，此时的   状态相当于把工作区的内容修改到指定版本的文件内容后，再把修改的内容添加到暂存区

​		   如哈希值为**c0ef2**提交的**abc.txt**：`git checkout c0ef2 abc.txt`

- ​	当不指定文件名和分支名(而是一个标签、远程分支、SHA-1值或者是像*分支名~3*类似的东西)，会得到一个匿名分支，也称为分离HEAD，能很方便地在历史版本之间互相切换。

  - 在分离HEAD提交操作可以正常进行，但是不会更新任何已命名的分支，且此后你切换到别的分支，比如说*main*，那么这个提交节点（可能）再也不会被引用到，然后就会被丢弃掉了。

    如果想要保持这个分离状态，使用`git checkout -b [branch-name]`

##### 1、 理解本地仓库和远程仓库

​	即使你更改了本地文件，但你并没有提交最新版本至本地仓库，push也是原先版本。

##### 2、分支tag与标签commit区别

​	tag用于版本控制，tag对应某次commit, 是一个点，是不可移动的。

​	commit用于代码改变，branch 对应一系列commit，是很多点连成的一根线，有一个HEAD 指针，是可以依靠 HEAD 指针移动的。

##### 3、merge、rebase、cherry-pick区别

​	**指针区别：**

​	merge 会将**所选分支**合并在**当前HEAD指针分支**的后面，合并分支名是所选分支，有个菱形关系。

​	rebase 会合并在**所选分支或第一个分支**的后面，合并分支名是初始分支。

​	**概念区别：**

​	cherry-pick 只是复制提交，选择的节点提交了什么就提交什么。注意不要使用HEAD上游提交。

​	rebase 是线性化的自动的cherry-pick多用于集成 一般用于合成master分支，会将其复制并移动到所选分支上，所以尽量不要在指向master分支情况上使用rebase其他分支。

​	merge 其实是合并该分支基于共同祖先的更改 ，所以尽量避免两个文件都有更新时进行merge，会有冲突。

​	

​	rebase： 使用`rebase -i [相对引用or提交名or分支名]` 打开一个文本编辑器，可以复制操作树 并重新手动调多个文件的顺序，

​					 **相对引用是往上获取，提交名或分支名是往下获取**

##### 4、相对引用操作

​	一般情况，我们会添加数字修改符(HEAD)，例如`git checkout master HEAD^`，即指针返回master且往上移动一次。

​	如果我们直接使用，`git checkout master^`，会回到父级提交记录。

​	在合并提交情况下，`"^"`代表指合并的正上方父级记录，`"^2"`代表另外一个父提交，`"~[数字]"`还是一样。

​	可以使用链式操作，如`git checkout master~^2~2`

##### 5、设置远程分支

一般情况下本地与远程分支的关联关系就是由分支的“remote tracking”属性，**例如**本地master分支会跟踪远程仓库的master(或者说origin master)分支，使得pull或push可以进行交互。

如果想要其他分支跟踪，使用下面两条指令都可以实现：

`git checkout -b [branch-name] o/master`

`git branch -u o/master [branch-name]`

