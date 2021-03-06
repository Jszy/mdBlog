# GIT常用命令
## 修改文件迁移分支

将A分支中的修改暂存起来

```shell
git stash
```

<br/>

切换到B分支，然后将A分支上的修改弹出到B分支上

```shell
git stash pop
```

<br/>

## 远程仓库
1.git clone http://git.firstshare.cn/fe/\*.git 克隆远程仓库到本地  
2.git clone http://git.firstshare.cn/fe-h5/\*.git --recursive 克隆远程仓库到本地，同时递归克隆引用的子模块  
3.git init 将本地目录初始化为git版本控制，会自动创建.git目录  
4.git remote add origin http://git.firstshare.cn/fe/\*.git 将第3条初始化的目录，与远程仓库关联，此后即可推送代码到远程仓库  
5.git remote update 同步远程仓库到本地  
6.git push -u origin master 第一次推送，需要通过-u输入用户名和密码  

## 分支
1.git branch 查看本地分支  
2.git branch -r 查看远程分支  
3.git branch -a 查看所有分支（包括本地分支和远程分支）  
4.git branch <branch> 基于当前分支新建本地分支（不会自动切换为当前分支）  
5.git branch <branch> <base_branch> 基于某个分支新建本地分支（不会自动切换为当前分支）  
6.git checkout <branch> 切换分支  
7.git checkout -b <branch> 基于当前分支创建新分支并立刻切换到新分支  
8.git checkout -b <branch> <base_branch> 基于某个分支创建新分支并立刻切换到新分支  
9.git checkout -- <fileName>  恢复指定文件 
9.git branch -d <branch> 删除本地分支  
10.git push origin --delete <branch> 删除远程分支，或者用：git push origin :<branch>   
11.git push origin <branch> 创建远程分支或推送本地分支代码到远程分支  
12.git merge <branch> 合并其他分支代码到本分支  
13.git fetch -p 清除远程已经不存在的分支的本地跟踪  
14.git branch temp <commit_id> 以某次的commit创建临时分支，一般用于将游离的commit合并到主分支中  
15.git tag -a <tag> -m 'xxx' 新建tag  
16.git push origin <tag> 推送tag到远程  
17.git checkout -- <fileName> 恢复指定文件    
18.git branch --track <branch> origin/<newbranch> 修改本地分支的源 
        

## 提交代码
1.git add <file> 添加修改或新文件到索引  
2.git add . 添加所有修改和新文件到索引  
3.git commit -m 'xxx' 提交工作空间的修改，必须填写log  
4.git commit -am 'xxx' 2和3的合并操作  
5.git rm <file> 从工作空间和索引中删除文件  
6.git push origin <branch> 推送commit代码到远程分支  
7.git pull origin <branch> 从远程分支拉取最近commit  
8.git log -p -n 查看最近n次提交log（显示修改的代码）  
9.git log -l n 查看最近n次提交log（只显示基本信息，不显示修改的代码）  
10.git revert <commit> 还原一个提交版本  
11.git reset <commit> 将当前的工作目录完全回滚到指定的版本号  

## 子模块
1.git submodule add http://git.firstshare.cn/fe/\*.git 添加子模块仓库  
2.git submodule init 初始化子模块，只在首次检出仓库时运行一次即可  
3.git submodule update 更新子模块  
4.git submodule foreach git pull origin <branch> 递归拉取子模块的最近提交 

## git config
1.git config --global alias.co checkout  
2.git config --global alias.st status  
3.git config --global alias.ci commit  
4.git config --global alias.br branch  
5.git config --global alias.ss stash  
6.git config --global alias.sl 'stash list'  
7.git config --global alias.sp 'stash pop'  
8.git config --global alias.la 'pull --rebase'  
9.git config --global alias.ti 'push origin HEAD'  
10.git config commit.template ../git_commit.template    

## git reset：

reset命令有3种方式：  
git reset --mixed：此为默认方式，不带任何参数的git   reset，即时这种方式，它回退到某个版本，只保留源码，回退commit和index信息git  
git reset --soft HEAD^：回退到某个版本，只回退了commit的信息，不会恢复到index file一级。如果还要提交，直接commit即可  
git reset --hard：彻底回退到某个版本，本地的源码也会变为上一个版本的内容  

1.回退所有内容到上一个版本  
git reset HEAD^  
2.回退a.py这个文件的版本到上一个版本  
git reset HEAD^ a.py  
3.向前回退到第3个版本  
git reset –-soft HEAD~3  
4.将本地的状态回退到和远程的一样  
git reset –-hard origin/master  
5.回退到某个版本  
git reset 057d  
6.回退到上一次提交的状态，按照某一次的commit完全反向的进行一次commit  
git revert HEAD  

## git reset 某次提交 

```git
// 回退到指定版本
git reset --hard commit_id

// 强制提交
git push origin HEAD --force
```


## git commit 提交时候，配置信息与push时候不匹配  
需要修改的话，运行下面命令  
注意把`old name`和`new name`、`new email`修改成相应的真实数据 
```
git filter-branch --commit-filter '  
        if [ "$GIT_COMMITTER_NAME" = "<Old Name>" ];  
        then  
                GIT_COMMITTER_NAME="<New Name>";  
                GIT_AUTHOR_NAME="<New Name>";  
                GIT_COMMITTER_EMAIL="<New Email>";  
                GIT_AUTHOR_EMAIL="<New Email>";  
                git commit-tree "$@";  
        else  
                git commit-tree "$@";  
        fi' HEAD 
```
