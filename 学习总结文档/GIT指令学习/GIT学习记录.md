# 1. 基础命令  
- ## 版本回退
  首先，Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，也就是最新的提交，上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。
  
  **$ git reset --hard HEAD^**  
  **HEAD is now at e475afc add distributed**
  
  --hard参数有啥意义？--hard会回退到上个版本的已提交状态，而--soft会回退到上个版本的未提交状态，--mixed会回退到上个版本已添加但未提交的状态。

  回退到某一个版本后，如果想要在恢复到最新的修改，那么就必须有最新提交的commit id，在git中可以使用git reflog用来记录你的每一次命令  

  **$ git reflog**

- ## git add / git commit 指令
  电脑工作的目录被称为工作区，工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。git add把文件添加进去，实际上就是把文件修改添加到暂存区。
  
  git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以，现在，git commit就是往master分支上提交更改。所以，git add命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行git commit就可以一次性把暂存区的所有修改提交到分支。一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的。

  git checkout -- file可以丢弃工作区的修改  
  **$ git checkout -- readme.txt**  

  用命令git reset HEAD <file>可以把暂存区的修改撤销掉（unstage），重新放回工作区, 当我们用HEAD时，表示最新的版本  
  **$ git reset HEAD readme.txt**

- ## 分支管理
  - ## 创建与分支合并
    创建dev分支，然后切换到dev分支
    
    **git checkout -b dev**

    git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：

    **$ git branch dev**
    **$ git checkout dev**

    用git branch命令可以查看仓库中有哪些分支和当前在哪个分支之中。此时使用git commit等命令所提交的修改就会提交到当前分支之中。

    使用如下指令进行不同分支之间的切换。  
    **$git checkout master**

    此时可以把dev分支之中的内容合并到master分支上来， git merge命令用于合并指定分支到当前分支。  
    **$ git merge dev**

    Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。  
    **git merge --no-ff -m "merge with no-ff" dev**  

    在master分支上修复的bug，想要合并到当前dev分支，可以用git cherry-pick <commit>命令，把bug提交的修改“复制”到当前分支，避免重复劳动。
    
    **$ git branch  
          * dev  
            master  
        $ git cherry-pick 4c805e2**  

  - ## 解决冲突
      先用git pull把最新的提交从origin/dev抓下来，然后，在本地合并，解决冲突，再推送。
      **$ git pull**
      **$ git commit -m "fix env conflict"**
      **$ git push origin dev**
    
  - ## 多人协作
    当你从远程仓库克隆时，实际上Git自动把本地的master分支和远程的master分支对应起来了，并且，远程仓库的默认名称是origin。  
    推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上。  
    **$ git push origin master**  
    
    如果要推送其他分支，比如dev，就改成
    **$ git push origin dev**

    克隆远程代码仓库
    **$ git clone git@github.com:michaelliao/learngit.git**

    要在dev分支上开发，就必须创建远程origin的dev分支到本地，于是他用这个命令创建本地dev分支
    **$ git checkout -b dev origin/dev**

    把dev分支push到远程
    **$ git push origin dev** 

