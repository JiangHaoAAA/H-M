# 1. 基础命令  
- ## 版本回退
  首先，Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，也就是最新的提交，上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。
  
  **$ git reset --hard HEAD^**  
  **HEAD is now at e475afc add distributed**
  
  --hard参数有啥意义？--hard会回退到上个版本的已提交状态，而--soft会回退到上个版本的未提交状态，--mixed会回退到上个版本已添加但未提交的状态。

  回退到某一个版本后，如果想要在恢复到最新的修改，那么就必须有最新提交的commit id，在git中可以使用git reflog用来记录你的每一次命令  

  ** $ git reflog **

  
