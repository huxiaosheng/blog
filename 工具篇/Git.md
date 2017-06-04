[TOC]



# Git

bash属于命令行shell的一种



### 安装GIt

```
$ git config --global user.name "your name"
$ git config --global user.email　"email@example.com"
```



初始化一个Git仓库，使用`git init`命令



**远程仓库**

`ssh-keygen -t rsa -C "eamil@com"`



**添加文件到Git仓库**

1. 第一步，使用命令`git add<file>`,可反复多次使用，添加多个文件
2. 第二部，使用命令`git commit`，完成



**版本状态**

- 随时掌握工作区的状态，是用`git status`命令
- 如果`git status`告诉你有文件夹被修改郭，用`git diff`可以查看修改内容





**版本回退**

- `HEAD`指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard  cmmit_id`.
- 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。`--pretty=oneline`可以在log后面试试看
- 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本



**撤销修改**

- 场景1：当你改乱了工作区某个文件的内容，向直接丢弃工作区的修改时，用命令`git checkout -- file`。
- 场景2：当你不但乱改了工作区某个文件的内容，还提添加到了暂存区时，向丢弃修改，分两步，第一步命令`git reset HEAD file`,就回到了场景1，第二部按场景1操作。
- 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过提前是没有推送到远程库



**删除文件**

`git rm `删掉，并且`git commit`就从版本库中删除该文件



**添加一个远程库**

- 关联一个远程库 使用命令`git remote add roigin git@github.com:huxiaosheng/learngit.git`;
- 关联后，使用命令`git push -u origin master 第一次推送master分支的所有内容`



**从远程库克隆** 

`git clone git@github.com:huxiaosheng/gitskills.git`从github克隆到本地





## 分支管理

### 创建与合并分支

- 创建`dev`分支，然后切换到dev分支

```
$ git checkout -b dev
Switched to a new branch 'dev'

//-b 表示创建并切换，，相当于下面两条命令
$ git branck dev
$ git checkout dev
Switched to branch 'dev'
```



然后用`git branch`命令查看当前分支

```
$ git branch
* dev
  master
  
```

`git branch` 命令会列出所有分支，当前分支前面会标一个*号。
  然后，我们就可以`dev`分支上正常提交，比如对readme.txt做个修改，然后提交

```
$ git add readme.txt
$ git commit -m "branch test"
[dev fec145a] branch test
1 file changed, 1 insertion(+)
```



现在，`dev`分支工作完成，切换会`master`分支

```
$ git checkout master
Switched to branch 'master'
```



把`dev`分支合并到`master`上

```
$ git merge dev
Updating ....
Fast-forward.
..

```



删除分支

```
$ git branch -d dev
Deleted branch dev(was ..)
```



小结：

查看分支：`git branch`

创建分支：`git  branch <name>`

切换分支：`git checkout <name>`

创建+切换分支：`git checkout -b <name>`

合并某分支到当前分支：`git merge <name>`

删除分支：`git branch -d <name>`



查看分支合并图`git log --graph`

