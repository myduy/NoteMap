为在mysql内操作
外键
用于加强两个表数据之间的连接
环境

```mysql
CREATE DATABASE chapter05;
USE chapter05;

CREAte TABLE grade(
		id int(4) NOT NULL PRIMARY KEY,
		name varchar(36)
		);

CREATE TABLE student(
		sid int(4) NOT NULL PRIMARY KEY,
		sname varchar(36),
		gid int(4) NOT NULL
		);
```
#### 为表添加外键约束
`alter table student add constraint FK_ID foreign key(gid) REFERENCES grade (id);`

#### 删除外键约束
`alter table student drop foreign key FK_ID;`

关联关系
\1. 多对一
2.多对多
3.一对多

#### 添加数据
`alter table student add constraint FK_ID foreign key(gid) REFERNECES grade (id)`

#### 增加环境
```mysql
INSERT INTO grade(id,name) VALUES(1,'软件一班');
INSERT INTO grade(id,name) VALUES(2,'软件二班');
INSERT INTO student(sid,sname,gid) VALUES(1,'王红'，1);
INSERT INTO student(sid,sname,gid) VALUES(2,'李强'，2);
INSERT INTO student(sid,sname,gid) VALUES(3,'赵四'，3);
INSERT INTO student(sid,sname,gid) VALUES(4,'赫娟'，4) ;
```

(1)查询班级
SELECT id FROM grade WHERE name='软件一班';
(2)查询学生
SELECT sname FROM student WHERE gid=1;

#### 删除数据
删除学生
`delect from stdent where sname='王红'`
删除班级
`delect from * from grade;`
查询结果展示
`desc student;`
`desc grade;`

#### 连接查询
交叉连接
环境

```mysql
USE  chapter05;
CREATE TABLE dapartment(
		did int(4) NOT NULL primary key,
		dname varchar(36)
		);

CREATE TABLE example(
	id int(4) NOT NULL PRIMARY KEY,
	name varchar(36),
	age int(2),
	did int(4) NOT NULL 
	);

INSERT INTO department(did,dname)VALUSE(1,'网络部');
INSERT INTO department(did,dname)VALUSE(2,'媒体部');
INSERT INTO department(did,dname)VALUSE(3,'研发部');
INSERT INTO department(did,dname)VALUSE(4,'人事部');

INSERT INTO employee(id,name,age,did)VALUES(1,'王红',20,1);
INSERT INTO employee(id,name,age,did)VALUES(2,'李强',22.1);
INSERT INTO employee(id,name,age,did)VALUES(3,'赵四,'20.2);
INSERT INTO employee(id,name,age,did)VALUES(4,'赫娟',20.4);
```



#### 使用交叉语句查询
`SELECT * FROM department CROSS JOIN employss;`

#### 内连接
`SELECT employss.name,department.dname FROM department JOIN employss ON department.did=employee.did;`

#### 外连接
左连接
`SELECT department.did,department.dname,employee.name FROM department LEFT JOIN employee on department.did=employee.did;`
右连接
`SELECT department.did,department.dname,employee.name FROM department RIGHT JOIN employee on department.did=employee.did;`

﻿