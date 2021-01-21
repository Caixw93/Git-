学习内容来自廖雪峰官方网站

# GitHub

1.Repository(仓库)

仓库用来存放项目代码，每个项目对应一个仓库

2.Star(收藏)

收藏项目，方便下次查看

3.Fork(复制克隆项目)

理解：项目分支

4.Pull Request(发起请求)

基于Fork的，别人在你的基础上做了改进，合并到Fork的根项目中

5.Watch(关注)

项目更新会有通知

6.Issue(事务卡片)

发现代码BUG，但是目前没有成型代码，需要讨论时使用

# Git原理图



![Git原理图](.\Git原理图.jpg)

# Git命令

git init 添加仓库

git add .添加所有文件到暂存区

git diff 查看修改文件的内容

git commit -m "xxx"     提交暂存区内容到仓库(xxx代表版本说明)

git status  查看当前git状态

git log 查看版本信息

git log --pretty==oneline 查看简写的版本信息

git reset --hard HEAD^  回退到上个版本

git reset --hard HEAD^^ 回退到上上个版本

git reset --hard HEAD~100  回退到上100个版本

git reset --hard 1094a00  会退到版本MD5前七位为1094a00的版本

git reflog 查看以往每次操作的MD5码

git diff  注意：只能在git add .之前显示修改内容

git diff HEAD -- 文件名.后缀名    查看工作区和版本库里面的区别



git checkout -- 文件名.后缀名     丢弃工作区的修改，这里分两种情况：

**1.工作区文件没有git add 到暂存区，丢弃修改相当于还原到最近的一个版本**

**2.工作区文件已经git add到暂存区，丢弃的是git add到暂存区之后的内容**



git reset HEAD 文件名.后缀名  将暂存区的文件回退到工作区

rm 文件名.后缀名 删除工作区文件

git rm 文件名.后缀名  删除工作区文件

git ckeckout --文件名.后缀名 从版本库替换工作区版本



# Git添加远程仓库

1.查看本地C盘用户目录有没有.ssh文件夹，没有的话，创建SSH Key:

```
ssh-keygen -t rsa -C "Git用户邮箱"
```

然后一直回车，会出现.ssh文件夹里面有两个文件：

id_rsa`和`id_rsa.pub

`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

2.注册GitHub,找到SSHKeys页面

点击“Add SSH Key”，填写Title,将.ssh文件夹中的`id_rsa.pub内容添加进Keywenben，最后“Add Key”

3.GitHub创建仓库,在Repository name填写仓库名（例“learngit”），创建一个叫learngit的仓库

4.关联一个远程仓库，本地仓库git运行：

git remote add origin git@github.com:GitHub用户名/仓库名.git

5.将本地仓库内容推送到GitHub远程仓库

```
git push -u origin master
```



把本地库的内容推送到远程，用`git push`命令，实际上是把当前分支`master`推送到远程。

由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。

6.推送成功后，可以立刻在GitHub页面中看到远程库的内容已经和本地一模一样

从现在起，只要本地作了提交，就可以通过命令：

```
$ git push origin master
```

把本地`master`分支的最新修改推送至GitHub，现在，你就拥有了真正的分布式版本库！



警告：

### SSH警告

当你第一次使用Git的`clone`或者`push`命令连接GitHub时，会得到一个警告：

```
The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
RSA key fingerprint is xx.xx.xx.xx.xx.
Are you sure you want to continue connecting (yes/no)?
```

这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入`yes`回车即可。

Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：

```
Warning: Permanently added 'github.com' (RSA) to the list of known hosts.
```

这个警告只会出现一次，后面的操作就不会有任何警告了。

如果你实在担心有人冒充GitHub服务器，输入`yes`前可以对照[GitHub的RSA Key的指纹信息](https://help.github.com/articles/what-are-github-s-ssh-key-fingerprints/)是否与SSH连接给出的一致。



# Git克隆仓库

1.克隆仓库命令：git clone git@github.com:用户名/仓库名.git

克隆出来的仓库有两个分支，一个是main,另外一个是master

## 注意事项：

因为本地仓库的分支是master,，所以需要切换分支



# Git分支管理

1.创建一个名为"dev"分支

```
git checkout -b dev
```

注意：-b参数表示创建并且切换，相当于

```
$ git branch dev
$ git checkout dev
```

2.git checkout切换分支

3.git  branch查看当前的分支

4.git merge dev 在master分支中输入此命令，表示将dev分支合并到master分支中

5.git branch -d dev 删除dev分支

6.git switch -c dev 创建并切换到dev分支

7.git switch master 直接切换到master分支



## 合并分支

出现冲突，可用

```
 git status
```

查看冲突内容

例如：

```
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.
<<<<<<< HEAD
Creating a new branch is quick & simple.
=======
Creating a new branch is quick AND simple.
>>>>>>> feature1
```

Git用`<<<<<<<`，`=======`，`>>>>>>>`标记出不同分支的内容

用带参数的`git log`也可以看到分支的合并情况

```
git log --graph --pretty=oneline --abbrev-commit
```

用`git log --graph`命令可以看到分支合并图



禁用快速合并Fast forward(dev:分支名)：

```
git merge --no-ff -m "merge with no-ff" dev
```

## 分支策略

在实际开发中，我们应该按照几个基本原则进行分支管理：

首先，`master`分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

那在哪干活呢？干活都在`dev`分支上，也就是说，`dev`分支是不稳定的，到某个时候，比如1.0版本发布时，再把`dev`分支合并到`master`上，在`master`分支发布1.0版本；

你和你的小伙伴们每个人都在`dev`分支上干活，每个人都有自己的分支，时不时地往`dev`分支上合并就可以了。

所以，团队合作的分支看起来就像这样：

![git-br-policy](https://www.liaoxuefeng.com/files/attachments/919023260793600/0)

### 小结

Git分支十分强大，在团队开发中应该充分应用。

合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并。

## Bug分支

```
git stash
```

Git还提供了一个`stash`功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作

```
git stash list
```

查看工作现场存放位置

一是用`git stash apply`恢复，但是恢复后，stash内容并不删除，你需要用`git stash drop`来删除；

另一种方式是用`git stash pop`，恢复的同时把stash内容也删了

恢复工作现场

```
git stash apply stash@{0}
```

你可以多次stash，恢复的时候，先用`git stash list`查看，然后恢复指定的stash

在master分支上修复了bug后，我们要想一想，dev分支是早期从master分支分出来的，所以，这个bug其实在当前dev分支上也存在。

那怎么在dev分支上修复同样的bug？重复操作一次，提交不就行了？

有木有更简单的方法？

有！

同样的bug，要在dev上修复，我们只需要把`4c805e2 fix bug 101`这个提交所做的修改“复制”到dev分支。注意：我们只想复制`4c805e2 fix bug 101`这个提交所做的修改，并不是把整个master分支merge过来。

为了方便操作，Git专门提供了一个`cherry-pick`命令，让我们能复制一个特定的提交到当前分支：

```
$ git branch
* dev
  master
$ git cherry-pick 4c805e2
[master 1d4b803] fix bug 101
 1 file changed, 1 insertion(+), 1 deletion(-)
```

Git自动给dev分支做了一次提交，注意这次提交的commit是`1d4b803`，它并不同于master的`4c805e2`，因为这两个commit只是改动相同，但确实是两个不同的commit。用`git cherry-pick`，我们就不需要在dev分支上手动再把修bug的过程重复一遍。

有些聪明的童鞋会想了，既然可以在master分支上修复bug后，在dev分支上可以“重放”这个修复过程，那么直接在dev分支上修复bug，然后在master分支上“重放”行不行？当然可以，不过你仍然需要`git stash`命令保存现场，才能从dev分支切换到master分支。

#### 小结

修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复bug，修复后，再`git stash pop`，回到工作现场；

在master分支上修复的bug，想要合并到当前dev分支，可以用`git cherry-pick <commit>`命令，把bug提交的修改“复制”到当前分支，避免重复劳动。



# 删除没合并的分支

开发一个新feature，最好新建一个分支；

如果要丢弃一个没有被合并过的分支，可以通过

`git branch -D <name>`

强行删除。



# 多人协作



当你从远程仓库克隆时，实际上Git自动把本地的`master`分支和远程的`master`分支对应起来了，并且，远程仓库的默认名称是`origin`。

要查看远程库的信息

`git remote`：

```
$ git remote
origin
```

显示更详细的信息：

`git remote -v`

```
$ git remote -v
origin  git@github.com:michaelliao/learngit.git (fetch)
origin  git@github.com:michaelliao/learngit.git (push)
```

上面显示了可以抓取和推送的`origin`的地址。如果没有推送权限，就看不到push的地址。

### 推送分支

推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上： 

```
$ git push origin master
```

如果要推送其他分支，比如`dev`，就改成：

```
$ git push origin dev
```

但是，并不是一定要把本地分支往远程推送，那么，哪些分支需要推送，哪些不需要呢？

1.`master`分支是主分支，因此要时刻与远程同步；

2.`dev`分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；

3.bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；

4.feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

### 抓取分支

多人协作时，大家都会往`master`和`dev`分支上推送各自的修改。

现在，模拟一个你的小伙伴，可以在另一台电脑（注意要把SSH Key添加到GitHub）或者同一台电脑的另一个目录下克隆：

```
$ git clone git@github.com:michaelliao/learngit.git
Cloning into 'learngit'...
remote: Counting objects: 40, done.
remote: Compressing objects: 100% (21/21), done.
remote: Total 40 (delta 14), reused 40 (delta 14), pack-reused 0
Receiving objects: 100% (40/40), done.
Resolving deltas: 100% (14/14), done.
```

当你的小伙伴从远程库clone时，默认情况下，你的小伙伴只能看到本地的`master`分支。不信可以用`git branch`命令看看：

```
$ git branch
* master
```

现在，你的小伙伴要在`dev`分支上开发，就必须创建远程`origin`的`dev`分支到本地，于是他用这个命令创建本地`dev`分支：

```
$ git checkout -b dev origin/dev
```

现在，他就可以在`dev`上继续修改，然后，时不时地把`dev`分支`push`到远程：

```
$ git add env.txt

$ git commit -m "add env"
[dev 7a5e5dd] add env
 1 file changed, 1 insertion(+)
 create mode 100644 env.txt

$ git push origin dev
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 308 bytes | 308.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To github.com:michaelliao/learngit.git
   f52c633..7a5e5dd  dev -> dev
```

你的小伙伴已经向`origin/dev`分支推送了他的提交，而碰巧你也对同样的文件作了修改，并试图推送：

```
$ cat env.txt
env

$ git add env.txt

$ git commit -m "add new env"
[dev 7bd91f1] add new env
 1 file changed, 1 insertion(+)
 create mode 100644 env.txt

$ git push origin dev
To github.com:michaelliao/learngit.git
 ! [rejected]        dev -> dev (non-fast-forward)
error: failed to push some refs to 'git@github.com:michaelliao/learngit.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

推送失败，因为你的小伙伴的最新提交和你试图推送的提交有冲突，解决办法也很简单，Git已经提示我们，先用`git pull`把最新的提交从`origin/dev`抓下来，然后，在本地合并，解决冲突，再推送：

```
$ git pull
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.

    git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> dev
```

`git pull`也失败了，原因是没有指定本地`dev`分支与远程`origin/dev`分支的链接，根据提示，设置`dev`和`origin/dev`的链接：

```
$ git branch --set-upstream-to=origin/dev dev
Branch 'dev' set up to track remote branch 'dev' from 'origin'.
```

再pull：

```
$ git pull
Auto-merging env.txt
CONFLICT (add/add): Merge conflict in env.txt
Automatic merge failed; fix conflicts and then commit the result.
```

这回`git pull`成功，但是合并有冲突，需要手动解决，解决的方法和分支管理中的[解决冲突](http://www.liaoxuefeng.com/wiki/896043488029600/900004111093344)完全一样。解决后，提交，再push：

```
$ git commit -m "fix env conflict"
[dev 57c53ab] fix env conflict

$ git push origin dev
Counting objects: 6, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 621 bytes | 621.00 KiB/s, done.
Total 6 (delta 0), reused 0 (delta 0)
To github.com:michaelliao/learngit.git
   7a5e5dd..57c53ab  dev -> dev
```

因此，多人协作的工作模式通常是这样：

1. 首先，可以试图用`git push origin <branch-name>`推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`推送就能成功！

如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。

### 小结

1.查看远程库信息，使用`git remote -v`；

2.本地新建的分支如果不推送到远程，对其他人就是不可见的；

3.从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；

4.在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；

5.建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；

6.从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。



# Rebase

```
git log --graph --pretty=oneline --abbrev-commit
```

查看分支情况

git rebase

原本分叉的提交现在变成一条直线了

### 小结

- rebase操作可以把本地未push的分叉提交历史整理成直线；
- rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。



# Git标签

## 创建标签

在Git中打标签非常简单，首先，切换到需要打标签的分支上：

```
$ git branch
* dev
  master
$ git checkout master
Switched to branch 'master'
```

打标签：git tag 标签名

```
$ git tag v1.0
```

可以用命令`git tag`查看所有标签：

```
$ git tag
v1.0
```

在历史提交的版本中找到一个版本打标签

1.查看历史版本

```
 git log --pretty=oneline --abbrev-commit
```

2.在提交的一次版本中打标签：

（

例如：

 版本提交名字为：add merge

它对应的commit id是`f52c633`

）

```
git tag v0.9 f52c633
```

再用命令`git tag`查看标签：

```
$ git tag
v0.9
v1.0
```



3.查看标签信息

git show <tagname>

```
$ git show v0.9
```

4.指定标签名和标签说明：

创建带有说明的标签，用`-a`指定标签名，`-m`指定说明文字

```
$ git tag -a v0.1 -m "version 0.1 released" 1094adb
```

用命令`git show <tagname>`可以看到说明文字：

```
$ git show v0.1
tag v0.1
Tagger: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 22:48:43 2018 +0800

version 0.1 released

commit 1094adb7b9b3807259d8cb349e7df1d4d6477073 (tag: v0.1)
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 21:06:15 2018 +0800

    append GPL

diff --git a/readme.txt b/readme.txt
...
```

### 小结

- 命令`git tag <tagname>`用于新建一个标签，默认为`HEAD`，也可以指定一个commit id；
- 命令`git tag -a <tagname> -m "blablabla..."`可以指定标签信息；
- 命令`git tag`可以查看所有标签。

## 操作标签

1.删除标签

git tag -d 标签名

```
$ git tag -d v0.1
```

2.推送某个标签到远程仓库

git push origin <tagname>

```
$ git push origin v1.0
```

3.一次性推送全部的标签到远程仓库

```
$ git push origin --tags
```

4.删除已推送的标签

·先删除本地：$ git tag -d v0.9，

·然后删除远程仓库：$ git push origin :refs/tags/v0.9



# Gitee的使用

![Gitee钥匙的添加](.\Gitee钥匙的添加.jpg)

1.将本地仓库与远程仓库关联

git remote add origin git@gitee.com:gitee的用户名/仓库名.git

git remote add origin  git@gitee.com:liaoxuefeng/learngit.git

2.如果本地仓库已经关联其他的远程仓库：

（1）查看关联的仓库信息

```
git remote -v
```

（2）删除已有的远程仓库

```
git remote rm origin
```

（3）关联新的Gitee仓库

```
git remote add origin git@gitee.com:liaoxuefeng/learngit.git
```

# 本地仓库关联多个远程仓库

远程仓库都叫origin，如果要想关联多个远程仓库：

1.git remote rm origin，删除本地仓库关联的远程仓库‘

2.原先关联远程仓库时使用的是

git remote add origin git@github.com:用户名/仓库名.git,

现在先关联github，使用命令：

git remote add github git@github.com:用户名/仓库名.git

再关联gitee

git remote add gitee git@gitee.com:用户名/仓库名.git

3.查看是否关联

git remote -v

4.如果要推送到GitHub，使用命令：

```
git push github master
```

如果要推送到Gitee，使用命令：

```
git push gitee master
```