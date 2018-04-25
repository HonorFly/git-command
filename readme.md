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
    git diff HEAD -- 文件名 可以查看工作区和仓库分支（版本库）里面最新版本的区别
    git add 是把要提交的所有修改放到暂存区 
    git commit 是把暂存区的修改提交到仓库分支
## 5.git commit后面没有写说明的情况 ##
    直接写git commit 进行提交，没有写提交说明和-m，git bash进入vim模式，处理方法：
    首先，输入i，进入insert输入模式，此时输入说明；（相当于给一次不就得说明机会）；
    然后，输入完后，按esc，下方的insert消失；
    最后，输入:wq,回车。
## 6.git log太长，无法退出的情况 ##
    按q即可（最好英文状态下，如果是中文按完q按回车键）
## 7.撤销修改 ##
    三种情况：
      1、修改的只是工作区某个文件的内容，想直接丢弃工作区的修改，用命令git checkout -- file；
      2、不但修改了工作区某个文件的内容，还添加到暂存区，想丢弃修改，分两步，第一步用命令git reset HEAD file,此时回到场景1，第二步就是按照第一步的命令git checkout -- file；
      3、已经git commit就是提交到版本库了，想撤销本次提交，参考上面的“版本回退”，回退到指定版本。

      工作区的修改分为两种情况：一种是修改后没被放到暂存区，此时用git checkout -- file 就可以回到和版本库一样的状态；另一种是已经添加到暂存区后，又做了修改，此时git checkout -- file这个命令就回到添加到暂存区后的状态，这时候就要采用第二种情况的方法进行撤销。

      git status 查看状态，可以根据下面的提示判断文件是否已在暂存区，当下面出现（use “git reset HEAD <file>..." to unstage）这句话说明修改添加到暂存区，还没有提交；当出现（use "git add <file>..." to update whaat will be committed) (use "git checkout -- <file>..." to discard changes in working directory)时，说明暂存区是干净的，工作区有修改。