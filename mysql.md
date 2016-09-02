# MySQL

### **MySQL管理**

**关闭开启服务**

```
ps -ef | grep mysqld # 检查MySQL服务是否启动
/usr/bin/mysqld_safe & # 启动MySQL服务器
/usr/bin/mysqladmin -u root -p shutdown # 关闭MySQL服务器
```

**用户设置**

```
use mysql;
INSTER INTO user
(
host,user,password,select_priv,insert_priv,update_priv
)
VALUES
(
'localhost','test',PASSWORD('test'),'Y','Y','Y'
);
FLUSH PRIVILEGES; # 重载授权表
SELECT host,user,password FROM user WHERE user='test';
```

> 注意:MySQL5.7中表user表的password换成**authentication\_string.**
> 
> select\_priv,insert\_priv,update\_priv为用户的权限.

```
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP
->ON TUTORIALS.*
->TO 'guest'@'localhsot'
->IDENTIFIED BY 'guest';
```

**管理命令**

```

```

