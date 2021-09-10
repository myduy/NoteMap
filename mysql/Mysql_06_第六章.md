#### 开启事务

```mysql
START TRANSACTION;
```
#### 提交事务

```mysql
COMMIT;
CREATE DATABASE chapter06;
USE chapter06;
CREATE TABLE account(
	id INT primary key auto_increment,
	name VAR CHAR(40),
	money FLOAT 
	);
INSERT INTO account(name,money) VALUES('a',1000);
INSERT INTO account(name,money) VALUES('b',1000);
```
#### 事务回滚
`ROLLBACK;`

## 事务隔离级别
`READ UNCOMMITIED(读未提交）`
`#READ COMMITIED(读提交）`
`REPEATABLE READ(可重复读）`
`SERIALIZABLE（可串行化）`

#### 脏读

```mysql
START TRANSACTION;
UPDATE account SET money=money-100 WHERE name='a';
UPDATE account SET money=money+100 WHERE name='b';
```

#### 1)设置b账户的隔离级别
SESSION 当前会话 	TRANSATION事务	 ISOLATION隔离 	LEVEL级别 	READ UNCOMMITTED隔离级别

```mysql
SET SESSION TRANSACTION ISOLATTON LEVEL READ UNCOMMITTED;
```

#### 查询事务的隔离级别

```mysql
SELECT @@tx_isolation；
```
mysql8以上
```mysql
select @@transaction_isolation;
```

### (2)演示脏读

```mysql
START TRANSATION;
		SELECT * FROM account;
		#-----------------------------------
		#|id	|name	|money	|
		#-----------------------------------
		#|1	|a	|1000	|
		#-----------------------------------
		#|2	|b	|1000	|
		#-----------------------------------
		START TRANSATION;
		UPDATE account SET money=money-100 WHERE name='a';
		UPDATE account SET money=money+100 WHERE name='b';
		#再次查询
		SELECT * FROM account;
		#-----------------------------------
		#|id	|name	|money	|
		#-----------------------------------
		#|1	|a	|900	|
		#-----------------------------------
		#|2	|b	|1100	|
		#-----------------------------------
		#验证是否脏读
		START TRANSACTION;
		#退出数据库
		#再次查询
		SELECT * FROM account;
		#-----------------------------------
		#|id	|name	|money	|
		#-----------------------------------
		#|1	|a	|1000	|
		#-----------------------------------
		#|2	|b	|1000	|
		#-----------------------------------
```
### 事务储存
环境

```mysql
USE chapter06;
CREATE TABLE student(
	id INT(3) PRIMARY KEY AUTO_INCREMENT,
	name VARCHAR(20) NOT NULL,
	grade FLOAT,
	gender CHAR(2)
	);
INSERT INTO student(name,grade,gender)
	VALUES("tom",60,"男"),
	("jack",70,'男'),
	('rose',90,'女'),
	('lucy',100,'女');
```

例

#### 创建查看stdent表的储存过程

```mysql
CREATE PROCEDURE Proc()
	BEGIN				
	SELECT * FROM student;                      
	END;
```
执行过程
```mysql
DELIMITER //
CREATE PROCEDURE Proc ()
	BEGIN
	SELECT * FROM student;
	END //
DELIMITER ;
```
#### 调用Proc();

```mysql
call Proc();
```
### 变量
格式
DECLARE 变量名  数据类型  default 变量值；
赋值
SET 变量名 = 变量值 ；
例

```mysql
delimiter //
CREATE PRODUCERE Proc1()
BEGIN
DECLARE var1 var2 var3 INT ;
SET var1=10 ,var2=20;
SET var3=var1+var2;
SELECT var3;
END //
delimiter ;
```

例题

#### 赋值查询

```mysql
demiliter //
create procedure proc2()
     begin
     DECLARE s_grade FLOAT;
     DECLARE s_gender CHAR(2);
     SELECT grade,gender INTO s_grade,s_gender
     FROM student  WHERE name='rose';
     end//
demiliter ;
```

#### 声明光标

```mysql
DECLARE 名 CURSIR FOR 结果集
```
#### 声明名为cursor_student的光标

```mysql
DECLARE cursor_student CURSIR FOR select s_name,s_gender FROM student;
```

#### 光标的使用

```mysql
OPEN CURSOR_NAME
FETCH cursor_name INTO var_name[,var_name]...
```

#### 使用cursor_student的光标，将查询信息存入 s_name,s_gender;

```mysql
FETCH cursor_student INTO s_name,s_gender;
```

#### 关闭光标

```mysql
CLOSE cursor_name
```
流程控制
判断语句
IF 变量名 is 变量值
	执行代码
END IF;

指定值语句
CASE 变量值
	执行代码
END CASE;

循环语句
[自定义循环名】:LOOP
	执行代码
END LOOP [自定义循环名]

退出循环相当于java的break
LEAVE [自定义循环名】
退出循环相当于java的continue
ITERATE [自定义循环名】

带条件循环
label:REPEAT
执行代码
UNTIL 条件
END REPEAT lable；

WHILE

#### 先判断循环

```mysql
DECLRE i INT DEFAULT 0;
WHILE i<10 DO
SET i=i+1;
END WHILE;
```

#### 查询储存执行过程

```mysql
SHOW PEOCEDURE STATUS LIKE 'C%' \G
SHOW CREATE PROCEDURE chapter06.proc \G
```
#### 修改储存过程

```mysql
ALTER RPOCEDURE proc 
MODIFIES SQL DATA 
SQL SECURIty INVOKER;
```

#### 删除储存过程

```mysql
DROP PROCEDUCE proc;
```