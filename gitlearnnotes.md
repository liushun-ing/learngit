#                git语句学习总结

1. 安装git及有些基础要点

   * ```
     $ git config --global user.name "your name"
     $ git config --global user.email "email"
     config 和 --global这两个参数表示这台机器上的所有的git仓库都会使用这个配置
     ```

   * `HEAD` 表示当前版本   `HEAD^ `  表示上一个版本   `HEAD^`   表示上上版本  第几个版本写成`HEAD~n` 

   * `Fast-forward`  快进模式，合并分支时，速度非常快，此模式下，删除分支，会丢掉分支信息

     `--no-ff`  表示禁用 `Fast-forward`

2. 创建版本库

| 命令语句         | 解释                        |
| ---------------- | --------------------------- |
| $ mkdir learngit | 创建一个空目录              |
| $ cd learngit    | 进入目录路径                |
| $ pwd            | 查看当前目录                |
| $ git init       | 把目录变成Git可以管理的仓库 |
| $ git ls -ah     | 查看隐藏目录                |
| $ git ls         | 查看文件目录                |

3. 文件操作

| 命令语句                     | 解释                                      |
| ---------------------------- | ----------------------------------------- |
| $ cat 文件名                 | 查看文件                                  |
| $ git add 文件名             | 把文件添加到仓库                          |
| $ git add -f 文件名          | 强制添加文件                              |
| $ git commit -m "操作说明"   | 把文件提交到仓库，可一次提交多个 -m加描述 |
| $ git status                 | 当前仓库的状态                            |
| $ git diff 文件名            | 查看文件的修改内容                        |
| $ git log                    | 查看提交历史纪录，详细记录                |
| $ git log --pretty=oneline   | 简单输出提交历史记录信息commit id和说明   |
| $ git reset --hard HEAD^     | 回退到上一个版本                          |
| $ git reset --hard commit id | 回退到某个版本                            |
| $ git reflog                 | 查看每一次命令历史                        |
| $ git diff HEAD -- 文件名    | 查看工作区和版本库最新版本的区别          |
| $ git checkout -- 文件名     | 撤销工作区的修改                          |
| $ git reset HEAD 文件名      | 撤销暂存区的修改，退回到工作区            |
| $ rm 文件名                  | 删除工作区的文件                          |
| $ git rm 文件名              | 确定从版本库中删除，要commit一次          |

4. 远程库

| 命令语句                                                     | 解释                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| $ ssh-keygen -t rsa -C "email"                               | 创建SSH Key                                                  |
| git remote add 远程库名字 git@server-name:path/repo-name.git | 关联本地仓库与远程库                                         |
| $ git push -u 远程库名字 分支                                | 推送内容到远程库，-u将分支关联                               |
| $ git push 远程库名字 分支                                   | 分支关联后，推送内容到远程库                                 |
| $ git clone git@server-name:path/repo-name.git               | 克隆远程库到本地库，ssh协议速度最快                          |
| $ git remote                                                 | 查看远程库信息                                               |
| $ git remote -v                                              | 显示远程库详细信息                                           |
| $ git pull                                                   | 把分支最新的提取从远程库抓下来                               |
| $ git checkout -b branch-name origin/branch-name             | 在本地创建和远程分支对应的分支                               |
| $ git branch --set-upstream-to <branch-name> origin/<branch-name> | 建立本地分支和远程分支的关联                                 |
| $ git rebase                                                 | 把本地未push的分叉提交历史整理成直线。但本地的分叉提交已经被修改过了 |
| $ git remote rm 远程库名                                     | 删除远程库                                                   |

5. 分支管理

| 命令语句                                           | 解释                            |
| -------------------------------------------------- | ------------------------------- |
| $ git checkout -b 分支名                           | 创建分支，-b参数表示创建并切换  |
| $ git switch -c 分支名                             | 创建分支，-c 参数表示创建并切换 |
| $ git branch 分支名                                | 创建分支                        |
| $ git checkout 分支名                              | 切换分支                        |
| $ git switch 分支名                                | 切换分支                        |
| $ git branch                                       | 查看分支，当前分支前有 *        |
| $ git merge 分支名                                 | 合并指定分支到当前分支          |
| $ git branch -d 分支名                             | 删除分支                        |
| $ git log --graph --pretty=oneline --abbrev-commit | 查看分支合并情况                |
| $ git merge --no-ff -m "说明文字" 分支名           | 合并分支                        |
| $ git stash                                        | 隐藏当前工作                    |
| $ git stash list                                   | 查看隐藏的工作现场位置          |
| $ git stash apply                                  | 恢复隐藏文件，但不删除stash内容 |
| $ git stash drop                                   | 删除stash内容                   |
| $ git stash pop                                    | 恢复隐藏内容并删除stash内容     |
| $ git stash apply stash名称                        | 删除指定的stash                 |
| $ git cherry-pick commit_id                        | 赋值特定的提交到当前分支        |
| $ git branch -D 分支名                             | 强行删除分支，未合并修改将丢失  |
| $ git remote                                       | 查看远程库信息                  |
| $ git remote -v                                    | 显示远程库详细信息              |

6. 标签

| 命令                                        | 解释                                   |
| ------------------------------------------- | -------------------------------------- |
| $ git tag <name>                            | 创建标签                               |
| $ git tag                                   | 查看所有标签                           |
| $ git tag 标签名 commit_id                  | 对某个特定提交加标签                   |
| $ git show <tagname>                        | 对某个特定标签查看其信息               |
| $ git tag -a 标签名 -m "说明文字" commid_id | 创建带有说明文字的标签                 |
| $ git tag -d 标签名                         | 删除标签                               |
| $ git push 远程库名 <tagname>               | 推送某个标签到远程库                   |
| $ git push 远程库名 --tags                  | 一次性推送全部尚未推送到远程的本地标签 |
| $ git push 远程库名 :refs/tags/标签名       | 删除远程库标签，注意要先删除本地的     |
|                                             |                                        |

7. 其他

* `$ git config --global color.ui true`    让Git显示颜色，让命令输出更醒目

* ```
  $ git config --global alias.co checkout
  $ git config --global alias.ci commit
  $ git config --global alias.br branch
  配置别名
  ```



