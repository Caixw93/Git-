学习部分内容来自廖雪峰官方网站

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

![Git原理图](C:\Users\Administrator\Desktop\杂项\Git原理图.jpg)

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

