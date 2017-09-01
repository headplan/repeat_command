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
```

散列

列表

集合

有序集合

