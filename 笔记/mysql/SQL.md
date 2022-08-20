

## 数据库SQL

### 一、数据库简介

#### 1）.什么是数据库？

         数据库：Database,按照数据结构来组织、存储和管路数据的仓库，简单来说，就是存储数据的仓库。

         数据库管理系统：用来管理数据库的软件系统，常见的数据库有：MySQL、Oracle、SQLServer、DB2、Access等。

#### 2）.数据库必要性

**传统文件存储的缺点**：项目如果特别大的时候需要建立的文件特别多

数据规范化、统一化管理的响需要

#### 3）.什么是MySQL？

**MySQL**:是一个开源的关系型数据库管理系统，由瑞典MySQL AB公司开发，后来被Oracle收购，所以，目前属于Oracle公司

特点:免费、体积小、速度快，中小型网站多使用MySQL数据库

DBA : Data  Base Administrator数据库管理员

### 二、基本操作

#### 1.连接mysql'数据库系统

       要想操作MySQL数据库系统，必须先使用账户和密码连接MySQL服务器，登陆成功后才能使用。

       MySQL默认提供了一个超级管理员账号root，使用安装时设置的密码即可登录

```mysql
语法： mysql -u root -p
-u：用户名
-p：密码
-h:数据库服务器地址
```

登录后可以使用  **exit**  或者  **quit ** 退出MySQL

#### 2.关于MySQL服务器中的数据库和表

       **MySQL服务器：**安装了MySQL数据库系统（程序）的电脑，称为MySQL服务器或数据库管理系统，MySQL服务器可以管理都多个数据库

       **数据库:**存储数据的仓库，**实际场景中**，一般会为每个应用都创建一个数据库，用于存储该应用相关的所有数据，如员工管理系统数据库、学生考试系统数据库等

**表：**一般会在数据库中创建多个表，用于存储应用中每个实体的数据。

**行：**表中的每一条数据，也称**记录**。

**列：**行中的每一个字段。

**结论**：一台MySQL服务器包含多个数据库，一个数据库包含多张表，一张表包含多条记录，一条记录包含多个字段。

#### 3.查看数据库和表

**show databases；**      //查看当前所有数据库

**use  数据库名；**            //切换数据库

**show tables；**             //查看当前数据库中所有表  

**select  *  from 表名；**    // 查看表中所有的数据  

```
注意：

1）.所有的命令都是在英文状态下；

2）.执行命令时需要以分号结尾；

3）.以 - -开头的内容表示注释。可以忽略；

4）.Dos窗口，无法识别汉字，默认是gbk'，通过set names gbk告诉浏览器用的是gbk编号。

```

### 三、SQL简介

#### **1.简介**

         **Structured Query Language结构化查询语言，该语言普遍存在并且适用于数据库系统环境中。（ mysql数据库所采用的一种语言)**

         **用来对数据库进行查询、更新和管理的一种语言，所有关系型数据库都支持SQL。**

         **关系型数据库:    是指采用了关系模型来组织数据的数据库，其以行和列的形式存储数据，以便于用户理解，*关系型数据库*这一系列的行和列被称为表，一组表组成了数据库。Mysql Oracle，**

         **非关系型数据库:   面向文档、去sql语句;Mongodb。**



#### **2.SQL组成**

         包含三个部分：

- **DML**

  Data Manipulation Language **数据操作语言**

  用于新增、删除、修改、查询数据: insert、delete、update、select

- **DDL** 

  Data Definition Language  **数据定义语言**

  用于定义数据的结构:create、alter、[**drop**（删除表格）]

- **DCL**

  Data Control Language  **数据控制语言**

  用于设置用户的权限:grant、revoke

  

#### **3.导入初始数据**

使用root用户连接MYSQL，然后执行如下命令：

```javascript
#source  路径
例：source  D：/init.sql  //也可直接拖动文件到里面
```

**注意：**以 **.sql ** 结尾的文件是数据库脚本文件，包含一系列的sql语句

### 四、查询操作

```javascript
desc 表名；  //查看表结构
select  *  from  表名； //查看表中所有数据
```

#### 1.简单查询

**语法：**

```javascript
验证SQL安装是否成功，获取SQL版本：mysql -V

1、进入SQL程序：mysql -uroot -p

2、输入数据库密码：******

3、获取所有数据库：show databases;

4、切换选择数据库：use 数据库名;

5、查看当前库中所有表：show tables;

6、查看表中所有的数据：select * from 表名;

7、查看单个表的数据：select 列名 别名，列名 别名... from 表名; //别名可以是中文注意兼容性   Dos窗口，无法识别汉字，默认是gbk'，通过set names gbk告诉浏览器用的是gbk编号。

8、退出数据库：quit / exit

//查询表中所有信息的时候建议用全写如：
select lempno,ename,job,mgr,hiredate,sal,comm,deptno from  emp;

```

ifnull（a，b）将表格中a列的值为空时替换为b

语法：

select   ename   姓名,(sal + ifnull (comm, 0))*12  年薪  from  emp;

#### 2.限定查询

语法：

```mysql
select * | 列名1 别名1，列名2 别名2 from 表名 where 条件；
```

##### 2.1.比较运算符

、>、<、>=、<=、=、!=

##### 2.2  null和not null

```mysql
例： select * from emp where comm is null;//null大写小写都可以
     select * from emp where comm is not null;
```

##### 2.3  and //并且

```mysql
分析需要查询的字段：
例：不大于3000，奖金不为空
select * from emp where sal<3000 and comm is not null;
```

##### 2.4  or//或者

```mysql
例： 查询从事销售工作，或者工资大于2000的雇员信息
select * from emp where job='salesman' or sal>='2000';
```

##### 2.5  not

```mysql
例：从事销售工作，工资不小于1500的雇员信息
select * from emp where not job = 'salesman' and not sal<1500;
```

##### 2.6  between ...  and ...

1）.包含临界值；

2）.between a  and b 意思是查询的值在a和b之间

```mysql
例：查询基本工资大于1500，但小于30000的雇员信息
select * from emp where sal>1500 and sal<3000;//第一种写法
select * from emp where sal between 1500 and 3000;//第二种写法

例:查询1981年入职的雇员编号、姓名、入职时间、所在部门编号
select empno,ename,hiredate,deptno from emp where hiredate between '1981-1-1' and '1981-12-31';
```

##### 2.7  in和not in

```mysql
in表示在某范围内，not in 不在其内
语法：in（a,b,c）

例：查询编号7788、7499、7369的雇员信息
select * from emp where empno in (7788,7499,7369);


例:查询姓名为SMITH、ALLEN、KING的雇员编号、姓名、入职时间
select  ename, empno,hiredate from emp where ename in('smith','allen','king');
```

##### 2.8  like

```mysql
用法：like 'S%';
用来进行模糊查询，需要结合通配符一起使用
常用通配符：
%  可以匹配任意长度字符
_  可以匹配单个字符
例：查询雇员姓名以S开头的雇员信息
select * from emp where ename like'S%';

例:查询姓名以D结尾，长度为4个字符的雇员信息
select * from emp where ename like'___d';
```

#### 3.排序

##### 3.1语法

```mysql
select*|列名1 别名1,列名2 别名2...from表名  where 条件 order by排序列名1 asc|desc,排序列名2 asc|desc;
asc表示升序，desc表示降序，如果省略不写，则默认为升序
```

##### 3.2示例

```mysql
例:查询所有雇员信息，按工资由低到高排序
select * from emp order by sal asc;

查询员工编号、姓名、工作、入职时间，按员工编号升序排序
select empno 员工编号,ename 姓名,job 工作,hiredate 入职时间 from emp order by empno asc;


例:查询雇员编号、姓名、年薪，按年薪由高到低排序
select empno,ename,(sal+ifnull( comm,0))*12 income from emp order by(sal+ifnull(comm,0)) *12 desc;

select empno,ename,(sal+ifnull(comm,0))*12 income from emp order by income desc; --功能一致

select empno,ename,(sal+ifnull(comm,0))*12 年薪 from emp order by 年薪 desc;--功能一致
```

## MySQL进阶

### 一、增删改查操作

#### 1.    insert增加数据

```mysql
语法：--插入一条数据
insert into 表名（列名1，列名2...）values(值1，值2...)

语法：--插入多条数据
insert into 表名 （列名1，列名2...）values(值1，值2...),(值1，值2...),(值1，值2...)

语法：简写
insert into 表名 values(值1，值2...)
```

```mysql
例:插入一个部门，部门编号为50，名称为开发部
insert into dept(deptno,dname,loc) values(50,'开发部','合肥');
```

注: Windows的DOS窗口默认使用的字符集是GBK，可能会出现中文乱码，可以执行set names gbk;使中文正常显示

#### 2.    delete

```mysql
语法：
delete from 表名  where 条件
例：删除市场部
delete from dept where dname='市场部';

删除多个：
delete from emp where ename='' and ename='';
delete from emp where ename in('','');

例:删除研发部（research）工资高于2500的雇员
delete from emp where sal>2500 and deptno = (select deptno from dept where dname='research');子查询方法
```

#### 3.    update

```mysql
语法：
update 表名 set 列名1=值1,列名2=值2... where 条件
例：将秋香的工资改为6000，奖金改为1000，职位改为总裁
update emp set sal=6000,comm=1000,job='总裁' where ename='秋香'
```

### 二、表和库的管理

#### 1、创建数据库

```mysql
语法：
create datebase 数据库名 charset utf8;
或
create database if not exists 数据库名 charset utf8;

例：创建名为shop的数据库
create database shop charset utf8;
```

#### 2、删除库

```mysql
语法：
drop database 数据库名；
drop database if exists 数据库名；

例：删除shop
drop database shop;
```

#### 3、创建表

dasc emp 查看表的结构不难发现，表是由一条条记录组成，也是由不同的字段名“堆成”而成！

##### 1）数据类型

整数：int

小数：float 、 double 

char 定长字符串，如char(10),最多存储10个字符串，如果不足10个字符，仍然占10个字符的空间

varchar 变长字符串，如varchar(10),最多存储10个字符，如果不足10个字符，则占实际字符个数的空间

text 存储文本

date  年月日

##### 2）语法：

```mysql
create table 表名
（
列名 数据类型，
列名 数据类型，
列名 数据类型，
）charset=utf8;

例：创建一个学生表，包含编号、姓名、年龄、性别、身高、出生日期
create table student
(
id int,
name varchar(10),
age int,
sex cahr(6),
height double,
birthday date,
)charset=utf8;
插入数据：
insert into student values(1001,'tom',18,'male',180,'1998-7-16');
insert into student values(1,'李白',25,'男',180,'1998-7-16'),(2,'李清照',25,'女',170,'2001-7-16');
```

#### 4.删除表

```mysql
语法：
drop table 表名；
drop table if exists 表名；

例：删除student表
drop table student ;
drop table if exists student;
```

### 三、约束

#### 1、简介

constraint ,约束是对表中数据的一种限制，保证数据的完整性和有效性

#### 2、约束分类

有五种分类：

主键约束 primary key :是唯一标识，表示一条记录（数据），本身不能为空；

唯一约束 unique:不允许出现重复值；

检查约束 check：判断数据是否符合指定条件；

注意：MySQL会对check约束进行分析，但会忽略check约束，不会强制执行约束

非空约束 not null：不允许为null ，但可以为空字符串；

外键约束 foreign key ：比如 foreign key （从表字段）references 主表名（主表字段）；

约束两表之间的关联关系，表示子（从）表的列与父表的列有所关系；

#### 3、添加约束

班级表class：

c_id 班级编号；

c_name 班级名称；

c_desc 班级描述；

##### 1）、创建数据库kgc

```mysql 
# create database kgc;
#创建班级表
create table class(
c_id int primary key,
c_name varchar(20) not null unique,
c_desc varchar(200)
);
insert into class(c_id,c_name,c_desc) values(1,'前端1班','Web前端开发1班');
insert into class(c_id,c_name,c_desc) values(2,'前端2班','Web前端开发2班');
```

##### 2)、创建学生表student

 id 学号

name 姓名.

IDCard身份证

class_id 所在班级编号

```mysql
#创建表
create table student(
 id int primary key auto_increment，//auto_increment表示自增长：凡是设置了自增长，可以省略具体的数值,但是字段不可省略;
 name varchar(50) not null,
 IDcard varchar(18) unique,
 foreign key (class_id) references class(c_id)
 ）;/ 从表外键指向主表
    --插入行、记录：
    insert into student (name,IDCard,class_id) values('tom','34222222222222222',101)
    
create table student(id int unique primary key not null auto_increment,name varchar(20) not null, IDCard varchar(25) not null,class_id int not null,foreign key (class_id) references class(c_id);
```

```javascript
 //导入模块
 const express = require('express')
 const mysql = require('mysql')

 // 通过express模块创建服务器；
 const app = express();


 // 通过createConnection方法，绑定数据信息，
 const conn = mysql.createConnection({
     host: "127.0.0.1",
     user: 'root',
     password: 'yanghu199869',
     database: 'yanghu' //"数据库"必须是存在的。这个是数据库名称不是表名称
 })

 //   连接数据库
 conn.connect((err, res) => {
     if (err) { throw error; } else {
         console.log('连接成功', res);
     }
 })

 //定义数据库语法
 const create_sql = 'create table if not exists person (id int not null primary key auto_increment,name varchar(30))';
 const insert_sql = `insert into person(name) value(?)`


 conn.query(create_sql, (err) => {
     if (err) throw error;
     // 插入表数据
     conn.query(insert_sql, '唐伯虎', (err, result) => {
         if (err) throw err;
         conn.query(insert_sql, '秋香', (err, result) => {
             if (err) throw err;
         })
     })
 })
```

