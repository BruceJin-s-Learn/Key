# Git

## .1 学习思路

1.这个技术是什么

2.优点，为什么学

3.缺点，如何避免

## .2 版本控制

1、本地

+ 自嗨，无法协同操作

2、集中化（CVCS）

+ 单点故障
+ 多个仓库，资源浪费

3、分布式（DVCS）

+ 每个电脑自己带了一个本地仓库

## .3 Git设置个人

用户名和邮箱

```linux
git config --global user.name ""
git config --global user.email ""
```

![image-20201208104854055](Git.assets/image-20201208104854055.png)

## .4 Git三种状态和工作模式

4.1 工作模式及工作区域

![image-20201208105925485](Git.assets/image-20201208105925485.png)

工作区、暂存区、git仓库

4.2 三种状态

已提交`committed`、已修改`modified`、已暂存``

## .5 常用命令

```linux
//常用
git init
git status
git add 目录/文件名
git commit -m "注释"
git commit -am "注释" = add+commit //第一次提交本文件不可以

//查看日志
git log
git log --pretty=oneline //一行显示
git reflog //查看唯一标识
git diff HEAD -- 文件名 //看不同，在未提交之前（modified）

//回退
git reset --hard HEAD^^^^ //回退几次有几个^
git reset --hard 唯一标识 //唯一标识通过reflog查看
git reset --hard HEAD~'数字' //回退版本
git reset HEAD file //撤消操作
git restore --staged file //从暂存区撤回，注意版本有的没--help查看
git restore file //撤销文件中内容

//删除
git checkout file //从版本库，误删拉取
git rm -f
删除文件，提交操作

//快捷键
Tab自动补全
ctrl+ins复制粘贴
```

## .6 拉取和推送

```linux
git clone 网址(https)

(新建一个仓库，可看到，不选readme等)
create a new repository on the command line//创建新的存储库
echo "# test" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main //分支重命名
git remote add origin https://github.com/VideJin/test.git//远程添加
git push -u origin main//推送

//推送已有的存储库到远程
git remote add origin https://github.com/VideJin/test.git
git branch -M main
git push -u origin main
```

## .7  SSH

ssh比https更安全和快速

+ 需要公钥SSH Keys

+ 本地git客户端 `ssh-keygen -t rsa -C "GitHub账户邮箱"`

+ settings中配置ssh

+ 检测`ssh -T git@github.com`

+ 使用ssh推送

 ```git
git remote add origin git@github.com:VideJin/test.git
git branch -M main
git push -u origin main
 ```

## .8 分支

### 8.1 本地操作

```git
git checkout branch //切换分支
git checkout -b new_branch //新建并切换到新分支

git branch //查看所有分支
git branch -m oldbranch newbranch //重命名

git merge branch //合并分支 注：先切换到主分支再合并

git branch -d branch //删除指定分支
```

### 8.2 远程操作

```git
git branch -a //查看本地和远程分支
//push
git push origin file/branch_name //推送
//pull
git checkout -b local_branch origin/remote_branch //拉取远程指定分支并在本地创建分支
//删除
git push origin : file/remote_branch //只删除远程的

git fach // 查看状态
```

## .9 冲突

### 9.1 本地

#### 9.1.1 产生原因

两个以上的分支commit后会造成

![image-20201209215234499](Git.assets/image-20201209215234499.png)

主动修改本地文件然后提交

### 9.2 多人

#### 9.2.1 原因

拉取远程库dev 并在本地创建dev开发库,执行命令 `git checkout -b dev origin/dev` 这里以同台机器不同窗口来模拟两个用户操作同一分支同一文件(实际开发时多人操作统一文件冲突情况比较常见)

#### 9.2.2 解决

.1 先执行 pull 拉去操作

`git pull`

.2 `cat`查看冲突文件内容

.3 本地处理，而后`push`

## .10 标签管理（版本管理）

### 10.1 常用命令

```git
git tag name //默认最后一次提交的-m 即HEAD
git tag -a name -m "dericr"

git tag
//推送
git push origin name //本地到远程
git push origin --tags //推送所有
//删除
git push origin:refs/tsafs/name //远程 
git tag -d name //本地
```

## .11 idea下git基本操作

> idea 添加：启动页 -> configure -> settings -> version control -> git

![image-20201210095952619](Git.assets/image-20201210095952619.png)

### 11.1 远程到本地

file -> new -> project from version control

![image-20201210102150293](Git.assets/image-20201210102150293.png)

### 11.2 本地到远程

+ 项目右键

+ VCS
  + remotes 绑定远程

+ 快捷导航栏

### 11.3 分支

+ 右下角分支图标中
  + 新建
  + 推送
  + 删除
  + 合并

+ 左下角git中可查看Log和diff操作

+ 冲突

  + 本地
  
    
  
  + 远程（多人协同）
  
    

### 11.4 插件：ignore

忽略一些我们不想提交的文件

生成一个gitignore文件，把想忽略的文件添加进去

注：若想忽略的文件加到暂存区则不会忽略成功

## .12 问题