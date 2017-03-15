# Linux

**初识涉及命令**

```
root/****** 登录
startx &    切换图形界面
Ctrl+Alt+F  切换虚拟终端
tty         查看当前终端设备
物理终端 - /dev/console
虚拟终端 - /dev/tty1
模拟终端 - /dev/pts/0

echo ${SHELL}    显示当前使用shell
cat /etc/shells  显示当前系统使用的所有shell
echo ${PS1}      查看环境变量显示
# 管理员
$ 普通用户

which    命令是查找命令是否存在,以及命令的存放位置在哪儿
which查找不到的命令,说明这个命令是shell的内建命令,例如cd
whereis  命令只能用于搜索程序名,而且只搜索二进制文件(参数-b),man说明文件(参数-m)和源代码文件(参数-s).如果省略参数,则返回所有信息.

type COMMAND  查看命令类型

Ctrl+c 取消命令执行
pwd    打印工作路径print work dir
```



