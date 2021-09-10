## 添加数据
### 配置环境

#### 1.建立数据库

```mysql
CREATE DATABASE chapter03;
```

#### 2.使用数据库

```mysql
USE chapter03;
```

#### 3.创建表

```mysql
CREATE TABLE student(
		id INT(4),
		name VARCHAR(20) NOT NULLL,
		grade FLOAT
		);
```

### 指定字段名插入数据

```mysql
INSERT INTO student (id,name)
VALUES
(1,'zhangsan')
(2,'koko')
(3.'mike')
;
```

### 不指定字段名插入数据  

```mysql
INSERT INTO student
VALUES
(4,'wangw',61.5)
(5,'liwu',61.5)
;
```

### 为指定字段添加值

```mysql
INSERT INTO student
set id=5,name='boya',grade=99;
```

更新数据
环境

|	id	|	name	|	grade	|
| ---- | ---- | ---- |
|	1 	|	zhang	|	98.5	|
|	2	|	list	|	95	|
|	3	|	wangwu	|	61.5	|

### UPDATE
更新部分数据

```mysql
UPTATE student
set name='caocao',grade=50
where id=1;
```

更新条件数据

```mysql
UPDATE student
set grade=100
WHERE id<4;
```

### update更新全部数据

``` mysql
UPDATE studio 
set grade=80;
```

### 删除数据

```mysql
DELETE FROM student
where id=1;
```

### 删除条件数据

```mysq
DELETE FROM student
where id<4;
```

### 删除全部数据

```mysql
DELETE FROM student;
```

### TRUNCATE删除

```mysql
TRUNCATE TABLE student;
```



﻿