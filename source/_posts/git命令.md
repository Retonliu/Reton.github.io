---
title: git命令
date: 2020-08-25 16:24:43
tags: git
---
*git的配置
pwd当前工作路径
ls-al 显示当前文件夹下的所有文件
clean 清屏
cp 加文件路径可以把该文件复制到当前的工作路径中 e.g cp ../a/b.css  c/b.css 
配置user信息
$git config --global user.name 'your name'
$git config --global user.email 'your_email@domain.com
$git connfig --local user.name 查看配置中的用户信息
$git config --local 只对某个仓库有效，需要在某个仓库的路径下使用
$git config --global 对当前用户的所有仓库有效
$git config --system 对系统所有登陆的用户有效
以上三条命令后面加上--list，就可以显示对应的config配置

*创建git仓库
①进入代码文件夹然后使用 $git init
②进入某个文件夹 然后 $git init your_project 然后再进入你的项目文件夹

*进行变更
$git mv oldfilename newfilename + git commit -m'' 修改文件名字
$git status 显示暂存区和工作区
$vi filename 可以查看文件内容
$git add filename 把文件内容添加到暂存区
$git commit -m'information' 把暂存区的内容放入到git管理之中
$git add -u 可以一次性把当前状态中的文件一次性放到暂存区当中

*查看版本历史
$git log (只看当前分支的历史)
$git log --all all和nx一起用的话，x是指所有分支合起来的最近的x次
$git log -nx x是表示查看最近的多少次的提交
$git log --oneline 简洁版的查看历史
$git branch -av 可查看本地有多少个分支
$git checkout -b temp(分支名字） id(基于哪个commit创建的分支)
$gig log --all -graph 命令行中图形化
$gitk 图形化

$git cat-file -p +哈希值 查看文件内容
$git checkout branchname 切换分支
$git cat-file -t +哈希值 查看对象的类型
$git diff id1 id2 查看两个commit的不同
$git branch -d branchname 删除分支
$git branch -D branchname 删除分支
$git commit --amend 修改最新commit的message
$git rebase -i 加上要修改的commit的父commit 的id reword其中的子commit

$git rebase -i 加上要合并的连续的几个commit的父commit的id，使用squash几个子commit
$git rebase -i 加上要合并的间隔的几个commit的父commit的id,在交互界面要把要合并的commit放在相邻 然后使用$git rebase --continue
以上两种方法合并后都会生成一个新的commit

$git diff --cached 比较暂存区和当前head的差别
$git diff 比较工作区和暂存区的差别，后面可以加具体的filename 或者两个分支的名字/commit id号码（也可以再加上两个分支中相同的文件的文件名字）
$git reset HEAD 暂存区全部文件恢复成HEAD模样
$git reset HEAD -- filename让暂存区选中的文件恢复成HEAD状态
$git checkout -- filename 让工作区文件状态变为暂存区相同文件的状态
$git reset --hard id(要回到哪个commit的那个id号码） 消除最近的几次提交，从选定的id到当前的commit都会被消除
$git reset --hard 把暂存区清空，不会影响git的历史
$git rm filename 删除文件，git会直接把这个情况放在暂存区
$git stash 可以把目前工作区所作的修改存起来
$git stash list 查看stash里面存得东西
$git stash apply 把stash 的状态重新放到工作区中
$git stash pop 把stash状态放到工作区当中并且把该状态从stash list当中删除
$git add remotename +githubaddress 建立和github的链接
$git push remotename -all/branchname 把当前仓库的所有信息都push到远端
$git fetch remotename branchname 可以把远端的某个分支拉到本地
$git merge remotename/branchname 将两个有父子关系的merge