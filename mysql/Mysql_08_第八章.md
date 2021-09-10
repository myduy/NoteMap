环境
```mysql
use chapter07
```
备份
```bash
mysql -uroot -ppasswd chapter07 > C:/backup/chapter07.sql
```
还原
```bash
mysql -uroot -ppasswd chapter07 < C:/backup/chapter07.sql
```
备份多个
```bash
mysql -uroot -ppasswd --database chapter06 chapter07 >C:/backup/mul.sql
```
还原
```bash
mysql -uroot -ppasswd --database chapter06 chapter07 <C:/backup/mul.sql
```
备份全部
```bash
mysql -uroot -ppasswd --all-database  >C:/backup/all.sql
```
另一种还原
```bash
source filename.sql
```
sql用户表
```mysql
use mysql;
select * from user;
```
GRANT创建用户
用户名为user1 密码123 授权chapter08 student有查询权限
```mysql
GRANT SELECT NO chapter08.student To 'user'@'localhost'IDENTIFED BY '123';
CREATE USER创建用户
CREATE USER 'user2'@'localhost' IDENTIFIED BY '123';
INSERT创建用户
INSERT INTO  mysql,user(Host,USer,Passwd)
VALUES('localhost','user3',PASSWORD('123'));
```

```mysql
#生效
FLUSH PRIVILEGES;
#DROP USER删除用户
DROP USER 'user1'@'localhost';
#DELETE删除
DELETE FROM mysql.user WHERE Host='localhost' AND User='user2';
```
修改用户秘密
```bash
mysqladmin -u root -p password password
--->newpwd
--->ReNewpwd
```

root密码丢失
```bash
net stop mysql
mysqld --skip-grant-tables
mysql -uroot
```
```mysql
update mysql.uesr SET Password=PASSWORD('newpwd') WHERE User='root'
Flush PRIVILEGES;
```