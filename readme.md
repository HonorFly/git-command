# git分布式版本控制系统 #
## 1.安装 ##
    1. git官网下载安装程序
    2. 配置  
       git config --global user.name 
       git config --global user.email
## 2.初始化 ##
    git init  初始化
    git add 添加文件
    git commit -m "提交说明" 文件提交
    git diff  比较文件的改变
    git status  仓库的状态
## 3.版本回退 ##
    git log 查看提交历史
    git log --pretty=oneline 查看提交历史精简
    git reflog  查看命令历史（便于回退版本）
    git reset --hard HEAD^ 回退上一版本 HEAD^^ 回退两个版本  HEAD~100 回退100个版本
    git reset --hard commit_id(例：384180) 数字指定回退到的版本号，数字是commit_id
## 4.工作区和暂存区 ##
    git diff 是工作区（work dict）和暂存区（stage）的比较
    git diff --cashed 是暂存区（stage)和仓库分支(master)的比较
    git add 是把要提交的所有修改放到暂存区 
    git commit 是把暂存区的修改提交到仓库分支
    git diff HEAD -- 文件名 可以查看工作区和仓库分支（版本库）里面最新版本的区别
## 5.git commit后面没有写说明的情况 ##
    直接写git commit 进行提交，没有写提交说明和-m，git bash进入vim模式，处理方法：
    首先，输入i，进入insert输入模式，此时输入说明；（相当于给一次不就得说明机会）；
    然后，输入完后，按esc，下方的insert消失；
    最后，输入:wq,回车。
## 6.git log太长，无法退出的情况 ##
    按q即可（最好英文状态下，如果是中文按完q按回车键）
    