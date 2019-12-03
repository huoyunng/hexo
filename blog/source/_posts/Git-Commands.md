---
title: Git-Commands
date: 2019-12-03 16:17:38
tags: git
---

Git常用命令补白，欢迎指正

## Git常用命令

### 本地与远程关联:
- ###### 修改远程仓库地址(1.先删除，2.再重新关联，3.再重新推送到远端仓库)

```bash
git remote rm origin
git remote add origin [new-url]

例：
git remote rm origin
git remote add origin git@github.com:huoyunng/hexo.git
git push --set-upstream origin master
```

- ###### 将本地仓库关联远程仓库(分如下5步)

```bash
git remote add origin <server>
例：
步骤1.关联到远程仓库
git init
git remote add origin https://gitee.com/xweiv/spring-el.git

步骤2.查看远程仓库
git remote -v

步骤3.添加本地所有文件到本地git暂存区
git add .

步骤4.将本地暂存区提交到本地git仓库
git commit -m 'init commit.'

步骤5.将本地仓库提交到远程仓库
git push origin master -f
```

- ###### 将本地修改推送到远程仓库

```bash
git push --set-upstream origin master
```

- ###### 本地与远程仓库不一致，先同步远程仓库代码

```bash
$ git pull --rebase https://gitee.com/huoyoung/springboot.git master

强制推送
$ git push origin master -f
```

- ###### 提交本地test分支作为远程的master分支

```bash
git push origin test:master
```

- ###### 提交本地test分支作为远程的test分支
```bash
git push origin test:test
```

- ###### 撤回已经push的提交

```bash
使用git reflog找到commit的版本号
撤回到需要的版本
git reset --hard 947e6b6

重新提交, 如果报错，则执行下面的强制提交
会报错是因为：我们本地库HEAD指向的版本比远程库的要旧，此时强推上去，就可以了
git push
或
git push --force
或
git push -f
```

### git config配置:

- ###### 配置全局 用户名、邮箱

```bash
git config --global user.name "bryan sun"
git config --global user.email "hitsjt@gmail.com"
```

- ###### 查看配置

```bash
git config -l
或
git config --list
```

### 暂存操作(git stash):

```
1. 可用来暂存当前正在进行的工作
git stash save "alias"

2. 比如你需要恢复stash@{1}这时候你需要做的是：
# 将暂存的信息还原到本地
git stash apply stash@{1}

# 应用最后一次stash的内容
git stash pop

# 查看指定的暂存信息
git stash show stash@{1}

# 查看当前的暂存列表
git stash list

# 清空暂存栈
git stash clear  
```

### 分支的操作(创建、切换、删除...):

```
# 创建一个feature_x的分支，并切换过去
git checkout -b feature_x

# 切换回主分支
git checkout master

# 将新建的分支删除
git branch -d feature_x
```

### add操作:

```
1. 舍弃未 git add的代码时
舍弃单个文件
git checkout -- readme.md 或
git checkout pom.xml

舍弃本地所有未add的修改
git checkout .

2. 撤销已经add的操作(只是撤销add操作，本地修改不会丢失)
撤销单个文件
git reset HEAD readme.md

撤销所有add操作
git reset HEAD . 

3. 将本地修改add到暂存区
git add .
```

### commit操作:

```
1. 舍弃已经commit的修改(commit操作和代码都还原，即代码会丢失)
// 回退到上一次commit的状态
git reset --hard HEAD^ 或
git reset --hard HEAD~1

// 回退到指定版本的状态
git reset --hard commitid

// 回退到前3次的提交状态(即:回退到reflog中的第4个commit状态)
git reset --hard HEAD~3

2. 撤销已经commit的提交
// [git revert]命令意思是撤销某次提交。它会产生一个新的提交，虽然代码回退了，但是版本依然是向前的.
所以，当你用revert回退之后，所有人pull之后，他们的代码也自动的回退了

// 撤销最近一次提交的修改(只撤销修改，但提交操作不撤销)
git revert HEAD 或
git revert HEAD~0

// 撤销上上次的提交，注意：数字从0开始
// 使用revert HEAD~1 表示撤销最近2次提交，这个数字是从0开始的，如果你之前撤销过产生了commi id，那么也会计算在内的
git revert HEAD~1

// 撤销commitId0这次提交(撤销某个提交，生成一个新的提交)
// 如果使用 revert撤销的不是最近一次提交，那么一定会有代码冲突，需要你合并代码，合并代码只需要把当前的代码全部去掉，保留之前版本的代码就可以了.
git revert commitId0

3. 提交本地修改的代码
// 提交未add的代码 (未add和已add的都会提交)
$ git commit -am '修改说明'

// 提交已add的代码
$ git commit -m '修改说明'

// 修改刚刚的提交说明
git commit --amend

4. reset 与 revert的区别
reset：回退到某一个版本的状态，之后的版本不再保留
revert：撤销某一个版本，但保留之后的版本，并生成一个新提交版本
```

### 查看操作日志:

```
# 查看commit日志
git reflog
```

### 配置SSH公钥访问代码仓库:
##### SSH 公钥介绍
- ###### 腾讯开发者平台 支持使用 SSH 协议来访问 Git 仓库，提供账户 SSH 公钥和项目 SSH 公钥设置。 用户可以设置账户 SSH 公钥，获所有仓库的读写权限； 也可以在项目设置里面设置项目部署公钥，获取单个项目仓库的只读权限。有关 SSH 更多信息可参考 [维基百科](http://zh.wikipedia.org/zh/Secure_Shell)。

- 添加公钥后，您就可以在项目的代码页面点击 SSH 切换到 SSH 协议的 clone 地址，类似这样：
```
git@git.dev.tencent.com:wzw/leave-a-message.git
```

- 使用 SSH 协议来访问 Git 仓库，不需要每次链接都输入账号和密码。

**注意：一个公钥只能认证一个用户，而一个用户却可以拥有多个公钥。**

- 生成公钥命令

```bash
# 进入默认 ssh目录
> cd ~/.ssh

# 生成rsa公钥
> ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

# 用文本编辑器打开生成的『id_rsa.pub』文件，复制全部内容
```

- 登录 [Coding.net](https://dev.tencent.com/user/account/setting/keys) / [Github](https://github.com/settings/keys)，进入『SSH 公钥』页面，点击『新增公钥』

- 本地和github的ssh配置是否正确

```bash
$ ssh -T git@github.com

如果你看到了一句提示信息:
Hi (你的注册用户名)! You've successfully authenticated, but GitHub does not provide shell access.
那么说明已经配置好了github远程仓库与本地。

# coding用以下命令[coding.net 整合归腾讯了]
ssh -T git@git.dev.tencent.com
```

---

###### 相关问题

```
You have not concluded your merge (MERGE_HEAD exists) git拉取失败
解决步骤：
1. 保留你本地的修改
git merge --abort
git reset --merge
合并后记得一定要提交这个本地的合并
然后在获取线上仓库
git pull

2.down下线上代码版本,抛弃本地的修改
不建议这样做,但是如果你本地修改不大,或者自己有一份备份留存,可以直接用线上最新版本覆盖到本地
git fetch --all
git reset --hard origin/master
git fetch

git remove untracked files 的使用  (删除未监视的文件)
解决步骤：
用 git clean
# 删除 untracked files
git clean -f
# 连 untracked 的目录也一起删掉
git clean -fd
# 连 gitignore 的untrack 文件/目录也一起删掉 （慎用，一般这个是用来删掉编译出来的 .o之类的文件用的）
git clean -xfd
# 在用上述 git clean 前，墙裂建议加上 -n 参数来先看看会删掉哪些文件，防止重要文件被误删
git clean -nxfd
git clean -nf
git clean -nfd
```