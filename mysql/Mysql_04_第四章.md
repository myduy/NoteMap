## 配置环境
1.创建数据库

```mysql      
CREATE DATABASE chapter4;
```
2.使用数据库

```mysql
USE chapter4
```
3.创建表
```mysql      
CREATE TABLE student(
		id INT(3) PRIMARY KEY AUTO_INCREMENT,
		name VARCHAR(20) NOT NULL，
		grade FLOAT,
		gender CHAR(2)
		);
```
4.插入记录
```mysql      
INSERT INTO student(name,grade,gender)
VALUES('songjiang',40,'男'),
('wuyong',100,'男'），
('qianming',90,'男'),
('husanning',88,'女'),
('sunnerniang',66,'女'),
('wusong',86,'男'),
('linchong',82,'男'),
('yanqing',90,NULL); 
```
### 1.查询student表中的记录

```mysql      
SELECT id,name,grade,gender FROM student;
```
```mysql      
SELECT * FROM student;
```
#### 2.按条件查询

```mysql      
SELECT id,name FROM student WHERE id=4;
```
```mysql      
SELECT * FROM student WHERE name='wusong';
```
```mysql      
SELECT * FROM student WHERE grade>80;
```
#### 3.带IN关键字查询

```mysql      
SELECT * FROM student WHERE id IN (1,2,3);
```
#### 4.带BETWEEN AND 关键字查询

```mysql      
SELECT * FROM WHERE id BETWEEN 2 AND 5;
```
#### 5.空值查询

```mysql      
SELECT  * FROM student WHERE gender IS NULL
```
#### 6.带DISTINCT关键字查询

```mysql      
SELECT DISTINCT gender,name FROM student;
```
#### 7.带LIKE关键字查询
百分号匹配符号

```mysql      
SELECT  * FROM student WHERE name LIKE "s%g";
```
下划线精确匹配符号
```mysql      
SELECT * FROM student WHERE name LIKE '_u_ong';
```
#### 8.带AND关键字的多条件查询

```mysql      
SELECT * FROM student WHERE id<5 AND gender='女'; 
```
#### 9.带OR关键字的多条件查询

```mysql      
SELECT * FROM student WHERE id<5 OR gender='女';
```