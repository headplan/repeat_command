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

# 数字增减
incrby num 5 # 加5
decrby num 2 # 减2
incr num # 加1
decr num # 减1

set float 1.11
incrbyfloat float 3.14
incrbyfloat float -0.25

# 二进制数据设置和获取
# python
import redis
r = redis.Redis()
r.set('bits', 0b10010100)
bin(int(r.get('bits')))
r.append('bits', 0b111)
bin(int(r.get('bits')))

# php
$r = new Redis();
$r->connect('127.0.0.1', 6379);
$r->ping();
$r->set('bits2', 0b10010100);
decbin($r->get('bits2'));
$r->append('bits2', 0b111);
decbin($r->get('bits2'));

# 设置和获取二进制位的值
setbit bit 0 1
setbit bit 2 1
getbit bit 2
bincount bit 2 1 # 计算二进制值为1的位的数量

# 二进制位运算
set b1 为01001101
set b2 为10110101
BITOP AND b1-and-b2 b1 b2 # b1-and-b2 = 00000101
BITOP OR b1-or-b2 b1 b2 # b1-or-b2 = 11111101
BITOP XOR b1-xor-b2 b1 b2 # b1-xor-b2 = 11111000
BITOP NOT not-b1 b1 # not-b1 = 10110010

# 客户端显示中文
redis-cli --raw
```

**散列**

```
# 设置关联域值对
hset message "id" 10086
hset message "name" "kony"
hset message "email" "abc@abc.com"

# 获取域关联的值
hget message "id"
hget message "name"
hget message "email"

# 仅当域不存在时设置关联域值对
hsetnx message "age" 18

# 检查域是否存在
hexists message "age"

# 删除给定域值对
hdel message "email"

# 获取散列包含的键值对数量
hlen message

# 批量操作
# 设置获取散列中多个域值对
hmset message2 "id" 10086 "name" "kony" "email" "abc@abc.com"
hmget message2 "id" "name" "email"

# 获取所有
hkeys message # 获取所有域
hvals message # 获取所有值
hgetall message # 获取所有域值对
```

列表

集合

有序集合

