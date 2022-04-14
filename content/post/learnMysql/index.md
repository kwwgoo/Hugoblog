---
title: "LearnMysql"
date: 2022-04-14T13:04:58+08:00
description: "学习mysql过程中的一些记录"
draft: false
slug:
image: 
categories:
    - tech
tags:
    - mysql
hidden: false
lastmod: 
toc:
---
## MySQL安装

[菜鸟教程](https://www.runoob.com/mysql/mysql-tutorial.html)

[下载地址](https://dev.mysql.com/downloads/installer/)

## MySQL简介

我们在前一章中介绍了数据库和SQL。正如所述，数据的所有存储、检索、管理和处理实际上是由数据库软件——DBMS（数据库管理系统）完成的。MySQL是一种DBMS，即它是一种数据库软件。

### 客户机—服务器软件

DBMS可分为两类：一类为基于共享文件系统的DBMS，另一类为基于客户机—服务器的DBMS。前者（包括诸如Microsoft Access和FileMaker)用于桌面用途，通常不用于高端或更关键的应用。

MySQL、Oracle以及Microsoft SQL Server等数据库是基于客户机—服务器的数据库。客户机—服务器应用分为两个不同的部分。服务器部分是负责所有数据访问和处理的一个软件。这个软件运行在称为数据库服务器的计算机上。

与数据文件打交道的只有服务器软件。关于数据、数据添加、删除和数据更新的所有请求都由服务器软件完成。这些请求或更改来自运行客户机软件的计算机。客户机是与用户打交道的软件。例如，如果你请求一个按字母顺序列出的产品表，则客户机软件通过网络提交该请求给服务器软件。服务器软件处理这个请求，根据需要过滤、丢弃和排序数据；然后把结果送回到你的客户机软件。

>服务器软件为MySQL DBMS。你可以在本地安装的副本上运行，
>也可以连接到运行在你具有访问权的远程服务器上的一个副本。
>
>客户机可以是MySQL提供的工具、脚本语言（如Perl）、Web应用
>开发语言（如ASP、ColdFusion、JSP和PHP）、程序设计语言（如
>C、C++、Java）等。

### MySQL工具(客户机)

+ mysql命令行实用程序

  使用`mysql -u root -p`输入密码后即可访问

  ![image-20210503153124481](https://cdn.jsdelivr.net/gh/kwwgoo/cdn/custom/image-20210503153124481.png)

+ MySQL Workbench

  [MySQL](http://c.biancheng.net/mysql/) Workbench 是一款专为 MySQL 设计的集成化桌面软件，也是下一代的可视化数据库设计、管理的工具，它同时有开源和商业化两个版本。该软件支持 Windows 和 Linux 系统，可以从 https://dev.mysql.com/downloads/workbench/ 下载。下载完成打开后图样。

  ![image-20210503153440718](https://cdn.jsdelivr.net/gh/kwwgoo/cdn/custom/image-20210503153440718.png)

## 使用MySQL

###  选择数据库

使用USE关键词.`USE test`

> test为自己建立的数据库名字

### 了解数据库和表

1. `SHOW DATABASES;`返回可用数据库的一个列表。包含在这个列表中的可能是MySQL内部使用的数据库（如例子中的mysql和(information_schema）。当然，你自己的数据库列表可能看上去与这里的不一样。

2. `SHOW TABLES;`获得一个数据库内的表的列表。

3. `SHOW COLUMNS FROM customers;`要求给出一个表名（ 这个例子中的FROM customers），它对每个字段返回一行，行中包含字段名、数据类型、是否允许NULL、键信息、默认值以及其他信息（如字段cust_id的auto_increment）。

   >DESCRIBE语句 MySQL支持用DESCRIBE作为SHOW COLUMNS
   >FROM的一种快捷方式。换句话说，DESCRIBE customers;是
   >SHOW COLUMNS FROM customers;的一种快捷方式。

## 检索数据

### 检索列

> 使用SELECT语句

`SELECT id,name FROM students`检索students表内的id和name列，或者使用`SELECT * FROM students`检索所有列。

```powershell
mysql> select * from students;
+----+----------+--------+--------+-------+
| id | class_id | name   | gender | score |
+----+----------+--------+--------+-------+
|  1 |        1 | 小明   | M      |    90 |
|  2 |        1 | 小红   | F      |    95 |
|  3 |        1 | 小军   | M      |    88 |
|  4 |        1 | 小米   | F      |    73 |
|  5 |        2 | 小白   | F      |    81 |
|  6 |        2 | 小兵   | M      |    55 |
|  7 |        2 | 小林   | M      |    85 |
|  8 |        3 | 小新   | F      |    91 |
|  9 |        3 | 小王   | M      |    89 |
| 10 |        3 | 小丽   | F      |    85 |
+----+----------+--------+--------+-------+
10 rows in set (0.00 sec)
```



### 检索不同的行

>解决办法是使用DISTINCT关键字，顾名思义，此关键字指示MySQL
>只返回不同的值。

```powershell
mysql> Select distinct class_id from students;
+----------+
| class_id |
+----------+
|        1 |
|        2 |
|        3 |
+----------+
3 rows in set (0.00 sec)
```



### 限制结果

`limit 0,1`意为从第0行开始取一行

`LIMIT 5, 5`指示MySQL返回从行5开始的5行。第一个数为开始位置，第二个数为要检索的行数。

![image-20210503160126803](https://cdn.jsdelivr.net/gh/kwwgoo/cdn/custom/image-20210503160126803.png)

## 排序检索数据

1. 按照成绩升序排列

   ```
   mysql> select name,score from students
       -> order by score;
   ```

   

2. 按照成绩降序排列

   ```powershell
   mysql> select name,score from students
       -> order by score desc;
   ```


## 过滤检索数据

| 操作符  |       说 明        |
| :-----: | :----------------: |
|    =    |        等于        |
|   <>    |       不等于       |
|   !=    |       不等于       |
|   <=    |      小于等于      |
| BETWEEN | 在指定的两个值之间 |

### 单WHERE语句

```powershell
mysql> select * from students
    -> where class_id=1;
+----+----------+--------+--------+-------+
| id | class_id | name   | gender | score |
+----+----------+--------+--------+-------+
|  1 |        1 | 小明   | M      |    90 |
|  2 |        1 | 小红   | F      |    95 |
|  3 |        1 | 小军   | M      |    88 |
|  4 |        1 | 小米   | F      |    73 |
+----+----------+--------+--------+-------+
4 rows in set (0.00 sec)
```

```powershell
mysql> select * from students
    -> where score between 90 AND 100
    -> order by score desc;
+----+----------+--------+--------+-------+
| id | class_id | name   | gender | score |
+----+----------+--------+--------+-------+
|  2 |        1 | 小红   | F      |    95 |
|  8 |        3 | 小新   | F      |    91 |
|  1 |        1 | 小明   | M      |    90 |
+----+----------+--------+--------+-------+
3 rows in set (0.00 sec)
```

### 组合WHERE语句

1. AND操作符

   ```powershell
   mysql> select * from students
       -> where score>=90 AND class_id=1
       -> ;
   +----+----------+--------+--------+-------+
   | id | class_id | name   | gender | score |
   +----+----------+--------+--------+-------+
   |  1 |        1 | 小明   | M      |    90 |
   |  2 |        1 | 小红   | F      |    95 |
   +----+----------+--------+--------+-------+
   2 rows in set (0.00 sec)
   ```

   >上述例子中使用了只包含一个关键字AND的语句，把两个过滤条件组
   >合在一起。还可以添加多个过滤条件，每添加一条就要使用一个AND。

2. OR操作符

   ```powershell
   mysql> select * from students
       -> where score>=90 AND class_id=1 OR class_id=2;
   +----+----------+--------+--------+-------+
   | id | class_id | name   | gender | score |
   +----+----------+--------+--------+-------+
   |  1 |        1 | 小明   | M      |    90 |
   |  2 |        1 | 小红   | F      |    95 |
   |  5 |        2 | 小白   | F      |    81 |
   |  6 |        2 | 小兵   | M      |    55 |
   |  7 |        2 | 小林   | M      |    85 |
   +----+----------+--------+--------+-------+
   5 rows in set (0.00 sec)
   
   mysql> select * from students
       -> where score>=90 AND (class_id=1 OR class_id=2)
       -> order by score desc;
   +----+----------+--------+--------+-------+
   | id | class_id | name   | gender | score |
   +----+----------+--------+--------+-------+
   |  2 |        1 | 小红   | F      |    95 |
   |  1 |        1 | 小明   | M      |    90 |
   +----+----------+--------+--------+-------+
   2 rows in set (0.00 sec)
   ```

   >SQL（像多数语言一样）在处理OR操作符前，优先处理AND操作符。
   >
   >在WHERE子句中使用圆括号 任何时候使用具有AND和OR操作符的WHERE子句，都应该使用圆括号明确地分组操作符。不要过分依赖默认计算次序，即使它确实是你想要的东西也是如此。使用圆括号没有什么坏处，它能消除歧义。

3. IN操作符

   ```powershell
   mysql> select * from students
       -> where class_id IN (1,2)
       -> order by score desc;
   +----+----------+--------+--------+-------+
   | id | class_id | name   | gender | score |
   +----+----------+--------+--------+-------+
   |  2 |        1 | 小红   | F      |    95 |
   |  1 |        1 | 小明   | M      |    90 |
   |  3 |        1 | 小军   | M      |    88 |
   |  7 |        2 | 小林   | M      |    85 |
   |  5 |        2 | 小白   | F      |    81 |
   |  4 |        1 | 小米   | F      |    73 |
   |  6 |        2 | 小兵   | M      |    55 |
   +----+----------+--------+--------+-------+
   7 rows in set (0.00 sec)
   ```

   > 圆括号内是匹配条件，和OR操作符相同

4. NOT操作符

   ```powershell
   mysql> select * from students
       -> where class_id NOT IN (1,2);
   +----+----------+--------+--------+-------+
   | id | class_id | name   | gender | score |
   +----+----------+--------+--------+-------+
   |  8 |        3 | 小新   | F      |    91 |
   |  9 |        3 | 小王   | M      |    89 |
   | 10 |        3 | 小丽   | F      |    85 |
   +----+----------+--------+--------+-------+
   3 rows in set (0.00 sec)
   ```

   >WHERE子句中的NOT操作符有且只有一个功能，那就是否定它之后所
   >跟的任何条件。MySQL中的NOT MySQL支持使用NOT 对IN 、BETWEEN 和
   >EXISTS子句取反，这与多数其他DBMS允许使用NOT对各种条件
   >取反有很大的差别。

## 用通配符进行过滤

1. LIKE操作符搭配通配符

2. %通配符任意字符多次(包括0次)

3. _通配符任意字符单次

## 用正则表达式进行搜索

>LIKE匹配整个列。如果被匹配的文本在列值中出现，LIKE将不会找到它，相应的行也不被返回（除非使用
>通配符）。而REGEXP在列值内进行匹配，如果被匹配的文本在列值中出现，REGEXP将会找到它，相应的行将被返回。这是一个非常重要的差别。那么，REGEXP能不能用来匹配整个列值（从而起与LIKE相同的作用）？答案是肯定的，使用^和$定位符（anchor）即可。

1. 匹配任意字符

   ```powershell
   mysql> select prod_name
       -> from products
       -> where prod_name regexp '.';
   +----------------+
   | prod_name      |
   +----------------+
   | .5 ton anvil   |
   | 1 ton anvil    |
   | 2 ton anvil    |
   | Detonator      |
   | Bird seed      |
   | Carrots        |
   | Fuses          |
   | JetPack 1000   |
   | JetPack 2000   |
   | Oil can        |
   | Safe           |
   | Sling          |
   | TNT (1 stick)  |
   | TNT (5 sticks) |
   +----------------+
   14 rows in set (0.00 sec)
   ```

   

2. 匹配产品名中有数字的行

```powershell
mysql> select prod_name
    -> from products
    -> where prod_name regexp '[0-9]';
+----------------+
| prod_name      |
+----------------+
| .5 ton anvil   |
| 1 ton anvil    |
| 2 ton anvil    |
| JetPack 1000   |
| JetPack 2000   |
| TNT (1 stick)  |
| TNT (5 sticks) |
+----------------+
7 rows in set (0.01 sec)

```

> 正如所见，`[]`是另一种形式的OR语句
>
> 字符集合也可以被否定，即，它们将匹配除指定字符外的任何东西。
> 为否定一个字符集，在集合的开始处放置一个^即可。因此，尽管`[123]`
> 匹配字符1、2或3，但`[^123]`却匹配除这些字符外的任何东西。

3. 匹配特殊字符

> 为了匹配特殊字符，必须用\\为前导。\\-表示查找-，\\.表示查找.。
>
> \或\\? 多数正则表达式实现使用单个反斜杠转义特殊字符，以便能使用这些字符本身。但MySQL要求两个反斜杠（MySQL自己解释一个，正则表达式库解释另一个）。

4. 匹配多个实例

   | 元 字 符 |            说 明             |
   | :------: | :--------------------------: |
   |    *     |        0个或多个匹配         |
   |    +     |  1个或多个匹配（等于{1,}）   |
   |    ?     |  0个或1个匹配（等于{0,1}）   |
   |   {n}    |        指定数目的匹配        |
   |   {n,}   |     不少于指定数目的匹配     |
   |  {n,m}   | 匹配数目的范围（m不超过255） |

   ```powershell
   mysql> select prod_name
       -> from products
       ->
       -> where prod_name regexp '\\([0-9] sticks?\\)';
   +----------------+
   | prod_name      |
   +----------------+
   | TNT (1 stick)  |
   | TNT (5 sticks) |
   +----------------+
   2 rows in set (0.00 sec)
   ```

>正则表达式\\([0-9] sticks?\\)需要解说一下。\\(匹配)，
>[0-9]匹配任意数字（这个例子中为1和5），sticks?匹配stick
>和sticks（s后的?使s可选，因为?匹配它前面的任何字符的0次或1次出
>现），\\)匹配)。没有?，匹配stick和sticks会非常困难。

```powershell
mysql> select prod_name
    -> from products
    -> where prod_name regexp '[[:digit:]]{4}';
+--------------+
| prod_name    |
+--------------+
| JetPack 1000 |
| JetPack 2000 |
+--------------+
2 rows in set (0.00 sec)
```

>如前所述，[:digit:]匹配任意数字，因而它为数字的一个集
>合。{4}确切地要求它前面的字符（任意数字）出现4次，所以
>[[:digit:]]{4}匹配连在一起的任意4位数字。

5. 定位符

   | 元 字 符 |   说 明    |
   | :------: | :--------: |
   |    ^     | 文本的开始 |
   |    $     | 文本的结尾 |
   | [[:<:]]  |  词的开始  |
   | [[:>:]]  |  词的结尾  |

   ```powershell
   mysql> select prod_name
       -> from products
       -> where prod_name regexp '^[0-9\\.]';
   +--------------+
   | prod_name    |
   +--------------+
   | .5 ton anvil |
   | 1 ton anvil  |
   | 2 ton anvil  |
   +--------------+
   3 rows in set (0.00 sec)
   ```

>`^`匹配串的开始。因此，^[0-9\\.]只在.或任意数字为串中第
>一个字符时才匹配它们。没有^，则还要多检索出4个别的行（那
>些中间有数字的行）。
>
>**^的双重用途 ^有两种用法。在集合中（用[和]定义），用它
>来否定该集合，否则，用来指串的开始处。**

>**使REGEXP起类似LIKE的作用 本章前面说过，LIKE和REGEXP
>的不同在于，LIKE匹配整个串而REGEXP匹配子串。利用定位
>符，通过用^开始每个表达式，用$结束每个表达式，可以使
>REGEXP的作用与LIKE一样。**

## 计算字段

Concat()拼接串，即把多个串连接起来形成一个较长的串。
Concat()需要一个或多个指定的串，各个串之间用逗号分隔。
上面的SELECT语句连接以下4个元素：

## 分组数据

** GROUP BY子句可以包含任意数目的列。这使得能对分组进行嵌套，
为数据分组提供更细致的控制。
 如果在GROUP BY子句中嵌套了分组，数据将在最后规定的分组上
进行汇总。换句话说，在建立分组时，指定的所有列都一起计算
（所以不能从个别的列取回数据）。
 GROUP BY子句中列出的每个列都必须是检索列或有效的表达式
（但不能是聚集函数）。如果在SELECT中使用表达式，则必须在
GROUP BY子句中指定相同的表达式。不能使用别名。
 除聚集计算语句外，SELECT语句中的每个列都必须在GROUP BY子
句中给出。
 如果分组列中具有NULL值，则NULL将作为一个分组返回。如果列
中有多行NULL值，它们将分为一组。
 GROUP BY子句必须出现在WHERE子句之后，ORDER BY子句之前。**

```
mysql> select * from students;
+----+----------+--------+--------+-------+
| id | class_id | name   | gender | score |
+----+----------+--------+--------+-------+
|  1 |        1 | 小明   | M      |    90 |
|  2 |        1 | 小红   | F      |    95 |
|  3 |        1 | 小军   | M      |    88 |
|  4 |        1 | 小米   | F      |    73 |
|  5 |        2 | 小白   | F      |    81 |
|  6 |        2 | 小兵   | M      |    55 |
|  7 |        2 | 小林   | M      |    85 |
|  8 |        3 | 小新   | F      |    91 |
|  9 |        3 | 小王   | M      |    89 |
| 10 |        3 | 小丽   | F      |    85 |
+----+----------+--------+--------+-------+
10 rows in set (0.01 sec)

mysql> select class_id,AVG(score) as avg_score
    -> form students
    -> group by class_id;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'form students
group by class_id' at line 2
mysql> select class_id,AVG(score) as avg_score
    -> from students
    -> group by class_id;
+----------+-----------+
| class_id | avg_score |
+----------+-----------+
|        1 |   86.5000 |
|        2 |   73.6667 |
|        3 |   88.3333 |
+----------+-----------+
3 rows in set (0.00 sec)

mysql> select gender,AVG(score) as avg_score
    -> from students
    -> group by gender;
+--------+-----------+
| gender | avg_score |
+--------+-----------+
| M      |   81.4000 |
| F      |   85.0000 |
+--------+-----------+
2 rows in set (0.00 sec)

mysql> select gender,MAX(score) as MAX_score
    -> from students
    -> group by gender;
+--------+-----------+
| gender | MAX_score |
+--------+-----------+
| M      |        90 |
| F      |        95 |
+--------+-----------+
2 rows in set (0.00 sec)

mysql> select class_id,MAX(score) as MAX_score
    -> from students
    -> group by class_id;
+----------+-----------+
| class_id | MAX_score |
+----------+-----------+
|        1 |        95 |
|        2 |        85 |
|        3 |        91 |
+----------+-----------+
3 rows in set (0.00 sec)
```

## 连接表

1. 使用`WHERE`进行连接

   ```powershell
   mysql> select vend_name,prod_name,prod_price
       -> from vendors,products
       -> where vendors.vend_id = products.vend_id
       -> order by vend_name,prod_price;
   +-------------+----------------+------------+
   | vend_name   | prod_name      | prod_price |
   +-------------+----------------+------------+
   | ACME        | Carrots        |       2.50 |
   | ACME        | TNT (1 stick)  |       2.50 |
   | ACME        | Sling          |       4.49 |
   | ACME        | Bird seed      |      10.00 |
   | ACME        | TNT (5 sticks) |      10.00 |
   | ACME        | Detonator      |      13.00 |
   | ACME        | Safe           |      50.00 |
   | Anvils R Us | .5 ton anvil   |       5.99 |
   | Anvils R Us | 1 ton anvil    |       9.99 |
   | Anvils R Us | 2 ton anvil    |      14.99 |
   | Jet Set     | JetPack 1000   |      35.00 |
   | Jet Set     | JetPack 2000   |      55.00 |
   | LT Supplies | Fuses          |       3.42 |
   | LT Supplies | Oil can        |       8.99 |
   +-------------+----------------+------------+
   14 rows in set (0.00 sec)
   ```

   目前为止所用的联结称为等值联结（equijoin），它基于两个表之间的相等测试。这种联结也称为内部联结

2. 内部联结

   ```
   mysql> select vend_name,prod_name,prod_price
       -> from vendors INNER JOIN products
       -> ON vendors.vend_id = products.vend_id;
   +-------------+----------------+------------+
   | vend_name   | prod_name      | prod_price |
   +-------------+----------------+------------+
   | Anvils R Us | .5 ton anvil   |       5.99 |
   | Anvils R Us | 1 ton anvil    |       9.99 |
   | Anvils R Us | 2 ton anvil    |      14.99 |
   | LT Supplies | Fuses          |       3.42 |
   | LT Supplies | Oil can        |       8.99 |
   | ACME        | Detonator      |      13.00 |
   | ACME        | Bird seed      |      10.00 |
   | ACME        | Carrots        |       2.50 |
   | ACME        | Safe           |      50.00 |
   | ACME        | Sling          |       4.49 |
   | ACME        | TNT (1 stick)  |       2.50 |
   | ACME        | TNT (5 sticks) |      10.00 |
   | Jet Set     | JetPack 1000   |      35.00 |
   | Jet Set     | JetPack 2000   |      55.00 |
   +-------------+----------------+------------+
   14 rows in set (0.00 sec)
   ```

   >此语句中的SELECT与前面的SELECT语句相同，但FROM子句不同。这里，两个表之间的关系是FROM子句的组成部分，以INNERJOIN指定。在使用这种语法时，联结条件用特定的ON子句而不是WHERE子句给出。传递给ON的实际条件与传递给WHERE的相同。

3. 连接多个表

   ```
   mysql> select prod_name,vend_name,prod_price,quantity
       -> from orderitems,vendors,products
       -> where products.vend_id = vendors.vend_id
       -> AND orderitems.prod_id = products.prod_id
       -> AND order_num = 20005;
   +----------------+-------------+------------+----------+
   | prod_name      | vend_name   | prod_price | quantity |
   +----------------+-------------+------------+----------+
   | .5 ton anvil   | Anvils R Us |       5.99 |       10 |
   | 1 ton anvil    | Anvils R Us |       9.99 |        3 |
   | TNT (5 sticks) | ACME        |      10.00 |        5 |
   | Bird seed      | ACME        |      10.00 |        1 |
   +----------------+-------------+------------+----------+
   4 rows in set (0.00 sec)
   ```

   >此例子显示编号为20005的订单中的物品。订单物品存储在orderitems表中。每个产品按其产品ID存储，它引用products表中的产品。这些产品通过供应商ID联结到vendors表中相应的供应商，
   >供应商ID存储在每个产品的记录中。这里的FROM子句列出了3个表，而WHERE子句定义了这两个联结条件，而第三个联结条件用来过滤出订单20005中的物品。
