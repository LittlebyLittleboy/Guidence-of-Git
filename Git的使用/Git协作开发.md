##### Linux下安装Git

$ sudo yum -y install git

$ sudo apt-get install git 

$ sudo wget https://; ./config，make，sudo make install

##### 查看仓库配置，并配置用户
$ git config --global --list
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"

##### 创建仓库
$ mkdir gitstudy
$ cd gitstudy
$ pwd

##### 初始化生成仓库
$ git init
$ ls -a 
$ touch readme.txt
$ echo hello,world > readme.txt
$ cat readme.txt

##### 提交到暂存区
$ git add readme.txt
$ git add file1,file2
##### 提交到本地仓库
$ git commit -m 'first commit'


##### 版本回退
$ git log
$ git log --pretty=oneline
$ git reset --hard HEAD^
$ git reset --hard HEAD~100

##### 查看修改状态
$ git status

##### 工作区和版本库里面最新版本的区别
$ git diff HEAD --readme.txt

##### 版本库中删除该文件
$ git rm test.txt

##### 版本库里的版本替换工作区的版本
$ git checkout --readme.txt

##### 创建远程仓库
$ git remote add origin git@github.com:michaelliao/learngit.git

##### 推送到远程库
$ git push -u origin master

##### 远程库克隆到本地
$ git clone git@github.com:michaelliao/gitskills.git


##### 分支管理


##### 创建并切换到分支
$ git checkout -b dev
##### 创建分支
$ git branch dev
##### 切换到分支
$ git checkout dev
##### 查看分支
$ git branch

##### 分支上进行操作
$ echo  create new branch > readme.txt
$ git add readme.txt 
$ git commit -m "branch test"

Git鼓励大量使用分支：

查看分支：git branch

创建分支：git branch <name>

切换分支：git checkout <name>

创建+切换分支：git checkout -b <name>

合并某分支到当前分支：git merge <name>

删除分支：git branch -d <name>



##### 多人协作的工作模式通常是这样：

多人协作时，大家都会往`master`和`dev`分支上推送各自的修改。

现在，模拟一个你的小伙伴，可以在另一台电脑（注意要把SSH Key添加到GitHub）或者同一台电脑的另一个目录下克隆：

```
$ git clone git@github.com:michaelliao/learngit.git
Cloning into 'learngit'...
remote: Counting objects: 40, done.
remote: Compressing objects: 100% (21/21), done.
remote: Total 40 (delta 14), reused 40 (delta 14), pack-reused 0
Receiving objects: 100% (40/40), done.
Resolving deltas: 100% (14/14), done.

```

当你的小伙伴从远程库clone时，默认情况下，你的小伙伴只能看到本地的`master`分支。不信可以用`git branch`命令看看：

```
$ git branch
* master

```

现在，你的小伙伴要在`dev`分支上开发，就必须创建远程`origin`的`dev`分支到本地，于是他用这个命令创建本地`dev`分支：

```
$ git checkout -b dev origin/dev

```

现在，他就可以在`dev`上继续修改，然后，时不时地把`dev`分支`push`到远程：

```
$ git add env.txt

$ git commit -m "add env"
[dev 7a5e5dd] add env
 1 file changed, 1 insertion(+)
 create mode 100644 env.txt

$ git push origin dev
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 308 bytes | 308.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To github.com:michaelliao/learngit.git
   f52c633..7a5e5dd  dev -> dev
```



首先，可以试图用git push origin <branch-name>推送自己的修改；



如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；



如果合并有冲突，则解决冲突，并在本地提交；



没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！



如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。

##### 小结

查看远程库信息，使用git remote -v；

本地新建的分支如果不推送到远程，对其他人就是不可见的；

从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；

在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；

建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；

从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。


