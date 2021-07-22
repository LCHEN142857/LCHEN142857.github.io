# Basic SQL

- 新增一个字段列  

```sql
ALTER TABLE `keyword` ADD `KW_NEW` VARCHAR(20) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '关键字NEWCOLUMN';
```

- 修改字段的属性  

```sql
ALTER TABLE `keyword` ALTER COLUMN `KW_FF` SET DEFAULT '1';
```

- 修改自增主键的起始值  

```sql
ALTER TABLE `user` AUTO_INCREMENT = 10000;
```

- 修改字段列类型  

```sql
ALTER TABLE `keyword` MODIFY COLUMN `KW_NAME` int;  -- 从varchar改为int，前提是记录中的值都是整数不然会报错
```

- drop column  

```sql
ALTER TABLE `keyword` DROP COLUMN `KW_NEW`;
```

- create database  

```sql
CREATE DATABASE IF NOT EXISTS `study_sql` DEFAULT CHARACTER SET utf8mb4;
```

- create table  

```sql
-- COLLATE utf8mb4_bin :以字符串的二进制形式来比较校对规则 
CREATE TABLE IF NOT EXISTS `keyword`(
  `KW_NAME` VARCHAR(20) COLLATE utf8mb4_bin NOT NULL COMMENT '关键字名',
  `KW_USAGE` VARCHAR(100) COLLATE utf8mb4_bin NOT NULL COMMENT '关键字用法',
  `KW_EXAMPLE` VARCHAR(200) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '关键字实例',
  `KW_REMARK` VARCHAR(50) COLLATE utf8mb4_bin NOT NULL COMMENT '关键字备注',
  PRIMARY KEY (`KW_NAME`)
)DEFAULT CHARSET = utf8mb4 COLLATE = utf8mb4_bin COMMENT '关键字表'
```

- delete raw  

```sql
DELETE FROM `keyword` -delete all raws
```

- drop database  

```sql
DROP DATABASE IF EXISTS `study_sql`; -- 使用if exists 就可以避免 Unknown table，Unknown database的报错
```

- drop table  

```sql
DROP TABLE IF EXISTS `keyword`; -- 使用if exists 就可以避免 Unknown table，Unknown database的报错
```

- insert raw  

```sql
INSERT INTO `keyword` (`KW_NAME`,`KW_USAGE`,`KW_EXAMPLE`,`KW_REMARK`) VALUES ('vvvss','seese','dabae','oooee');
```

- select raws  

```sql
SELECT * FROM `keyword` ;
```

- show sql of create table  

```sql
SHOW CREATE TABLE `keyword`;
```

- show tables in the database  

```sql
SHOW TABLES;
```

- update data  

```sql
UPDATE `keyword` SET `KW_REMARK` = 'dddddd'  - update all raws
```

- use database  

```sql
USE `study_sql`;
```

- 创建无参存储过程  

```sql
DELIMITER $       -- 声明存储过程的结束符 
DROP PROCEDURE if EXISTS pro_emp;
CREATE PROCEDURE pro_emp()           -- 存储过程名称(参数列表)
BEGIN             -- 开始
-- 可以写多个sql语句          -- sql语句+流程控制
SELECT * FROM `user`;
END $            -- 结束 结束符
```

- 创建有参存储过程  

```sql
  -- IN：  表示输入参数，可以携带数据到存储过程中
  -- OUT： 表示输出参数，可以从存储过程中返回结果
  -- INOUT： 表示输入输出参数，既可以输入功能，也可以输出功能
  -- 参数列表：（输入/输出 参数名 参数类型,...）       参数名可以与表中的列名不同,但是存储过程的参数名最好不要和列名相同，例如sid = sid作为条件的时候会查出来多行，即没有用入参就执行了查询

DELIMITER $
CREATE PROCEDURE pro_test1(IN did INT)
BEGIN
 SELECT * FROM `user` WHERE uid = did;
END $

DELIMITER $
CREATE PROCEDURE pro_test2(OUT dname VARCHAR(20))
BEGIN
 SET dname = 'hello';
END $

DELIMITER $
CREATE PROCEDURE pro_test3(INOUT cid INT)
BEGIN
 SET cid = cid+1;
END $
```

- 调用存储过程  

```sql
CALL pro_emp();  -- 无参的存储过程可以省略括号直接写存储过程名

CALL pro_test1(1); -- 传入输入条件

CALL pro_test2(@n); -- 用@加参数名（可自定义）接收输出参数
SELECT @n;   -- 查询@n参数的值，默认列名为@n，可以自己取别名，如 SELECT @n AS `name`;

SET @num = 1001;  -- 设置一个入参@num
CALL pro_test3(@num); -- @num 即作为入参也作为出参
SELECT @num AS uid;
```

- 删除存储过程  

```sql
DROP PROCEDURE IF EXISTS pro_test;
```

- 查看所有存储过程  

```sql
SHOW PROCEDURE STATUS;
```

- 带有条件判断的存储过程  

```sql
DELIMITER $
CREATE PROCEDURE pro_testIf(IN num INT,OUT str VARCHAR(20))
BEGIN
 IF num=1 THEN
  SET str='星期一';
 ELSEIF num=2 THEN
  SET str='星期二';
 ELSEIF num=3 THEN
  SET str='星期三';
 ELSE
  SET str='输入错误';
 END IF;
END $

CALL pro_testIf(4,@str);
SELECT @str;
```

- 带有循环功能的存储过程  

```sql
DELIMITER $
CREATE PROCEDURE pro_testWhile(IN num INT,OUT result INT)
BEGIN
  -- 定义一个局部变量
 DECLARE i INT DEFAULT 1;
 DECLARE vsum INT DEFAULT 0;
 WHILE i<=num DO
  SET vsum = vsum+i;
  SET i=i+1;
 END WHILE;
 SET result=vsum;
END $

DROP PROCEDURE pro_testWhile;
CALL pro_testWhile(100,@result);
SELECT @result;
```

- 使用查询的结果赋值给变量（INTO）  

```sql
DELIMITER $
CREATE PROCEDURE pro_findById2(IN eid INT,OUT vname VARCHAR(20) )
BEGIN
 SELECT empName INTO vname FROM employee WHERE id=eid;
END $

CALL pro_findById2(1,@NAME);
SELECT @NAME;
```
