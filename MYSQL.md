每一个sqlyog的执行操作，本质还是sql命令

```mysql
mysql -uroot -p123456 -- 连接数据库
update mysql.user set authentication
flush privilegdes; -- 刷新权限
--------------------------------
-- 所有语句使用分号结尾
show database; -- 查看所有数据库

mysql> use school -- 切换数据库
Database changed

show tables; -- 查看数据库中所有的表
describe student; -- 显示数据中所有的表的信息

create database /name/; -- 创建一个数据库

exit; -- 退出连接
/*多行注释*/

```

**数据库? ?语言**

- DDL define 定义

- DML manipulation 操作

- DQL query 查询

- DCL control 控制




mysql关键词不区分大小写

```mysql
create database /name/ -- 创建数据库
drop database /name/ -- 删除数据库
use /name/ -- 使用数据库
show databases -- 查看所有的数据库
```

**数值**

- tinyint 十分小的数据 1个字节
- smallint 较小的数据 2个字节
- int 标准整数 4个字节
- bigint 较大数据 8个字节
- float 浮点数 4个字节
- double 浮点数 8个字节
- decimal 字符串形式的浮点数

**字符串**

- char 0-255
- varchar 可变字符串   0-65535  常用的string
- tinytxt 微型文本   2^8-1
- text 文本串   2^16-1  保存大文本

**时间日期**

- date YYYY-MM-DD  日期格式
- time HH：MM：SS 时间格式
- timestamp 时间戳 
- year 年份表示

**null**

- 没有值，未知
- 不要对null进行运算

**unsigned**

- 无符号整数
- 说明了该列不能声明为负数

**zerofill**

- 0填充的
- 不足的位数，使用0来填充

**自增**

- 通常理解为自增，自动在上一条记录的基础上默认加一
- 通常用来设计唯一的主键 ~index，必需是整数类型
- 可以自定义步长

**非空 not null**

- 不能为空

 **默认**

- sex 默认值为男



每一个表都必须存在以下五个字段

```mysql
/*
id 主键

'version' 乐观锁

is_delete 伪删除

gmt_create 创建时间

gmt_update 修改时间
*/
```



```mysql
CREATE TABLE IF NOT EXISTS `people`(
	`id` INT (4) NOT NULL AUTO_INCREMENT COMMENT '学号',
	`name` VARCHAR(30) NOT NULL DEFAULT '林克' COMMENT '姓名',
	`password` VARCHAR(20) NOT NULL DEFAULT '123456' COMMENT '密码',
	`sex` VARCHAR(2) NOT NULL DEFAULT '女' COMMENT '性别',
	`birthday` DATETIME DEFAULT NULL COMMENT '出生日期',
	`address` VARCHAR(100) DEFAULT NULL COMMENT '家庭住址',
	`email` VARCHAR(50) DEFAULT NULL COMMENT '邮箱',
	PRIMARY KEY(`id`)
	
)ENGINE=INNODB DEFAULT CHARSET=utf8
-- 使用英文()，表的名称和字段用''(单引号)括起来
-- auto_increment 表示自增
-- 字符串使用单引号
-- 所有的语句后面加逗号，最后一句不需要加逗号
-- 主键一张表一般只有唯一的

primary key (`/etc/`)
-- 对表设置主键
```

```mysql
-- 常用命令
SHOW CREATE DATABASE school -- 查看创建数据库的语句
SHOW CREATE TABLE people -- 查看创建表的语句
DESC people -- 显示表的结构
```

|              | MYISAM | INNODB |
| ------------ | ------ | ------ |
| 事务支持     | 不支持 | 支持   |
| 数据行锁定   | 不支持 | 支持   |
| 外键约束     | 不支持 | 支持   |
| 全文索引     | 支持   | 不支持 |
| 表空间的大小 | 较小   | 较大   |

常规使用操作

- MYISAM 	节约空间，速度较快
- INNODB     安全性高，事务的处理，多表多用户操作

设置数据库的字符编码

```mysql
CHARSET=utf8
```

**对表的修改与删除操作**

```mysql
-- 修改表名 ALTER TABLE 旧表名 RENAME AS 新表名
ALTER TABLE people RENAME AS people1
-- 增加表的字段 ALTER TABLE 表名 ADD 字段名 列属性
ALTER TABLE people1 ADD age INT(11)

-- 修改表的字段（重命名，修改约束）
-- ALTER TABLE 表名 MODIFY 字段名 列属性
ALTER TABLE people1 MODIFY age VARCHAR(11) -- 修改约束
-- ALTER TABLE 表名 CHANGE 旧名 新名 列属性
ALTER TABLE people1 CHANGE age age1 INT(1) -- 字段重命名

-- 删除表的字段
ALTER TABLE people1 DROP age1 

-- 删除表
DROP TABLE IF EXISTS people1
```

注意点：

- ``字段名
- 注释 --   /**/
- sql关键词大小写不敏感，建议大家写小写
- 使用英文符号



## MySQL数据管理

### 外键

**方法一：在创建表的时候，增加约束**

```mysql
create table `grade`(
	`gid` int(10) not null auto_increment comment '年级id',
	`gname` varchar(50) not null comment '年级名称',
	primary key (`gid`)
)engine=innodb default charset=utf8

CREATE TABLE IF NOT EXISTS `student`(
	`id` INT (4) NOT NULL AUTO_INCREMENT COMMENT '学号',
	`name` VARCHAR(30) NOT NULL DEFAULT '林克' COMMENT '姓名',
	`password` VARCHAR(20) NOT NULL DEFAULT '123456' COMMENT '密码',
	`sex` VARCHAR(2) NOT NULL DEFAULT '女' COMMENT '性别',
	`birthday` DATETIME DEFAULT NULL COMMENT '出生日期',
	`gid` INT(10) NOT NULL COMMENT '年级',
	`address` VARCHAR(100) DEFAULT NULL COMMENT '家庭住址',
	`email` VARCHAR(50) DEFAULT NULL COMMENT '邮箱',
	PRIMARY KEY(`id`),
	KEY `fk_gid` (`gid`),
	CONSTRAINT `fk_gid` FOREIGN KEY (`gid`) REFERENCES `grade`(`gid`)
	
)ENGINE=INNODB DEFAULT CHARSET=utf8
-- 学生表的gid字段去引用年级表的gid
-- 定义外键key
-- 给这个外键添加约束（执行引用）
```

删除有外键关系的表的时候，需要先删除引用别人的表（从表），再删除被引用的表（主表）

**方法二：创建表成功后，添加外键约束**

```mysql
ALTER TABLE `student`
ADD CONSTRAINT `fk_gid` FOREIGN KEY(`gid`) REFERENCES `grade`（`gid`);
```

以上的操作都是物理外键，数据库级别的外键

## DML语言

- insert
- update
- delete

### 添加

```mysql
-- 插入语句
-- insert into 表名([字段名1,字段2,字段3,..])values('1','2','3',..)
INSERT INTO `grade`(`gname`)VALUES('大四')

-- 由于主键自增我们可以省略（如果不写表的字段，就会一一匹配）
INSERT INTO `grade`VALUES('大三')

-- 一般写插入语句，我们一定要数据和字段一一对应

-- 插入多个字段
INSERT INTO `grade`(`gname`)VALUES('大二'),('大一')
INSERT INTO `student`(`id`)VALUES('123')
INSERT INTO `student`(`name`,`password`,`sex`)VALUES('塞尔达','321','女')
```

注意事项：

1. 字段和字段之间使用英文逗号
2. 字段可以省略，但后面的值必须对应
3. 可以同时插入多条数据 VALUES(''),(''),('')

### 修改

```mysql
-- 修改学员名字
UPDATE `student` SET `name`='塞尔达' WHERE id = 1

-- 不指定条件的情况下，会改动表内所有行
UPDATE `student` SET `name`='希克'

-- 语法：
-- UPDATE 表名 set colnum_name = value where [条件]

-- 修改多个属性，可用逗号隔开
UPDATE `student` SET `name`='塞尔达',`email`='630853319@qq.com' WHERE id=1

-- BEWTWEEN语句
UPDATE `grade` SET `gname`='rex'WHERE gid BETWEEN 1 AND 3

-- 通过多个条件定位数据
UPDATE `grade` SET `gname`='homura' WHERE `gname`='rex' AND `gid`=1
```

条件：where  子句  运算符   id等于某个值，大于某个值，在某个区间中

| 操作符             | 含义        | 范围        | 结果  |
| ------------------ | ----------- | ----------- | ----- |
| =                  | 等于        | 5=6         | false |
| <> 或  !=          | 不等于      | 5<>6        | true  |
| >                  |             |             |       |
| <                  |             |             |       |
| >=                 |             |             |       |
| <=                 |             |             |       |
| BETWEEN  .. and .. | 在[x,y]区间 | [x,y]       |       |
| AND                | &&          | 5>1 AND 1>2 | false |
| OR                 | \|\|        | 5>1 OR 1>2  | true  |

注意：

- colnum_name 是数据库的列，需要带上``

- 如果没有填上筛选的条件，则会修改所有的列

- value可以是一个具体值，也可以是变量

  ```mysql
  UPDATE `student` set `birthday`=CURRENT_TIME WHERE `name`='Zelda' AND `sid`=1
  ```

### 删除

```mysql
-- 删除数据（全部删除）
DELETE FROM `grade`

-- 删除数据
DELETE FROM `grade` WHERE gid = 1;

-- 会清空表，但表的结构和索引约束不会变
TRUNCATE `grade`
```

**delete和truncate的区别：**

- 相同点：都能删除表的数据

- 不同点：

  - TRUNCATE 重新设置自增列，计数器归零

  - Delete 会继续原来的设置

    ```mysql
    CREATE TABLE `test`(
    	`id` INT(4) NOT NULL AUTO_INCREMENT,
    	`coll` VARCHAR(20) NOT NULL,
    	PRIMARY KEY (`id`)
    
    )ENGINE=INNODB DEFAULT CHARSET=utf8
    
    INSERT INTO `test` (`coll`) VALUES('1'),('2'),('3')
    
    DELETE FROM `test` -- 不会影响自增
    
    TRUNCATE TABLE `test` -- 自增归零
    ```

    

