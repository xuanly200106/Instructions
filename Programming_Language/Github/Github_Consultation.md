# GitHub Consult Notes
## 初始化
在对应目录下  `git init`

## 基本操作
#### 查看信息
- `git status`  查看状态
- `git diff` <file> 查看文档修改细节（未提交的变动）
- `git log` 查看最远到最近日志  
    常用`git log --graph --pretty=oneline --abbrev-commit`
- `git reflog` 查看历史的日志

#### 添加文件或者添加修改到仓库
    git add <file>

#### 提交仓库
    git commit -m "<Instructions>"

#### 版本退回
- `git reset --hard HEAD^`  
 HEAD为当前版本，HEAD^^（^个数表示退回数目），HEAD~N(N表示退回数目)
- `git reset --hard <版本号>`  
 退回固定版本

#### 撤销工作区修改
`git checkout -- <file>` 暂存区没有时返回版本库，否则返回暂存区

#### 撤销暂存区修改
`git reset HEAD <file>` 即重设为HEAD版本

#### 删除文件：
    git rm <file> -r
    git commit -m "<Instructions>"

## 远程库操作

- 添加远程库 
`git remote add <远程库名称，默认为origin> git@github.com:xuanly200106/<repository name>.git`
- 修改远程库 `git remote set-url <origin> <new address>`
- 查看远程库  `git remote`
- 查看远程库详细信息 `git remote -v`
- 删除远程库
    `git remote remove <Name>`
- 推至远程库：
`git push origin master`  
    (我们第一次推送master分支时，加上了-u参数（位于origin前面），Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。)
- 从远程库克隆：
    +  `git clone git@github.com:xuanly200106/<Name>.git` 克隆`master`
    +  `git checkout -b <branch name> <remote>/<branch name>` 创建本地并克隆分支

## 分支操作
#### 基本命令
- 查看当前分支 `git branch`
- 创建分支  `git branch <name>`
- 切换分支  `git checkout <name>`
- 创建并切换分支 `git checkout -b <name>`  
 实际为上面创建和切换分支的组合
- 删除分支 `git branch -d <name>`  
如果分支未合并要进行强制删除，则使用`git branch -D <name>`
- 分支合并 `git merge <branch name>`
    + 需要先切回要合并的分支
    + `Fast-forward`模式为默认模式，直接提交，合并很快，但是会在删除分支之后丢掉分支信息
    + 可以加入参数禁用`Fast-forward`
        * `git merge --no-ff -m "<tag>" <branch name>`
        * 由于会生成新的commit，所以需要`-m "<tag>"`
        * 此时会使用`recursive`模式
    + 产生冲突时，会显示`conflict`
        * 此时修改不同内容并保存之后，可以`git commit -m "<tag>"` 来进行重新合并
        * 或者`git merge --abort`进行取消
    + 可以用`git log --graph --pretty=oneline --abbrev-commit`查看合并状况

#### 分支策略 
- `master`应该为稳定版本，平时不在上面干活。一般在分支上干活，稳定了之后再合并入`master`上面。
- bug分支
    + 首先利用`git stash`储存工作区（隐藏当前的工作分支的修改情况）
    + 通过创建分支，处理完bug
    + 再通过`git checkout <hidden branch name>`，进入继续原工作，并且恢复工作区
        * 查看隐藏 `git stash list`
        * 恢复隐藏 `git stash apply <name>`，一般名字为`stash@{#}` （此时保留stash内容）
        * 删除隐藏 `git stash drop <name>`
        * 恢复隐藏 `git stash pop`，恢复同时删除stash内容
- feature分支
- 多人合作
    + 需要同步`master`分支和工作分支，bug只需要本地，feature看情况
    + 利用`git clone`和`git checkout <> <>/<>`同步`master`和工作分支
    + 如果发现冲突，利用`git pull`(track设置完毕后)或者`git pull <remote> <branch>`，将分支本地同步后合并，再push
    + track关联设置：`git branch --set-upstream branch-name origin/branch-name`
- rebase：当你领先master多个版本号时，使修改日志成线性，`git rebase`
    + 不使用rebase： orgin->1->2，别人提交origin->3，则最终为2与3merge
    + 利用`git rebase`: orgin->3->1->2
    + 使用步骤  
    ```
    git pull
    git rebase
    git push origin master
    ```
    + 线性的优点：无需交叉对比

## 标签管理
- 标签tag其实就是某个commit的指针
- 本地标签
    + 添加标签
        * `git tag <tagname>`切换到对应分支上后对于目前分支标签
        * `git tag <tagname> <commit id>`补之前的标签（id在log日志中查看）
        * `git tag -a <tagname> -m <info>`可以插入`-m`提供说明
    + 查看所有标签`git tag`
    + 查看标签信息`git show <tagname>`
    + 删除标签`git tag -d <tagname>`
- 远程标签
    + 推送一个本地标签`git push <remote> <tagname>`
    + 推送所有未推送的本地标签`git push <remote> --tags`
    + 删除远程标签
        * 先删除本地标签`git tag -d <tagname>`
        * 然后推送删除远程标签`git push <remote> :refs/tags/<tagname>`
## 参与项目
- `Fork`，在自己的目录下复制一个库，然后clone，推送修改
- 通过`pull request`，希望官方接受修改
    

## 补充内容
#### Git结构
- Working Directory（工作区）
- Repository（版本库）
    + Stage（暂存区）
    + Master（分支）---对应的指针HEAD
    
#### Windows Settings:
    $ git config --global user.name "xuanly200106"
    $ git config --global user.email "xuanly200106@foxmail.com"

#### 远程仓库设置：
1.创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：
    $ ssh-keygen -t rsa -C "youremail@example.com"  
你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。  
如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。
2.登陆GitHub，打开“Account settings”，“SSH Keys”页面：  
然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容

#### 分支管理
原来主分支为master，对应指针为HEAD  
创建分支dev，则产生了新的分支指针dev，并且将HEAD指向dev  
当前分支即为指针HEAD所对应的版本

#### 自定义
- 显示颜色`git config --global color.ui true`
- 忽略文件
    + 通过配置`.gitignore`文件导致
    + 参见https://github.com/github/gitignore[https://github.com/github/gitignore]
        * 忽略操作系统自动生成的文件，比如缩略图等
        * 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的.class文件
        * 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。
    + 无视忽略文件强制添加`git add -f <file>`
    + 通过忽略文件检查 `git check-ignore -v <file>`
- 配置别名
    + 格式：`git config --global alias.<Abb name> <real name>`
    + 常用
        ```
        git config --global alias.st status
        git config --global alias.co checkout
        git config --global alias.ci commit
        git config --global alias.br branch
        git config --global alias.unstage 'reset HEAD'
        git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
        ```
    + 查看修改
        * 仓库（无global选项）：通过查看`.git/config`文件可以查看修改情况（在alias后面）
        * 用户： 查看`.gitconfig`

<meta http-equiv="refresh" content="0.2">