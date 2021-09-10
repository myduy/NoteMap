环境
```mysql
CREATE DATABASE chapter07;
USE chapter07;
CREATE TABLE student(
s_id INT(3),
name VARCHAR(20),
math FLOAT,
chinese FLOAT
);
INSERT INTO student VALUES 
(1,'"TOM',80,78),
(2,'"Jack',70,80),
(3,'"Lucy',97,95);
```

```bash
mysql> select * from student;
+------+-------+------+---------+
| s_id | name  | math | chinese |
+------+-------+------+---------+
|    1 | "TOM  |   80 |      78 |
|    2 | "Jack |   70 |      80 |
|    3 | "Lucy |   97 |      95 |
+------+-------+------+---------+
3 rows in set (0.00 sec)
```



#### 创建视图

```mysql
CREATE VIEW view_stu AS SELECT math,chinese,math+chinese FROM student;
```
#### 查询view_stu

```mysql
SELECT * FROM view_stu;
```

```bash
mysql> SELECT * FROM view_stu;
+------+---------+--------------+
| math | chinese | math+chinese |
+------+---------+--------------+
|   80 |      78 |          158 |
|   70 |      80 |          150 |
|   97 |      95 |          192 |
+------+---------+--------------+
3 rows in set (0.01 sec)
```



#### 自定义字段名称

```mysql
CREATE VIEW view_stu2(math,chin,sum) AS SELECT math,chinese,math+chinese FROM student;
SELECT * FROM view_stu2;
```

```bash
mysql> SELECT * FROM view_stu;
+------+---------+--------------+
| math | chinese | math+chinese |
+------+---------+--------------+
|   80 |      78 |          158 |
|   70 |      80 |          150 |
|   97 |      95 |          192 |
+------+---------+--------------+
3 rows in set (0.01 sec)

mysql> CREATE VIEW view_stu2(math,chin,sum) AS SELECT math,chinese,math+chinese FROM student;
Query OK, 0 rows affected (0.01 sec)

mysql> SELECT * FROM view_stu2;
+------+------+------+
| math | chin | sum  |
+------+------+------+
|   80 |   78 |  158 |
|   70 |   80 |  150 |
|   97 |   95 |  192 |
+------+------+------+
3 rows in set (0.00 sec)
```

#### 多表查询

```mysql
CREATE TABLE stu_info(
s_id INT(3),
class VARCHAR(50),
addr VARCHAR(100)
);
INSERT INTO stu_info(s_id,class,addr) VAlUES 
(1,'erban','anhui'),
(2,'sanban','chongqing'),
(3,'siban','shandong');
SELECT * FROM stu_info;
```

```bash
mysql> SELECT * FROM stu_info;
+------+--------+-----------+
| s_id | class  | addr      |
+------+--------+-----------+
|    1 | erban  | anhui     |
|    2 | sanban | chongqing |
|    3 | siban  | shandong  |
+------+--------+-----------+
3 rows in set (0.00 sec)
```

```mysql
CREATE VIEW stu_class(id,name,glass)
AS
SELECT student.s_id,student.name,stu_info.class
FROM student,stu_info
WHERE student.s_id=stu_info.s_id;
```
```bash
mysql> SELECT * FROM stu_class;
+------+-------+--------+
| id   | name  | glass  |
+------+-------+--------+
|    1 | "TOM  | erban  |
|    2 | "Jack | sanban |
|    3 | "Lucy | siban  |
+------+-------+--------+
3 rows in set (0.01 sec)
```


```mysql
#查看视图
DESC view_stu
#查看视图基本信息
SHOW TABLE STATUS LIKE "视图名" \G;
SHOW CREATE VIEW 视图名
#创建修改视图
CREATE OR REPLACE VIEW view_stu AS SELECT * FROM student;
#修改视图
ALTER VIEW view_stu AS SELECT chinese FROM student;
#更新视图
UPDATE view_stu SET chinese =100 ;
#用视图删除数据
DELETE FROM view_stu2 WHERE math=70;
#删除视图
DROP VIEW IF EXISTS view_stu;
```