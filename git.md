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

```
