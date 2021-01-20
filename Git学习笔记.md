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

git命令

git add .添加所有文件到暂存区

git diff 查看修改文件的内容

git commit -m "xxx"     提交暂存区内容到仓库(xxx代表版本说明)

git status  查看当前git状态

git log 查看版本信息

git log --pretty==oneline 查看简写的版本信息

git reset --hard HEAD^  回退到上个版本

git reset --hard HEAD~100  回退到上100个版本

git reset --hard 1094a00  会退到版本MD5前七位为1094a00的版本

git reflog 查看以往每次操作的MD5码

git diff 注意：只能在git add .之前显示修改内容
