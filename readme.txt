GitHub托管地址：
https://github.com/dangjunhui/learngit.git
------------------------------------------------------------------------
安装完成后，还需要最后一步设置，在命令行输入：
$ git config --global user.name "你再github上注册的用户名"
$ git config --global user.email "注册时候的邮箱"
--------------------------------------------------
$ git config --global user.name "dangjunhui"
$ git config --global user.email "616172218@qq.com"
创建一个版本库非常简单，首先，选择一个合适的地方，创建一个空目录：

$ mkdir learngit
$ cd learngit
$ pwd
/c/learngit
通过git init命令把这个目录变成Git可以管理的仓库：

$ git init
添加文件到Git仓库，分两步：
    第一步，使用命令git add <file>，注意，可反复多次使用，添加多个文件；
    第二步，使用命令git commit，完成。
$ git commit -m "wrote a readme file"

为了学Git先搭个服务器绝对是小题大作。好在这个世界上有个叫GitHub的神奇的网站，从名字就可以看出，这个网站就是提供Git仓库托管服务的，所以，只要注册一个GitHub账号，就可以免费获得Git远程仓库。
在继续阅读后续内容前，请自行注册GitHub账号。由于你的本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以，需要一点设置：
$ ssh-keygen -t rsa -C "616172218@qq.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/dangjunhui/.ssh/id_rsa):
Created directory '/c/Users/dangjunhui/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/dangjunhui/.ssh/id_rsa.
Your public key has been saved in /c/Users/dangjunhui/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:qYSY9HQve4Afrxn+QZF7oPmgRpd+vXZNioZvBBSWqwU 616172218@qq.com
The key's randomart image is:
+---[RSA 2048]----+
|        oo       |
|      E.o.       |
|  . . .o+.       |
| . = + =+=       |
|  o = @oS..      |
|   . *.@ o.   .  |
|    o * *o.. +   |
|   . . *..=.o .  |
|      +..=o.     |
+----[SHA256]-----+


现在，我们根据GitHub的提示，在本地的learngit仓库下运行命令：

$ git remote add origin git@github.com:michaelliao/learngit.git
$ git remote add origin git@github.com:dangjunhui/learngit.git


$ git push -u origin master  (第一次提交)
The authenticity of host 'github.com (192.30.255.113)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'github.com,192.30.255.113' (RSA) to the list of known hosts.
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 2.56 KiB | 2.56 MiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To github.com:dangjunhui/learngit.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
从现在起，只要本地作了提交，就可以通过命令：
$ git push origin master
把本地master分支的最新修改推送至GitHub，现在，你就拥有了真正的分布式版本库！
3dsMax2018day107.txt

要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；
git remote add origin git@github.com:dangjunhui/learngit.git；

关联后，使用命令git push -u origin master第一次推送master分支的所有内容；
此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；
分布式版本系统的最大好处之一是在本地工作完全不需要考虑远程库的存在，也就是有没有联网都可以正常工作，而SVN在没有联网的时候是拒绝干活的！当有网络的时候，再把本地提交推送一下就完成了同步，真是太方便了！

现在，远程库已经准备好了，下一步是用命令git clone克隆一个本地库：
$ git clone git@github.com:dangjunhui/gitskills.git

因此，多人协作的工作模式通常是这样：
    首先，可以试图用 git push origin branch-name 推送自己的修改；
    如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
    如果合并有冲突，则解决冲突，并在本地提交；
    没有冲突或者解决掉冲突后，再用git push origin branch-name推送就能成功！
如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream branch-name origin/branch-name。
这就是多人协作的工作模式，一旦熟悉了，就非常简单。
小结
    查看远程库信息，使用git remote -v；
    本地新的分支如果不推送到远程，对其他人就是不可见的；
    从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；
    在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；
    建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；
    从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。

退出vim
按了ESC后直接按:x






