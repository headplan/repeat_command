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

```

