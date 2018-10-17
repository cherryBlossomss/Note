# Git和GitHub

## 1，版本控制工具应该具备的功能

* 协同修改
  * 多人并行不悖的修改服务器的同一文件
* 数据备份
  * 不仅保存目录和文件的当前状态，还保存每一个提交过的历史状态
* 版本管理
  * 在保存每一个版本的文件信息时做到不保存重复数据，以节约存储空间，提高运行效率。这方面==SVN采用的是增量式管理==的方式，而==Git采用了文件系统快照==的方式；
* 权限控制
  * 对团队中参与的开发人员进行权限控制；
  * 对团队外开发者贡献的代码进行审核--Git独有；
* 历史记录
  * 查看修改人，修改时间，修改内容，日志信息
  * 将本地文件恢复到某一个历史状态
* 分支管理
  * 允许开发团队在工作过程中多条生产线同时推进任务，进一步提高效率

## 2.关于版本控制

​    什么是版本控制？我为什么要关心它呢？版本控制是一种记录一个或若干文件内容变化，以便将来查阅特定版本修订情  况的系统。在本书所展示的例子中，我们仅对保存着软件源代码的文本文件作版本控制管理，但实际上，你可以对任何类型的文件进行版本控制。

### 2.1本地版本控制系统

  许多种本地版本控制系统，大多都是采用某种简单的数据库来记录文件的历次更新差异![local](D:\笔记\pictures\TIM截图20181016101759.png)

### 2.2集中化的版本控制系统

接下来人们又遇到一个问题，如何让在不同系统上的开发者协同工作？于是，集中化的版本控制系统（ Centralized Version Control Systems，简称 CVCS ）应运而生。这类系统，诸如 CVS，Subversion 以及 Perforce 等，都有一个单一的集中管理的服务器，保存所有文件的修订版本，而协同工作的人们都通过客户端连到这台服务器，取出最新的文件或者提交更新。多年以来，这已成为版本控制系统的标准做法。**缺点是：服务器若宕机，则无法恢复之前的所有**(**单点故障)**![](D:\笔记\pictures\TIM截图20181016101923.png)

### 2.3分布式版本控制系统

分布式版本控制系统（ Distributed Version Control System，简称 DVCS ）面世了。在这类系统中，像 Git，Mercurial，Bazaar 以及 Darcs 等，客户端并不只提取最新版本的文件快照，而是把代码仓库完整地镜像下来。这么一来，任何一处协同工作用的服务器发生故障，事后都可以用任何一个镜像出来的本地仓库恢复。因为每一次的提取操作，实际上都是一次对代码仓库的完整备份

![](D:\笔记\pictures\TIM截图20181016102338.png)

## 3.Git

### 3.1Git结构

![](D:\笔记\pictures\TIM截图20181016104324.png)

### 3.2Git和代码托管中心

 代码托管中心的使命：维护远程库

* 局域网环境下
  * GitLab服务器
* 外网环境下
  * GitHub
  * 码云

### 3.3本地库和远程库的交互

团队内

![](D:\笔记\pictures\TIM截图20181016105453.png)

团队外

![](D:\笔记\pictures\TIM截图20181016105841.png)

### 3.4Git命令行操作

#### 3.4.1本地库初始化

* 命令：git init

* 效果：

  ```shell
  user@TQ MINGW64 /d/笔记/weChat
  $ git init   #Create an empty Git repository or reinitialize an existing one
  Initialized empty Git repository in D:/笔记/weChat/.git/
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ ls
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ ll -a
  total 8
  drwxr-xr-x 1 user 197610 0 10月 16 11:20 ./
  drwxr-xr-x 1 user 197610 0 10月 16 11:19 ../
  drwxr-xr-x 1 user 197610 0 10月 16 11:20 .git/
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ ls .git/
  config  description  HEAD  hooks/  info/  objects/  refs/
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ ls
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ ll .git/  #新建一个.git目录
  total 7
  -rw-r--r-- 1 user 197610 130 10月 16 11:20 config
  -rw-r--r-- 1 user 197610  73 10月 16 11:20 description
  -rw-r--r-- 1 user 197610  23 10月 16 11:20 HEAD
  drwxr-xr-x 1 user 197610   0 10月 16 11:20 hooks/
  drwxr-xr-x 1 user 197610   0 10月 16 11:20 info/
  drwxr-xr-x 1 user 197610   0 10月 16 11:20 objects/
  drwxr-xr-x 1 user 197610   0 10月 16 11:20 refs/
  
  ```

* 注意：.git存放的是本地库相关的文件和子目录，不要随意修改

#### 3.4.3设置签名

* 为了区分不同开发人员

* 命令

  * 项目/仓库级别：仅在本地库有效

    * 命令：git ==config== user.name tony 
    * ​          git ==config== user.email 1524037538_pro@qq.com
    * 信息保存在：.git/config文件夹

  * 系统用户级别：所登陆的操作系统的用户范围

    * 命令：git ==conifg --global== user.name tony 
    * ​          git c==onfig  -global== user.email 1524037538_pro@qq.com

  * 优先级

    * 就近原则：项目级别优先于系统用户级别，两者都存在时，采用项目级别

    * 只有系统用户就采用系统用户的

      ```shell
      user@TQ MINGW64 /d/笔记/weChat (master)
      $ cat .git/config
      [core]
              repositoryformatversion = 0
              filemode = false
              bare = false
              logallrefupdates = true
              symlinks = false
              ignorecase = true
      [user]
              name = tony
              email = 1524037538_pro@qq.com
      
      ```


#### 3.4.3Git添加提交以及查看状态操作

* git add  文件（添加）

* git  commit  -m “提交信息”  文件

  ```shell
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git status #查看状态
  On branch master
  
  No commits yet
  
  nothing to commit (create/copy files and use "git add" to track)
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ vim good.txt
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ cat good.txt
  今天天气阴，心情有点沉重，不过在用途感觉环视挺好的，加油
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git status
  On branch master
  
  No commits yet
  
  Untracked files:
    (use "git add <file>..." to include in what will be committed)
  
          good.txt
  
  nothing added to commit but untracked files present (use "git add" to track)
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git add good.txt  #添加文件到缓存区
  warning: LF will be replaced by CRLF in good.txt.
  The file will have its original line endings in your working directory.
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git status
  On branch master
  
  No commits yet
  
  Changes to be committed:
    (use "git rm --cached <file>..." to unstage)
  
          new file:   good.txt
  
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git rm --cached good.txt
  rm 'good.txt'
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git status
  On branch master
  
  No commits yet
  
  Untracked files:
    (use "git add <file>..." to include in what will be committed)
  
          good.txt
  
  nothing added to commit but untracked files present (use "git add" to track)
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git add good.txt
  warning: LF will be replaced by CRLF in good.txt.
  The file will have its original line endings in your working directory.
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git status
  On branch master
  
  No commits yet
  
  Changes to be committed:
    (use "git rm --cached <file>..." to unstage)
  
          new file:   good.txt
  
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git commit good.txt  #提交文件
  warning: LF will be replaced by CRLF in good.txt.
  The file will have its original line endings in your working directory.
  [master (root-commit) a68c2f6] My first new file create finash
   1 file changed, 1 insertion(+)
   create mode 100644 good.txt
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git add
  Nothing specified, nothing added.
  Maybe you wanted to say 'git add .'?
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ vim good.txt
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git status
  On branch master
  Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)
  
          modified:   good.txt
  
  no changes added to commit (use "git add" and/or "git commit -a")
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git add
  Nothing specified, nothing added.
  Maybe you wanted to say 'git add .'?
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git add good.tst
  fatal: pathspec 'good.tst' did not match any files
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git add good.txt
  warning: LF will be replaced by CRLF in good.txt.
  The file will have its original line endings in your working directory.
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git status
  On branch master
  Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
  
          modified:   good.txt
  
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git commit -m "my second commit" good.txt
  error: pathspec 'my second commit' did not match any file(s) known to git.
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git commit -m m "my second commitsdsd" good.txt
  error: pathspec 'my second commitsdsd' did not match any file(s) known to git.
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git commit -m "my second commitsdsd" good.txt
  warning: LF will be replaced by CRLF in good.txt.
  The file will have its original line endings in your working directory.
  [master 2d8f770] my second commitsdsd
   1 file changed, 1 insertion(+)
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ cat good.txt
  今天天气阴，心情有点沉重，不过在用途感觉环视挺好的，加油
  fdsfsdfdfdfdf
  
  ```

  #### 

  日志查看:git log

  ```shell
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git log  #查看日志
  commit 2d8f770aa87ca85f4db69dc4f3ea9ccead33aff0 (HEAD -> master)  #版本号（指针）
  Author: cherryBlossomss <2712827632@qq.com> #签名（）
  Date:   Tue Oct 16 11:50:30 2018 +0800 #提交时间
  
      my second commitsdsd #提交注释
  
  commit a68c2f6409eaab756a9988561a513cd822e163be
  Author: cherryBlossomss <2712827632@qq.com>
  Date:   Tue Oct 16 11:38:39 2018 +0800
  
      My first new file create finash
  
  ```

  显示在一行： git log --pretty=oneline

  ```shell
  $ git log --pretty=oneline #显示在一行
  1b512bd8a4d321c187109d427aa1265c462a8fa8 (HEAD -> master) nine commit
  036e09cef3837ac350c1526cbc691f014e135d79 eight commit
  6631acd0a14925091305b5056b577a929bdf93b6 seven commit
  dbd273c71a95172112793d92f93830abf56605bf six commit
  7c21d28ffaebfee752446c5d42f0d37ae9075b15 five commit
  92354ff99593d36766e6ef8679d3b70479650ed3 Forth commit
  2fee977847c0cff5168f552d090ea8c062034a83 third commit
  f075309419179493d96fb9ed58202ce2ccb305a2 m
  2d8f770aa87ca85f4db69dc4f3ea9ccead33aff0 my second commitsdsd
  a68c2f6409eaab756a9988561a513cd822e163be My first new file create finash
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git log --oneline #简约显示在一行
  1b512bd (HEAD -> master) nine commit
  036e09c eight commit
  6631acd seven commit
  dbd273c six commit
  7c21d28 five commit
  92354ff Forth commit
  2fee977 third commit
  f075309 m
  2d8f770 my second commitsdsd
  a68c2f6 My first new file create finash
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git reflog #有指针的显示
  1b512bd (HEAD -> master) HEAD@{0}: commit: nine commit
  036e09c HEAD@{1}: commit: eight commit
  6631acd HEAD@{2}: commit: seven commit
  dbd273c HEAD@{3}: commit: six commit
  7c21d28 HEAD@{4}: commit: five commit
  92354ff HEAD@{5}: commit: Forth commit
  2fee977 HEAD@{6}: commit: third commit
  f075309 HEAD@{7}: commit: m
  2d8f770 HEAD@{8}: commit: my second commitsdsd
  a68c2f6 HEAD@{9}: commit (initial): My first new file create finash
  
  ```

#### 3.4.4前进后退版本

基于索引值  git reset --hard  【索引】

```shell
user@TQ MINGW64 /d/笔记/weChat (master)
$ git reset --hard a68c2f6  #后退到初始版本
HEAD is now at a68c2f6 My first new file create finash

user@TQ MINGW64 /d/笔记/weChat (master)
$ cat good.txt #初始版本的内容
今天天气阴，心情有点沉重，不过在用途感觉环视挺好的，加油

user@TQ MINGW64 /d/笔记/weChat (master)

```

使用^符号：只能后退   git reset --hard  HARD^^^

```SHELL
user@TQ MINGW64 /d/笔记/weChat (master)
$ git log --oneline
1b512bd (HEAD -> master) nine commit
036e09c eight commit
6631acd seven commit
dbd273c six commit
7c21d28 five commit
92354ff Forth commit
2fee977 third commit
f075309 m
2d8f770 my second commitsdsd
a68c2f6 My first new file create finash

user@TQ MINGW64 /d/笔记/weChat (master)
$ git reset --hard  HARD^^^ #后退三个版本（相当于git reset --hard  HARD~3）
fatal: ambiguous argument 'HARD^^^': unknown revision or path not in the working tree.
Use '--' to separate paths from revisions, like this:
'git <command> [<revision>...] -- [<file>...]'

user@TQ MINGW64 /d/笔记/weChat (master)
$ git reset --hard  HEAD^^^
HEAD is now at dbd273c six commit


```

注：

reset三个参数的比较

* --soft 只在本地库移动指针
* --mixed 本地库移动指针+重置暂存区
* --hard  本地库移动指针  +重置暂存区+重置工作区

#### 3.4.5 删除文件

rm 【文件】

```shell
$ ll
total 2
-rw-r--r-- 1 user 197610  14 10月 16 14:22 good,txt
-rw-r--r-- 1 user 197610 273 10月 16 14:01 good.txt

user@TQ MINGW64 /d/笔记/weChat (master)
$ rm  good,txt #删除文件

user@TQ MINGW64 /d/笔记/weChat (master)
$ ll
total 1
-rw-r--r-- 1 user 197610 273 10月 16 14:01 good.txt

user@TQ MINGW64 /d/笔记/weChat (master)
```

#### 3.4.5 比较文本差异

```shell
$ git diff apple.txt #比较不同版本（工作区的文件和暂存区的文件进行比较）
warning: LF will be replaced by CRLF in apple.txt.
The file will have its original line endings in your working directory.
diff --git a/apple.txt b/apple.txt
index 2375f2d..b419b1d 100644
--- a/apple.txt
+++ b/apple.txt
@@ -1,5 +1,5 @@
 apple
-apple @@@@@@@@@@@@@@@@@@!!!!!!!!!!!!!!!!!!!!!!!
+apple @@@@@@@@@@@@@@@@@@
 apple
 apple
 
 user@TQ MINGW64 /d/笔记/weChat (master)
$ git diff HEAD~3 apple.txt #与上三个版本比较
diff --git a/apple.txt b/apple.txt
new file mode 100644
index 0000000..b419b1d
--- /dev/null
+++ b/apple.txt
@@ -0,0 +1,5 @@
+apple
+apple @@@@@@@@@@@@@@@@@@
+apple
+apple
+


```

### 3.5Git分支

![](D:\笔记\pictures\TIM截图20181016151319.png)

分支的好处

* 同时，并行推进多个分的开发，提高开发效率
* 如果有分支开发失败，直接删除即可，不会对其他分支造成影响

#### 3.5.1分支操作

* 查看当前分支 git branch -v

```shell
$ git branch -v
* master d3b585b commit Third git diff HEAD apple.txt
```

* 创建分支 git branch 【分支名】

  ```shell
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git branch -v
  * master d3b585b commit Third git diff HEAD apple.txt
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git branch host-fix  #创建分支 host-fix
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git branch -v
    host-fix d3b585b commit Third git diff HEAD apple.txt
  * master   d3b585b commit Third git diff HEAD apple.txt
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  ```

* 切换分支

  ```shell
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git checkout host-fix  #切换到host -fix
  Switched to branch 'host-fix'
  D       good,txt
  
  user@TQ MINGW64 /d/笔记/weChat (host-fix)
  
  ```

* 合并分支

  ```shell
  
  $ git checkout host-fix
  Switched to branch 'host-fix'
  D       good,txt
  
  user@TQ MINGW64 /d/笔记/weChat (host-fix)
  $ git branch -v
  * host-fix d3b585b commit Third git diff HEAD apple.txt
    master   d3b585b commit Third git diff HEAD apple.txt
  
  user@TQ MINGW64 /d/笔记/weChat (host-fix)
  $ vim apple.txt
  
  user@TQ MINGW64 /d/笔记/weChat (host-fix)
  $ git add apple.txt
  warning: LF will be replaced by CRLF in apple.txt.
  The file will have its original line endings in your working directory.
  
  user@TQ MINGW64 /d/笔记/weChat (host-fix)
  $ git commit -m "commit host-fix finish"
  [host-fix c890d6d] commit host-fix finish
   1 file changed, 1 insertion(+)
  
  user@TQ MINGW64 /d/笔记/weChat (host-fix)
  $ git checkout master
  Switched to branch 'master'
  D       good,txt
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git marge host-fix
  git: 'marge' is not a git command. See 'git --help'.
  
  The most similar command is
          merge
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ git merge host-fix
  Updating d3b585b..c890d6d
  Fast-forward
   apple.txt | 1 +
   1 file changed, 1 insertion(+)
  
  user@TQ MINGW64 /d/笔记/weChat (master)
  $ cat apple.txt
  apple
  apple @@@@@@@@@@@@@@@@@@
  1234567890
  apple
  apple
  ```

* 有冲突时

  ![](D:\笔记\pictures\TIM截图20181016153623.png)

  冲突的解决

  ![](D:\笔记\pictures\TIM截图20181016153835.png)

### 3.6Git版本数据管理机制

* 集中![](D:\笔记\pictures\TIM截图20181016154125.png)

* Git（分布式）（保存完整）
* ![](D:\笔记\pictures\TIM截图20181016154347.png)

Git文件管理机制详解

 对文件进行add  --> commit 才会发现objects文件目录才发生变化，也就是说 git 在每次对本地版本库 ==进行commit的时候，就会对数据 进行一次保存，这是 会生成 commit对象，tree对象以及blob对象。==Git 存储数据内容的方式──为每份内容生成一个文件，取得该内容与头信息的 SHA-1 校验和，创建以该校验和前两个字符为名称的子目录，并以 (校验和) 剩下 38 个字符为文件命名 (保存至子目录下)。

通过 `cat-file` 命令可以将数据内容取回。

![](D:\笔记\pictures\TIM截图20181016155415.png)

​          Git的提交对象

![](D:\笔记\pictures\TIM截图20181016155424.png)

​              做些修改后再次提交，那么这次产生的提交对象会包含一个指向上次提交对象（父对象）的指针

![](D:\笔记\pictures\TIM截图20181016155025.png)

### 3.7在本地创建远程库以及别名

* 查看远程库 git remote -v

```shell
user@TQ MINGW64 /d/笔记/hashan (master)
$ git remote -v
orign   https://github.com/cherryBlossomss/huashan.git (fetch)
orign   https://github.com/cherryBlossomss/huashan.git (push)

```

* 起别名 git remote add orign https://github.com/cherryBlossomss/huashan.git

* 推送 git push orign master

  ```shell
  $  git push orign master
  fatal: ArgumentException encountered.
     ▒▒▒▒▒▒˾▒▒▒▒▒ͬ▒▒▒▒▒
  fatal: ArgumentException encountered.
     ▒▒▒▒▒▒˾▒▒▒▒▒ͬ▒▒▒▒▒
  Username for 'https://github.com': cherryBlossomss
  fatal: ArgumentException encountered.
     ▒▒▒▒▒▒˾▒▒▒▒▒ͬ▒▒▒▒▒
  fatal: ArgumentException encountered.
     ▒▒▒▒▒▒˾▒▒▒▒▒ͬ▒▒▒▒▒
  Counting objects: 7, done.
  Delta compression using up to 4 threads.
  Compressing objects: 100% (4/4), done.
  Writing objects: 100% (7/7), 635 bytes | 158.00 KiB/s, done.
  Total 7 (delta 0), reused 0 (delta 0)
  remote:
  remote: Create a pull request for 'master' on GitHub by visiting:
  remote:      https://github.com/cherryBlossomss/huashan/pull/new/master
  remote:
  To https://github.com/cherryBlossomss/huashan.git
   * [new branch]      master -> master
  
  ```

### 3.8 克隆操作

* 命令： git clone 【远程地址】
* 命令效果
  * 完整吧远程库下载到本地
  * 创建orign远程地址别名
  * 初始化本地库