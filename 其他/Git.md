# Git 学习
### 创建版本库
- 初始化一个 Git 仓库，使用 `git init` 命令
- 添加文件到Git仓库，分两步：
  1. 使用命令 `git add <file>` ，注意，可反复多次使用，添加多个文件；
  2. 使用命令 `git commit -m "提交说明"` ，完成。

### 时光机
- 查看状态
  - 要随时掌握工作区的状态，使用 `git status` 命令。
  - 如果 `git status` 告诉你有文件被修改过，用 `git diff` 可以查看修改内容。
- 版本回退
  - `git log` 查看文件更改日志
  - `HEAD` 表示当前版本， `HEAD^` 表示上一个版本，以后依此类推。
  - `git reset --hard commit_id/HEAD^` 命令可以实现回到过去未来某个版本。
  - `git reflog` 查看每一次命令的记录，可以用来查看 commit_id。
- 工作区和暂存区<br />
  [全是概念性的东西，看网页版](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013745374151782eb658c5a5ca454eaa451661275886c6000)
- 撤销修改
  - `git checkout -- file`  可以把文件在工作区的修改全部撤销，有两种情况
    - 一种是文件自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
    - 一种是文件已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
    - 总之，就是让这个文件回到最近一次git commit或git add时的状态。
  - `git reset HEAD file` 命令可以把暂存区的修改撤销掉（unstage）
- 删除文件
  - `git rm file` 用于删除版本库里的文件
  - 如果文件从工作区被误删，可以用 `git checkout -- file` 恢复

### 远程仓库
- 添加远程库
  - 创建 SSH Key ：`ssh-keygen -t rsa -C "youremail@example.com"`
  - 关联远程库 `git remote add origin https://github.com/miotyan/learngit.git`
  - 关联后用命令`git push -u origin master`第一次推送 master 分支的所有内容
  - 用`git push origin master`把本地 master 分支的最新修改推送至GitHub
- 从远程库克隆
  - `git clone url` 克隆一个本地库，url可以在 GitHub 网站看见

### 分支管理
- 创建 合并与删除分支
  - 查看分支：`git branch`
  - 创建分支：`git branch <name>`
  - 切换分支：`git checkout <name>`
  - 创建+切换分支：`git checkout -b <name>`
  - 合并某分支到当前分支：`git merge <name>`
  - 删除分支：`git branch -d <name>`
  - `git checkout -b <name>` 新建建并切换至分支，等于`git branch <name>`+`git checkout <name>`
- 解决冲突
  - `git log --graph` 命令可以看到分支合并图

### 标签管理
### 使用 Github
### 自定义 Git
