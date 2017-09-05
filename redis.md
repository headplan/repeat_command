# Redis

#### **字符串**

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

#### **散列**

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

# 数字操作
hincrby message age 1
hincrby message age -2
hset message height 183.5
hincrbyfloat message hight 2.5
hincrbyfloat message hight -1.2
```

#### **列表**

```
# 从列表的左右推入弹出的操作
lpush list "php"
lpush list "C"
lpush list "Linxu" "Lua" # 推入多个
rpush list "JS"
rpush list "Python" "Rubyf"
lpop list
rpop list

# 长度,索引和范围操作
llen list
lindex list 2
lindex list -3
lrange list 0 2
lrange list -3 -1

# 插入和删除数据
lset list 0 "Linux_c" # 修改数据
lindex list 0
lset list -1 "Python_c"
lindex list -1
linsert list before "php" "before_php" # 插入数据
linsert list after "php" "after_php"
rpush list C
rpush list C
rpush list C
lrem list 1 "C" # 从左删除1个C
lrem list -2 "C" # 从右删除1个C
lrem list 0 "C" # 删除所有C
ltrim list 1 3 # 裁剪list,trim掉不在(1,3)范围的其他内容

# 阻塞弹出
blpop/brpop empty-1 empty-2 10 # 都是空的list,阻塞10秒
blpop/brpop empty-1 empty-2 list 10 # 哪里有值哪里弹出
blpop/brpop empty-1 empty-2 20 # 另开一个客户端,push到list中值,马上停止并弹出(20秒之内)
```

#### **集合**

```
# 集合操作
sadd friends "小明" "小红" "小花" # 添加
srem friends "小花" # 移除
sismember friends "小花" # 检查是否存在
scard friends # 统计个数
smembers friends # 返回所有元素
spop friends # 随机弹出一个元素
SADD friends "peter" "jack" "tom" "john" "may"
SRANDMEMBER friends # 随机的返回一个元素
SRANDMEMBER friends 3 # 随机的返回三个无重复的元素,最多返回元素总数
SRANDMEMBER friends -3 # 随机的返回三个可能有重复的元素,最多返回指定个数,所以会有很多重复的.

# 集合运算操作
sadd number1 "123" "456" "789"
sadd number2 "123" "456" "999"
sdiff number1 number2 # 计算差集
sdiffstore mydiff number1 number2 # 计算差集并存储在mydiff中
sinter number1 number2 # 计算交集
sinterstore myinter mumber1 number2 # 计算交集并存储在myinter中
sunion number1 number2 # 计算并集
sunionstore myunion number1 number2 # 计算并集并存储在myunion中
```

#### **有序集合**

```
# 集合操作
zadd fruits-price 3.2 "香蕉" # 添加元素
zadd fruits-price 2.0 "西瓜"
zadd fruits-price 4.0 "石榴" 7.0 "梨" 6.8 "芒果"

zrem fruits-price "香蕉" "西瓜" # 删除元素

zadd fp 3.2 "香蕉" 2.0 "西瓜" 4.0 "石榴" 7.0 "梨" 6.8 "芒果"
zscore fp "芒果" # 返回关联分值
zincrby fp 1.5 "西瓜" # 增加或减少分值
zincrby fp -0.8 "芒果"
zcard fp # 返回元素数量
zrank fp "西瓜" # 返回西瓜的正排名,这里排1,从0开始
zrevrank fp "西瓜" # 返回西瓜的反排名,这里排名3,也是从0开始,只不过是反着的.

# 分值范围操作
zrange fp 0 2 # 返回索引升序元素
zrange fp 0 2 withscores # 返回索引升序元素,带分值
zrevrange fp 0 2 # 返回索引降序元素
zrevrange fp 0 2 withscores # 返回索引降序元素,带分值

zrangebyscore fp 1.0 5.0 # 返回分值升序元素
zrangebyscore fp 1.0 5.0 withscores # 返回分值升序元素,带分值
zrangebyscore fp 1.0 5.0 withscores limit 1 3 # 返回分值升序元素,带分值,这里的limit和mysql中的一样
zrevrangebyscore fp 1.0 5.0 # 返回分值降序元素
zrevrangebyscore fp 1.0 5.0 withscores # 返回分值降序元素,带分值
zrevrangebyscore fp 1.0 5.0 withscores limit 1 3 # 返回分值降序元素,带分值,这里的limit和mysql中的一样

zcount fp 1.0 3.5 # 计算给定分值范围内的元素数量

zremrangebyrank fp 0 1 # 删除索引范围元素
zremrangebyscore fp 3.9 7.0 # 删除分值范围元素

# 集合运算操作
zadd fruits-8-13 300 "apple" 200 "banana" 150 "cherry" # 8 月 13 日水果销量
zadd fruits-8-14 250 "apple" 300 "banana" 100 "orange" # 8 月 14 日水果销量
zunionstore fruits-8-13&14 2 fruits-8-13 fruits-8-14 # 计算两天水果的总销量
zrange fruits-8-13&14 0 -1 WITHSCORES # 查看集合
zinterstore fruits-8-13&14-pop 2 fruits-8-13 fruits-8-14 # 计算两天畅销的水果
zrange fruits-8-13&14-pop 0 -1 WITHSCORES # 查看集合
```

#### HyperLogLog

```
pfadd hll a b c d e f g # 添加元素
pfadd hll2 1 2 3 4 5 6 7
pfcount hll # 统计返回估算值
pfcount hll hll2 # 统计返回估算值
pfmerge hll-all hll hll2 # 合并多个HyperLogLog
pfcount hll-all
```

---

#### 处理数据库中的单个键

```
type msg # 查看类型
type list
del hll2 # 删除键
del test abc
exists wtf # 检查键是否存在
exists hll
rename msg msg2 # 键改名,msg必须存在,msg2存在则覆盖
rename msg msg2 # 键改名,msg必须存在,msg2存在则不变,不存在才改名
```

#### 键过期

```
# 键生存时间
set msg "hello world"
expire msg 5
exists msg

set num 10086
pexpire num 5500
exists num
```



