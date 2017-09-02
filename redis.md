# Redis

**字符串**

```
# 为字符串设置键值
set msg "hello"
set msg "goodbye" # 覆盖
set num 10086
set nx-msg "没有这个key才创建,有了就不能创建了" NX
set xx-msg "没有这个key设置失败,有则覆盖value" XX
setnx new-msg "没有这个key才创建,有了就不能创建了" # 同nx参数.但成功返回1,失败返回0.

# 获取字符串的值
get msg
get num
get nx-msg
get xx-msg

# 设置获取多个字符串键值
mset kony::email "headplan@163.com" kony::name "headplan"
mget kony::email kony::name
msetnx yuan::email "abc@abc.com" yuan::name "yuan" # 同nx参数.但成功返回1,失败返回0

# 字符串键的命名(自定义分隔符)
user::10086::info
user|10086.info/abc

# 设置新值获取就值,如果设置的key也是新的,当然就获取不到旧的值了,但是也会设置成功
getset my-key "hello"

# 追加内容到value结尾,返回长度.当然,没有key也会创建
append akey "hello"
append akey "-world"

# 返回value长度
strlen akey

# 索引范围设置与取值
setrange t.msg 1 "appy" # 只接受正索引,覆盖内容
getrange t.msg 0 4
getrange t.msg -5 -1
```

散列

列表

集合

有序集合

