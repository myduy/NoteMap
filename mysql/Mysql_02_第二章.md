为初始化MYSQL
$mysql_secure_installation

创建数据库名为itcast
```MySQL
CREATE DATABASE itcast;
```

查看数据库
```MySQL
SHOW DATABASES:
```
查看创建好的itcast数据库信息
```MySQL
SHOW CREATE DATABASE itcast;
```
修改数据库itcast的的编码修改为gbk
```MySQL
ALTER DATABASE itcast DEFAULT CHARACTER SET gbk COLLATE gbk_bin;
```
删除数据库itcast
```MySQL
DROP DATABASE itcast;
```
### 数据类型

#### 整形类型
| 数据类型	| 字节 |
| ---- | ---- |
| TINYINT	| 1 |
| SMALLINT	| 2 |
| MEDIUMINT	| 3	|
| INT		| 4	|
| BIGING	| 8	|

#### 浮点数类型和定点数据类型	
| 数据类型	| 字节 |
| ---- | ---- |
| FLOAT	| 4	|
| DOUBLE	| 8	|
| DECIMAL(M,D)	| M+2	|

#### 日期与时间类型
| 数据类型	| 字节	| 日期格式	|
| ---- | ---- | ---- |
| YEAR | 1 	| YYYY |
| DATE | 4	| YYYY-MM-DD |
| TIME	| 3	| HH:MM:SS	|
| DATATIME	| 8	YYYY-MM-DD HH:MM:SS	|
| TIMESTAMP	| 4	YYYY-MM-DD HH:MM:SS	|

#### 字符串和二进制
| 数据类型	|	类型说明	|
| ---- | ---- |
| CHAR	| 固定长度字符串	|
| VARCHAR	| 可变长度字符串	|
| BINARY	| 固定长度的二进制数据	|
| VARBINARY	| 可变长度的二进制数据	|
| BLOB	| 二进制大数据	|
| TEXT	| 大文本数据	|
| ENUM	| 枚举类型，储存一个枚举字符集	|
| SET	| 字符串对象	|
| BIT	| 位字段类型	|

#### 空间类型
|	数据类型	|
|	----	| 
|	GEOMETRY	|
|	POINT	|
|	LINESTRING	|
|	POLYGON	|

### 创建数据表步骤 数据库名称gb_grade

|	字段名称	|	数据类型	|	备注说明	|
| ---- | ---- | ---- | 
|	id	|	INT(11)	|	学生的编号	|
|	name	|	VARCHAR	|	学生的姓名	|
|	grade	|		FLOAT	|	学生的成绩	|

步骤一：
创建数据库
\#CREATE DAATABASE itcast;
步骤二：
选择数据表
\#USE itcast;
步骤三：

##### 创建数据表

```MySQL
CREATE TABLE tb_grade
	(
	id	INT(11),
	name	VARCHAR(20),
	grade	FLOAT
	);
```
##### 查看数据表的方法；

```MySQL
SHOＷ　CREATE TABLE td_grade；
SHOＷ　CREATE TABLE td_grade \G
#DESC/DESCRIBE td_grade;
```

字段讲解
（1）NULL:表示该列是否可以储存NULL值
（2）Key:表示该列可以编制索引
（3）Default:表示该列的默认值
（4）EXtra：获取到给定的附加信息

##### 修改表名
td_grade旧表名	grade新表名

```MySQL
ALTER TABLE td_grade RENAME TO grade;
```
##### 查看数据表

```MySQL
SHOW TABLES;
```
##### 修改字段名
grade表名 	name旧字段	username新字段	VARCHAR(20)新字段类型

```MySQL
ALTER TABLE grade CHANGE name username VARCHAR(20);
```
##### 修改字段数据类型
grade表名		id字段名		INT(20)数据类型

```MySQL
ALTER TABLE grade MODIFY id INT(20);
```
##### 添加字段
grade表名		age新字段		数据类型INT(10)

```MySQL
ALTER TABLE grade ADD age INT(10);
```
##### 删除字段
grade表名		age字段名

```MySQL
ALTER TABLE grade DROP age;
```
##### 修改字段的排列位置
grade表名		username字段名1	VARCHAR(20)	FEITST第一个位置

```MySQL
ALTER TABLE grade MODEFY username VARCHAR(20) FIRST;
```
##### 修改字段插入到grade后面
第一个grade表名	id字段名	INT(20)数据类型	第二个grade字段名

```MySQL
ALTER TABLE grade MODIFY id INT(20) AFTER grade;
```
##### 删除数据表
grade表名

```MySQL
DROP TABLE grade;
```
### 表的约束

| 约束条件	|	说明  |
| ---- | ---- |
| PRIMARY KEY	|	主键约束，用于唯一标识对应记录	|
| FOREIGN KEY	|	外键约束	|
|	NOT NULL	|	非空约束	|
|	UNIQUE	|	唯一性约束	|
|	DEFAULT	|		默认值约束，用于设置字段默认值	|

##### 主键约束
1.单字段主键
example01表名	id/name/grade字段名	INT/VARCHAR/FLOAT数据类型 	PRIMARY KEY主键约束

```MySQL
CREATAE TABLE example01(id INT PRIMARY KEY,
			name VARCHAR(20),
			grade FLOAT);
```
2.多字段主键
example02表名	stu_id/course_id/grade字段名 INT/FLOAT数据类型
```MySQL
CREATE TABLE example02(stu_id INT,
			course_id INT,
			grade FLOAT,
			PRIMARY KEY(stu_id,course_id)
			);
```
##### 非空约束
example04表名 	id/name/grade字段名 	INT/VARCHAR/FLOAT数据类型		PRIMARY/NOT NULL约束

```MySQL
CREATE TABLE example04(id INT PRIMARY KEY,
			name VARCHAR(20) NOT NULL,
			grade FLOAT);
```
##### 唯一约束
example05表名	id/stu_id/name字段名	INT/VARCHAR数据类型	PRIMARY KEY/UNIQUE/NOT NULL约束

```MySQL
CREATE TABLE example05(id INT PRIMARY KEY,
			stu_id INT UNIQUE,
			name VARCHAR(20) NOT NULL
			);
```
##### 默认约束
example06表名	id/stu_id/grade字段名	INT/FLOAT数据类型		PRIMARY KRY/UNIQUE/DEFALT约束	AUTO_INCREMENT特殊字段值自动增加

```MySQL
CREATE TABLE example06(id INT PRIMARY KEY AUTO_INCREMENT,
			stu_id INT UNIQUE,
			grade FLOAT DEFAULT 0
			);
```