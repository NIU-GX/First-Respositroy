## 1. git的几个区域

1.  工作区
2.  暂存区
3.  本地库

工作区    git add 【filename】  --->        暂存区          git commit 【filename】  ------>  本地库



## 2. git命令

### 1. 将某个文件夹设置为工作区

git init  ：可以初始化文件夹为git的工作区，会产生一个隐藏的文件夹[.git] 。

### 2. 设置git的签名

1.  设置当前工作区的签名

    git config user.name 牛高翔

    git config user.email xxx.@qq.com

    **工作区签名存储在当前文件夹的隐藏目录里**

2.  设置全局的签名

    git config --global user.name 牛高翔

    git config --global user.email xxx@qq.com

    **全局签名存储在C:\Users\NGX  系统用户目录下**

**需要注意的是：这个签名只是设置的本地属性，与gitbub或者gitee上的账户没有什么关系**

### 3. 查看当前工作区的状态

git status：可以查看哪些文件没有被add 或者 commit

### 4. 由工作区提交到暂存区

git add 【filename】： git add hello.txt

被add的文件将被追踪，git可以检测到文件是否经过修改，一个被修改的文件可以不经过add 直接 commit

### 5. 由暂存区提交到本地库

git commit 【filename】：git commit hello.txt

commit的时候要添加提交信息：会进入vim页面

git commit -m “提交信心” hello.txt : 可以直接为提交添加信息，不需要进入vim

### 6. 查看本地库的提交记录

git log ：这种状态多行显示，一个屏幕可能放不下

git log --pretty=oneline :  每条记录只显示一行，同时显示全部的哈希码

git log --oneline ：每条记录只显示一行，同时显示部分的哈希码

git reflog ： 每条记录只显示一行，显示HEAD@{id}

### 7. 版本的前进与后退

1.  使用索引值

    git reset --hard 【索引值】：先使用git reflog 查看版本信息，然后决定前往哪一个版本



2.  使用 ^ : 只能后退版本

    git reset --hard HEAD^    :  后退一个版本，几个 ^ 符号就后退几个版本

3.  使用~：只能后退版本

    git reset --hard HEAD~3 ：回退三个版本



resset命令的三个参数对比

 	1. --soft：仅在本地库移动HEAD指针
 	2. --mixed：在本地库移动HEAD指针，然后重置暂存区
 	3. --hard：在本地库移动HEAD指针，重置暂存区，重置工作区



### 8. 删除文件并找回

前提：删除前，文件存在时的状态提交到了本地库中

操作：git reset --hard HEAD [指针位置]

​	删除操作已经提交到本地库，指针指向历史记录

​	删除操作没有提交到本地库，指针指向HEAD

### 9. 比较文件差异

git diff 【filename】：将工作区中的文件和暂存区比较

git diff  HEAD [本地库中历史版本比较]

git diff 不加文件名可以比较当前工作区中的所有文件

git diff HEAD

## 3. 分支管理

### 1. 创建分支

git branch 【分支名】：

### 2. 查看分支

git branch -v

### 3. 切换分支

git checkout 【分支名】

### 4. 分支合并

1.  首先应该 切换到 接收合并的分支上，
2.  git merge 【分支名】

### 5. 冲突解决

1.  找到冲突的文件，进入文件，将文件中的特殊符号删除
2.  将文件修改到满意的程度
3.  使用 git add 【filename】  将文件添加到暂存区
4.  使用 git commit -m “xxxxxxx”  命令直接提交，此时不可以加文件名

## 4. github 操作

### 1. 在github上创建远程仓库

输入仓库名

### 2. 远程仓库设置

git remote add 【别名】  【仓库地址】



**git remote -v** 可以查看远程仓库的设置

### 3. 推送

将本地库推送到远程库

git push 【远程仓库名】 【分支名】

### 4. 克隆

git clone 【远程仓库地址】

1.  会自动初始化本地为git仓库
2.  完整的克隆远程库到本地

### 5. 拉取

pull =  fetch + merge

git fetch 【远程仓库名】  【远程分支名】

git merge 【远程仓库名】/ 【远程分支名】

git pull 【远程仓库名】  【远程分支名】

### 6. 协同开发冲突解决

两人修改用一个文件，会产生冲突。

要先拉取下来，解决完冲突才可以推送成功

### 7. fork 和 pull request

别人可以使用fork 拷贝某个仓库然后使用pull request 请求合并，等待仓库拥有者同意

### 8. ssh 免密登陆

1.  先进入user目录  C:\Users\NGX
2.  使用命令 ssh -keygen -t rsa -C 【邮箱】  ，   回车确认  
3.  会产生公钥和私钥   
4.  将公钥上传到github
5.  将github的ssh地址添加到本地的remote地址中 git remote add origin_ssh 【ssh地址】