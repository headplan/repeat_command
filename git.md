# Git

**全局配置Git仓库用户名和email地址**

```
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
```

**创建版本库**

```
mkdir test
cd test
pwd
git init
ls -ah
```

**把文件添加到版本库**

```
touch README
git add README
git commit -m "readme file"
```

**把多个文件添加到版本库**

```
touch file1 file2 file3
git add file1
git add file2 file3
git commit -m "add 3 files"
```

**时光机穿梭**

```
vim README
git status # 随时查看工作区的状态
git diff README
git add README
git commit -m "add distributed"
```

**版本回退**

```
git log
git log --pretty=oneline # 只显示版本号和提交时的描述
git reset --hard HEAD^ # HEAD^^表示上上个版本,HEAD~10上10个版本
git reset --hard 4d20cfd # 使用版本号前8位
git reflog # 查看所有分支的commit和reset记录
```

**工作区-&gt;暂存区-&gt;版本库**

**管理修改**

```
vim README # 修改内容
git diff README # 查看本身和缓冲区的不同
git add README
git diff HEAD -- README # 查看暂存区和版本库比较
```

**撤销修改**

```
vim README # 修改内容
git status
git checkout -- README # 丢弃add之前的修改,重新检出文件
git reset HEAD README # 撤销add的修改
git checkout -- README # reset之后执行恢复最初的原样
git reset --hard HEAD^ # commit之后,可以回退到上一个版本
```

**删除文件**

```
rm file1
git rm file1 # 从版本库中删除
git commit -m "确认删除文件,这也是一次提交修改"
rm file2
git checkout -- file2 # 如果误删了文件,可以重新检出
```

**远程仓库**

```
ssh-keygen -t rsa -C "headplan@163.com"
github # 设置秘钥对文件名
vim config
Host github.com www.github.com
    IdentityFile ~/.ssh/github
# 进入 Account settings 设置公钥
# 把本地仓库连接到远程仓库
git remote add git-command git@github.com:headplan/git-command.git
git push -u git-command master # 把本地库的所有内容推送到远程库,第一次使用-u参数
git clone git@github.com:headplan/git-command.git # 从远程库克隆
```

**分支管理**

```
git branch # 查看分支
git branch dev # 创建分支
git checkout dev # 切换分支
git checkout -b dev # 创建并切换到分支
touch file4
git add file4
git commit -m "添加file4文件"
git checkout master
git merge dev # 合并某分支到当前分支,Fast-forward表示没有冲突快速合并
git branch -d dev # 删除分支
```

**解决冲突**

```
git checkout -b dev
vim README
git add README
git commit -m "修改了最后一行"
git checkout master
vim README
git add README
git commit -m "同样修改了最后一行"
git merge dev
# 提示合并冲突了Merge conflict
vim README # 修改冲突
git add README
git commit -m "修改完冲突后提交"
git log --graph --pretty=oneline --abbrev-commit # 展示精简log
# --graph:冲突的提交
# --pretty=oneline:只显示一行
# --abbrev-commit:显示短的提交标识
git branch -d dev # 删除分支
```

**标签管理**

**使用GitHub**

**自定义Git**

