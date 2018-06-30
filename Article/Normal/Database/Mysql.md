
# 启动关闭连接

```
// 设置别名
   $ alias mysql='/usr/local/mysql/bin/mysql'
   $ alias mysqladmin='/usr/local/mysql/bin/mysqladmin'
```

```
$ mysqladmin start                          // 启动
$ mysqladmin restart                        // 重新启动
$ mysqladmin -u root -p <password> shutdown // 关闭服务
```

```
$ mysql -u root -p // 连接服务器
```

# 修改密码

```
$ mysqladmin -u <username> -p <old password> <new password>
> SET PASSWORD FOR '<username>'@'<local host>' = PASSWORD('<new password>');
> SET PASSWORD = PASSWORD('<new password>');
```

# 数据库操作

## 引入外部 sql 文件

```
> source <sql file full path>;
```

## 数据库

```
> show databases;         // 显示数据库列表
> drop database <name>;   // 删除数据库
> create database <name>; // 创建数据库
```


