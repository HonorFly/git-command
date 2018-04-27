# git分布式版本控制系统 #
## 1.安装 ##
    1. git官网下载安装程序
    2. 设置用户名和邮箱(这台机器上的git仓库使用此配置)
       git config --global user.name "你的name"
       git config --global user.email "你的email地址"
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
      2、不但修改了工作区某个文件的内容，还添加到暂存区，想丢弃修改，分两步，第一步用命令git reset HEAD file,此时回到场景1，第二步就是按照第一步的命令git checkout -- file；(git reset --hard HEAD 或者 git checkout HEAD -- file,这两种方法也可以实现add后的撤销）；
      3、已经git commit就是提交到版本库了，想撤销本次提交，参考上面的“版本回退”，回退到指定版本。

      工作区的修改分为两种情况：一种是修改后没被放到暂存区，此时用git checkout -- file 就可以回到和版本库一样的状态；另一种是已经添加到暂存区后，又做了修改，此时git checkout -- file这个命令就回到添加到暂存区后的状态，这时候就要采用第二种情况的方法进行撤销。

      git status 查看状态，可以根据下面的提示判断文件是否已在暂存区，当下面出现（use “git reset HEAD <file>..." to unstage）这句话说明修改添加到暂存区，还没有提交；当出现（use "git add <file>..." to update whaat will be committed) (use "git checkout -- <file>..." to discard changes in working directory)时，说明暂存区是干净的，工作区有修改。
## 8.删除文件 ##
      通常情况下，没用的文件直接在文本管理器将文件删除，也可以用rm命令删除文件（rm file）；
      删除文件后，工作区和版本库不一致，git status查看那个文件删除；

      此时，有两种选择情况：
        1.删错了，版本库还有，直接将误删的文件恢复到最新版本；git checkout -- file 这种情况本质就是版本库的替换工作区的，无论工作区是修改还是删除，都可以一键还原，但只能恢复到版本库的最新文件，不会恢复最近一次提交后修改的内容。
        2.确实从版本库中删除该文件。用命令git rm删掉，并且git commit提交。文件从版本库被删除。

      rm删除文件和从文件管理器删除文件是一样的,只是将工作区的文件删除,版本库的文件未删除,git rm file是删除版本库的文件。两者是不同的。如果是只删除工作区的文件可以用git checkout -- file，如果是git rm file删除文件，此时将版本库，暂存区和工作区的都删除，此时没有使用git commit命令提交到版本库时，可以使用版本回退或者git checkout HEAD file 或者 git checkout HEAD -- file；如果使用git rm file删除文件，并用git commit提交到版本库时，只能用版本回退恢复。
## 9.远程仓库 ##
     1.本地git仓库和GitHub仓库的设置
       首先，创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有看看目录下有没有id_rsa和id_rsa.pub这两个文件，如果有，直接跳过。如果没有，创建SSH Key：
       ssh-keygen -t rsa -C "email"
       然后一路回车。
       然后，登录github，打开settings，SSH Keys页面，点击add ssh keys，将id_rsa.pub文件的内容粘贴到key的文本框。点击add key。
       进入主目录：cd ~
     2.添加远程仓库
      两个仓库远程同步：
      首先，github创建一个新的仓库：create a new repository
      然后，将本地git仓库的内容推送到github仓库：
      git remote add origin git@github.com:github账户名/learngit.git
      最后，把本地仓库的内容推送到远程库上：
      git push -u origin master
      把master分支推送到远程，第一次推送master分支时，加上-u参数，git把本地的master分支推送到远程新的master分支，还会把本地的master分支和远程的master分支关联起来。
      以后提交命令：git push origin master
      关联远程库：git remote add origin git@server-name:path/repo-name.git
      第一次把分支推送到远程：git push -u origin master
      修改后推送远程：git push origin master
     3.从远程库克隆
      git clone 仓库地址(ssh或https都可以)
## 10.分支管理 ##
     1.创建分支和合并分支
      创建分支：git branch <name>
      切换分支：git checkout <name>
      创建+切换分支：git checkout -b <name>
      查看当前分支：git branch
      合并分支：git merge <name>  (合并指定分支到当前分支)
      合并后删除分支：git branch -d <name>

      HEAD指向当前分支，master指向提交分支
     2.解决冲突
      创建并切换分支后修改内容提交，然后切换分支修改同一个文件提交，然后将两个分支合并，这两个分支时修改了同一个文件，合并时发生冲突，需要先解决冲突，解决冲突后，重新提交，冲突解决，文件合并成功。一般情况下，合并是与主分支合并，最后提交也是提交主分支。最后删除分支。
      带参数的git log查看分支合并情况(分支合并图)：git log --graph  或 git log --graph --pretty=oneline --abbrev-commit
     3.分支管理
      团队开发过程中，master主分支上基本不写代码，只是合并发布用，团队都是在分支上进行的开发，合并也是合并在分支上，意思是主分支创建一个dev分支，然后在dev分支的基础上再创建每个开发人员的分支，平时开发人员的代码合并主要是合并到dev分支上，等到发布版本时，将代码合并到主分支master，最后提交。
      合并分支时：git merge  <name> 此方法合并时一种fast forward模式，快速模式，这种方法合并后看不出曾经做过合并，删除分支后丢掉分支信息。因此，开发时，合并采用禁用fast forward模式。
      合并dev产生新提交:git merge --no-ff -m "" dev   
     4.bug分支
      开发过程中出现修改bug的情况，从dev分支(当前工作分支)，切换到主分支master，在主分支master从新建立一个bug分支，在切换到主分支之前将工作区内容保存一下，不用git add，直接git stash保存当前工作区内容。然后切换到主分支master创建bug分支，解决问题后提交，合并到主分支，将bug分支删除，然后返回dev分支(切换到主分支之前的工作分支)，git stash list查看保存列表，然后恢复工作区内容，git stash apply 然后 git stash drop删除stash内容，或者直接采用git stash pop恢复的同时删除stash内容，再用git stash list查看，stash内容消失。可以多次git stash，恢复时查看列表git stash list，恢复指定的stash(git stash apply stash@[0])。

      修复bug时，通过创建新的bug分支进行修复，然后合并，最后删除；
      当手头工作没有完成时先把工作现场git stash一下，然后去修复bug，修复后再git stash pop 回到工作现场。
     5.分支未合并强制删除
      新功能开发建立一个新的分支：
      创建+切换分支：git checkout -b <name>
      开发完提交：git add -> git commit
      切换分支：git checkout dev
      未合并分支删除新的分支：git branch -D <name>

      未合并删除的分支就再也找不到。
     6.多人协作
      查看远程库：git remote
      查看远程库信息：git remote -v
      从本地推送分支：git push origin branch-name
      本地新建的分支如果不推送到远程，就对其他人不可见；从远程clone时，默认只能看到本地的master分支。如果在dev分支上开发，必须创建远程origin的dev分支到本地，于是创建本地dev分支：
      git checkout -b dev origin/dev
      两个人同时推送一个文件提交时，推送失败。此时先抓取分支：git pull
      然后在本地合并，解决冲突，再推送。
      git pull失败时，提示“no tracking information”，说明本地分支和远程分支的链接关系没创建，本地和远程关联：
      git branch --set-upstream-to=origin/<branch> branch-name
      抓取分支：git pull
      抓取分支失败,建立本地分支与远程分支的关联：
      git branch --set-upstream-to=origin/<branch> branch-name
      本地创建和远程分支对应的分支：git checkout -b branch-name origin/branch-name
      远程仓库创建分支：git push origin branch-name
      远程仓库删除分支：git push origin :branch-name
## 11.标签管理 ##
     1.创建标签
      创建新标签:git tag <name>
      创建标签在某一个版本：git tag <name> commit_id
      创建标签指定信息(带说明):git tag -a <name> -m "说明文字" commit_id 
                             -a指定标签名    -m 指定说明文字
      查看标签信息：git show <tagname>
      <!-- 用PGP签名标签: git tag -s <tagname> -m "说明文字" commit_id -->
      查看所有标签：git tag
     2.推送标签到远程
       推送一个标签到远程：git push origin <tagname>
       推送所有标签到远程：git push origin --tags
     3.删除标签
      未推送到远程之前(删除本地标签):git tag -d <tagname>
      已推送到远程后：
         首先，在本地删除：git tag -d <tagname>
         然后，远程删除：git push origin :refs/tags/<tagname>
## 12.同时关联码云和GitHub
     关联码云：git remote add origin git@gitee.com:username/learngit.git
     git remote add时报错：fatal: remote origin already exists.说明本地库已经关联了一个名叫origin的远程库，此时，可以先用git remote -v查看远程库信息:
        origin    git@github.com:username/learngit.git (fetch)
        origin    git@github.com:username/learngit.git (push)
     本地库已经关联了origin的远程库，并且，该远程库指向GitHub.
     删除已有的GitHub远程库：git remote rm origin
     再关联码云的远程库:git remote add origin git@gitee.com:username/learngit.git
     再查看远程库信息：git remote -v
        origin    git@gitee.com:username/learngit.git (fetch)
        origin    git@gitee.com:username/learngit.git (push)
     origin已经被关联到码云的远程库了。通过git push命令就可以把本地库推送到Gitee上。

     有多个远程库，我们需要用不同的名称来标识不同的远程库:
     先删除已关联的名为origin的远程库：git remote rm origin
     先关联GitHub的远程库：git remote add github git@github.com:username/learngit.git
     再关联码云的远程库：git remote add gitee git@gitee.com:username/learngit.git
     查看远程库信息:git remote -v
     推送到GitHub:git push github master
     推送到码云:git push gitee master
