# git分布式版本控制系统
## 1.安装 ##
1. git官网下载安装程序
2. 配置  
         `git config --global user.name`
         `git config --global user.email`
## 2.初始化 ##
    git init  初始化
    git diff  比较文件的改变
    git status  仓库的状态
## 3.版本回退 ##
    git log 查看提交历史
    git log --pretty=oneline 查看提交历史精简
    git reflog  查看命令历史（便于回退版本）
    git reset --hard HEAD^ 回退上一版本 HEAD^^ 回退两个版本  HEAD~100 回退100个版本
    git reset --hard commit_id(例：384180) 数字指定回退到的版本号，数字是commit_id