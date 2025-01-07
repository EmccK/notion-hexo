---
updated: '2025-01-07T13:45:00.000Z'
date: '2024-10-31T15:51:00.000Z'
categories: 基础
urlname: mysql-study-progress
tags:
  - 数据库
title: MySql学习
cover: 'https://cn.bing.com/th?id=OHR.MontBlancMassif_EN-US3284638409_UHD.jpg&rf=LaDigue_UHD.jpg&pid=hp&w=3840&h=2160&rs=1&c=4'
---

## 常用命令合集

<details>
<summary>连接数据库</summary>

```sql
-- mysql -u 用户名 -p密码 数据库[可选] -P 端口 -h IP
mysql -u root -p -P 3307 -h 127.0.0.1
```


</details>


### 数据库

<details>
<summary>显示所有数据库</summary>

```sql
-- SHOW DATABASES;
show databases;
```


</details>

<details>
<summary>使用数据库</summary>

```sql
-- USE 数据库名;
use practice;
```


</details>

<details>
<summary>查看创建数据库的命令（如何创建的）</summary>

```sql
-- SHOW CREATE DATABASE 数据库名;
show create database practice;
```


</details>

<details>
<summary>查看当前使用的数据库</summary>

```sql
-- SELECT DATABASE();
select database();
```


</details>


### 数据表

<details>
<summary>查看当前数据库下的所有表</summary>

```sql
-- SHOW TABLES;
show tables;
```


</details>

<details>
<summary>查看某个表下的所有列</summary>

```sql
-- DESCRIBE 表名;
-- 或者
-- SHOW COLUMNS FROM customers;

show create table customers;
-- 或者
desc table customers;
```


</details>

<details>
<summary>创建一个表</summary>

```sql
/*
CREATE TABLE 表名 (
    列名1 数据类型 约束,
    列名2 数据类型 约束,
    ...
);
*/

create table users(
id int auto_increment primary key,
username varchar(50) not null,
email varchar(50) not null,
create_at timestamp default current_timestamp
);
```


</details>

<details>
<summary>查看创建某个表的命令（如何创建的）</summary>

```sql
-- SHOW CREATE TABLE 表名;
show create table customers;
```


</details>

<details>
<summary>删除某个表</summary>

```sql
-- DROP TABLE 表名;
drop table users;
```


</details>


### 数据操作

<details>
<summary>新增数据</summary>

```sql
-- INSERT INTO 表名 (列1, 列2, ...) VALUES (值1, 值2, ...);
insert into users (username, email) values ('EmccK', 'demo@gmail.com');
```


</details>

<details>
<summary>删除数据</summary>

```sql
-- DELETE FROM 表名 [WHERE 条件]
-- 不加条件则是删除所有
delete from users where id = 2
```


</details>

<details>
<summary>修改数据</summary>

```sql
-- UPDATE 表名 SET 列1 = 新值1, 列2 = 新值2 WHERE 条件;
update users set username = 'John' where id = 6;
```


</details>

<details>
<summary>查询数据</summary>

```sql
-- SELECT 列1, 列2, ... FROM 表名 [WHERE 条件] [ORDER BY 列 ASC|DESC] [LIMIT 数量];
-- 所有列表：SELECT *
-- 排序：ORDER BY，ASC升序（默认从小到大），DESC降序
-- 限制数量：LIMIT 
select username, email from users order by email asc limit 1;
```


</details>


### 条件查询数据

<details>
<summary>查询所有数据</summary>

```sql
-- SELECT * FROM 数据表;
select * from products;
```


</details>

<details>
<summary>查找之后去重</summary>

```sql
-- DISTINCT关键字
select distinct vend_id from products;

-- 同时两列不同
select distinct vend_id, prod_price from products;
```


</details>

<details>
<summary>查找限制几行</summary>

```sql
-- LIMIT 数量，限制只有固定数量行
select * from products limit 5;

-- LIMIT 起点索引（包含）, **数量**
select * from products limit 5, 10;
```


</details>

<details>
<summary>排序数据</summary>

```sql
-- ORDER BY [列1] ASC(升序，默认值，可以不写)/DESC(降序), [列表2] ASC(升序，默认值，可以不写)/DESC(降序)
select * from products order by prod_price;

select * from products order by prod_price desc;

select * from products order by prod_price asc, prod_name desc;

-- 在大多数数据库中，A和a是相同的
```


</details>

<details>
<summary>过滤数据</summary>

```sql
-- WHERE关键字
/* 
= 等于 
<> 不等于 
!= 不等于 
< 小于 
<= 小于等于 
> 大于 
>= 大于等于 
BETWEEN AND 在指定的两个值之间，前后都包括 
*/
```


</details>

<details>
<summary>查询某一列是NULL</summary>

```sql
-- WHERE 列表 IS NULL
select * from users where email is null;
```


</details>

<details>
<summary>组合查找</summary>

```sql
-- 使用 AND 和 OR 可以组合处理多个条件
select prod_id, prod_price, prod_name from products where vend_id = 1003 and prod_price <= 10 order by prod_price;

select * from products where vend_id = 1002 or vend_id = 1003;

-- AND和OR放一起的时候，会优先处理AND语句，再处理OR语句
-- 如果是：列出价格为10美元（含）以上且由1002或1003制造的所有产品，则下面的就是错误的
select * from products where vend_id = 1002 or vend_id = 1003 and prod_price >= 10;

-- 正确的是需要添加括号
select * from products where (vend_id = 1002 or vend_id = 1003) and prod_price >= 10 order by prod_price;

-- IN (1002, 1003) 等价于 vend_id = 1002 OR vend_id = 1003,
-- IN里面是一个列表，IN比OR更快，更容易管理
select * from products where vend_id in (1002, 1003) order by prod_price;
```


</details>

<details>
<summary>否定查找</summary>

```sql
-- NOT WHERE子句中用来否定后跟条件的关键字
select * from products where vend_id not in (1002, 1003) order by vend_id;
```


</details>


### 字符串查找，通配符&正则

<details>
<summary>查找`prod_name`以`jet`开头的产品-匹配多字符</summary>

```sql
-- 可以使用 LIKE 关键字，后面跟通配符，不区分大小写
-- 可以使用%查询，%表示任何字符出现任意次数**(0,1,以及任意)**
SELECT * FROM products WHERE prod_name LIKE 'jet%';

-- %可以同时位于两端
SELECT * FROM products WHERE prod_name LIKE '%anvil%';
```


</details>

<details>
<summary>通配符查找，匹配单字符</summary>

```sql
-- 可以使用 _ 匹配单字符，使用起来跟%差不多
SELECT * FROM products WHERE prod_name LIKE '_ ton anvil';
```


</details>


最好和其他条件配合查找，因为通配符的查找会比较慢一点

<details>
<summary>正则表达式查找</summary>

```sql
-- 使用关键字<u>**REGEXP**</u>，代替LIKE，使用起来是一样的，后面跟正则表达式，这个也是不区分大小写。
-- 正则表达式中的<u>**.**</u>可以匹配任意<u>**一个**</u>字符
SELECT * FROM products WHERE prod_name REGEXP '.000';

-- 如果需要匹配特殊字符，则需要添加<u>\\</u>为前导。<u>**\\-**</u>为查找<u>**-**</u>字符，<u>**\\.**</u>为查找<u>**.**</u>字符
SELECT vend_name FROM vendors WHERE vend_name REGEXP '\\.';
```


</details>


### 拼接字段

<details>
<summary>查找供应商和地区，并拼接在一块name(location)的样式</summary>

```sql
-- MySQL中使用Concat()拼接字符串
SELECT Concat(vend_name, '(', vend_country, ')') FROM vendors ORDER BY vend_name;

-- 使用函数Trim()来去除数据左右两侧多余的空格，RTrim()则是去掉右侧多余的空格，LTrim()则是去掉左侧多余的空格
SELECT Concat(Rtrim(vend_name), '(', Rtrim(vend_country), ')') FROM vendors ORDER BY vend_name;
```


</details>

<details>
<summary>拼接字段之后设置别名</summary>

```sql
-- 上述拼接完之后，如果不设置别名的话，其他人是没办法使用的，可以使用AS关键字设置别名
SELECT Concat(Trim(vend_name), '(', Trim(vend_country), ')') AS vend_title FROM vendors ORDER BY vend_name;
```


</details>

<details>
<summary>计算`orderitems`表里面`order_num`是20005的产品的每一项的总价，命名为`expanded_price`</summary>

```sql
-- 计算的话，可以直接使用+-*/
SELECT prod_id, quantity, item_price, quantity*item_price AS expanded_price FROM orderitems WHERE order_num = 20005;
```


</details>


### 常用函数

<details>
<summary>字母转换成大写</summary>

```sql
-- Upper()方法，将所有小写字母转换成大写字母
SELECT vend_name, Upper(vend_name) AS vend_name_upcase FROM vendors ORDER BY vend_name;
```


</details>

<details>
<summary>常用的一些函数</summary>

```sql
-- Left()  返回字符串左边的字符
-- Length() 返回字符串的长度
-- Locate() 找出串的一个子串
-- Lower() 将串转换成小写
-- LTrim() 去掉左边的空格
-- Right() 返回串右边的字符
-- RTrim() 去掉右边的空格
-- Soundex() 返回串的SOUNDEX值
-- SubString() 返回字串的字符
-- Upper() 将串转换成大写
```


</details>

<details>
<summary>常用的时间函数</summary>

![image.png](/images/c4188b0428b6811aa4f9477d01095cac.png)


</details>


> 💡 时间格式默认最好是：yyyy-mm-dd


```sql
SELECT * FROM orders WHERE Year(order_date) = 2005 AND Month(order_date) = 9;
```

<details>
<summary>数值处理函数</summary>

![image.png](/images/6c6498418121ba8d37f88aa3ba17f64f.png)


</details>


### 汇总数据

<details>
<summary>常用的汇总函数</summary>

![image.png](/images/3c72f4f7b4cf7884fd8441c37afaa1ea.png)


</details>

<details>
<summary>AVG函数</summary>

查询某一列的平均值，后面可以跟条件


```sql
-- 查询所有产品的平均值
SELECT AVG(prod_price) AS avg_price FROM products;

-- 查询vend_id为1003的产品的平均值
SELECT AVG(prod_price) AS avg_price FROM products WHERE vend_id = 1003;
```


</details>

<details>
<summary>COUNT函数</summary>

```sql
-- 查询某个表下数据总数
SELECT COUNT(*) AS num_cust FROM customers;

-- 只对有值的行计数，如果某一个行没有值，则不计数
SELECT COUNT(cust_email) AS num_cust FROM customers;
```


</details>

<details>
<summary>MAX函数和MIN函数</summary>

```sql
-- 查询最大值
SELECT MAX(prod_price) as max_price FROM products;

-- 查询最小值
SELECT MIN(prod_price) as min_price FROM products;
```


</details>

<details>
<summary>SUM函数</summary>

```sql
-- 计算某列下的所有值的和
SELECT SUM(quantity) AS items_ordered FROM orderitems WHERE order_num = 20005;

-- 计算值
SELECT SUM(quantity*item_price) AS total_price FROM orderitems WHERE order_num = 20005;

-- 去除重复的值
SELECT AVG(DISTINCT prod_price) AS avg_price FROM products WHERE vend_id = 1003;
```


</details>

<details>
<summary>组合聚集函数</summary>

```sql
SELECT COUNT(*) AS num_items, MIN(prod_price) AS price_min, MAX(prod_price) AS price_max, AVG(prod_price) AS price_avg FROM products;
```


</details>


### 分组数据

<details>
<summary>返回每个供应商提供的产品数目</summary>

```sql
SELECT vend_id COUNT(*) AS num_prods FROM products GROUP BY vend_id;
```


</details>

<details>
<summary>设置分组过滤条件</summary>

```sql
SELECT vend_id COUNT(*) AS num_prods FROM products GROUP BY vend_id HAVING COUNT(*) >= 3;
```


</details>

<details>
<summary>列出具有2个（含）以上、价格为10（含）以上的产品的供应商</summary>

```sql
SELECT vend_id, COUNT(*) AS num_prods FROM products WHERE prod_price >= 10 GROUP BY vend_id HAVING num_prods >= 2 ORDER BY num_prods;
```


</details>

<details>
<summary><u>**查找总计订单价格大于等于50的订单的订单号和总计订单价格，**</u><u>**`orderitems`**</u></summary>

```sql
SELECT order_num, SUM(item_price * quantity) AS ordertotal FROM orderitems GROUP BY order_num HAVING ordertotal >= 50 ORDER BY ordertotal;
```


</details>


### 子查询

> **最好先写出子查询的SQL语句，再组合**
<details>
<summary>要列出订购物品TNT2的所有客户</summary>
1. 检索包含物品TNT2的所有订单的编号`orderitems`
2. 检索具有前一步骤列出的订单编号的所有客户的ID`orders`
3. 检索前一步骤返回的所有客户ID的客户信息

```sql
-- 1. 检索包含物品TNT2的所有订单的编号
SELECT order_num FROM orderitems WHERE prod_id = 'TNT2';
-- 得到结果：20005, 20007

-- 2. 检索具有前一步骤列出的订单编号的所有客户的ID
SELECT cust_id FROM orders WHERE order_num IN (20005, 20007);
-- 得到结果：10001, 10004

-- 3. 检索前一步骤返回的所有客户ID的客户信息
SELECT * FROM customers WHERE cust_id IN (10001, 10004);



-- 1和2可以合并成一个语句
SELECT cust_id FROM orders WHERE order_num IN (SELECT order_num FROM orderitems WHERE prod_id = 'TNT2');

-- 1、2、3三个合并成一个子句
SELECT * FROM customers WHERE cust_id IN (SELECT cust_id FROM orders WHERE order_num IN (SELECT order_num FROM orderitems WHERE prod_id = 'TNT2'));
```


</details>

<details>
<summary>显示customers表中每个客户的订单总数，订单与相应的客户ID存储在orders表中</summary>

```sql
SELECT cust_name, cust_state, (SELECT COUNT(*) FROM orders WHERE orders.cust_id = customers.cust_id) AS orders FROM customers;
```


</details>


### 联结表

<details>
<summary>找出有产品的供应商的所有产品，vend_name, prod_name, prod_price</summary>

```sql
SELECT vend_name, prod_name, prod_price FROM vendors, products WHERE vendors.vend_id = products.vend_id ORDER BY vend_name, prod_name;
```


</details>

<details>
<summary>使用Join关键字</summary>

```sql
SELECT vend_name, prod_name, prod_price FROM vendors INNER JOIN products ON vendors.vend_id = products.vend_id;
```


</details>

<details>
<summary>显示编号为20005的订单中的物品，prod_name, vend_name, prod_price, quantity</summary>

```sql
SELECT prod_name, vend_name, prod_price, quantity FROM orderitems, vendors, products WHERE orderitems.prod_id = products.prod_id AND vendors.vend_id = products.vend_id AND order_num = 20005;
```


</details>

<details>
<summary>查找购买了产品ID是`TNT2` 的用户名和用户联系方式</summary>

```sql
-- 首先查看orders、orderitems、customer的数据结构
DESC orders;
DESC orderitems;
DESC customers;

SELECT cust_name, cust_contact FROM orders, orderitems, customers WHERE orderitems.order_num = orders.order_num AND orders.cust_id = customers.cust_id AND orderitems.prod_id = 'TNT2';
```


</details>


### 高级联结

<details>
<summary>自联结：查询产品id为`DTNTR` 的相同供应商的其他产品，这里设置过滤条件的时候，不能用要查询的表</summary>

```sql
SELECT p1.vend_id, p1.prod_id, p1.prod_name FROM products as p1, products as p2 WHERE p1.vend_id = p2.vend_id AND p2.vend_id = 'DTNTR';
```


</details>

<details>
<summary>外部联结：对每个客户下了多少订单进行计数，包括那些至今尚未下订单的客户</summary>

```sql
SELECT customers.cust_id, orders.order_num FROM customers LEFT OUTER JOIN orders ON customers.cust_id = orders.cust_id;
```


</details>

<details>
<summary>使用带聚集函数的联结，检索所有客户及每个客户所下的订单数，（所有客户-GROUP BY 客户的ID)</summary>

```sql
SELECT customers.*, COUNT(*) AS cust_order_count FROM customers INNER JOIN orders ON customers.cust_id = orders.cust_id GROUP BY customers.cust_id;
```


</details>

<details>
<summary>检索所有客户及每个客户所下的订单数，包含没有订单的客户（所有客户-GROUP BY 客户的ID)</summary>

```sql
SELECT customers.cust_name, customers.cust_id, COUNT(orders.order_num) AS num_ord FROM customers LEFT OUTER JOIN orders ON customers.cust_id = orders.cust_id GROUP BY customers.cust_id;
```


</details>


### 组合查询

<details>
<summary>需要价格小于等于5的所有物品，以及供应商是1001和1002的所有物品，使用组合查询</summary>

```sql
SELECT vend_id, prod_id, prod_price FROM products WHERE prod_price <= 5 UNION SELECT vend_id, prod_id, prod_price FROM products WHERE vend_id in (1001, 1002);
```


</details>

<details>
<summary>需要价格小于等于5的所有物品，以及供应商是1001和1002的所有物品，使用组合查询，显示重复的行，并排序</summary>

```sql
SELECT vend_id, prod_id, prod_price FROM products WHERE prod_price <= 5 UNION ALL SELECT vend_id, prod_id, prod_price FROM products WHERE vend_id in (1001, 1002) ORDER BY vend_id, prod_price;
```


</details>


### 全文本搜索

<details>
<summary>搜索产品备注里面包含`rabbit` 的数据</summary>

```sql
SELECT * FROM productnotes MATCH(note_text) AGAINST('rabbit');
```


</details>

<details>
<summary>搜索产品备注里面包含`anvils` 的数据（扩展数据）</summary>

```sql
SELECT * FROM productnotes WHERE Match(note_text) Against('anvils' WITH QUERY EXPANSION);
```


</details>

<details>
<summary>全文本布尔操作符</summary>

![image.png](/images/5191d307a0316136d22da2672f263de2.png)


</details>

<details>
<summary>布尔文本搜索：匹配包含`heavy`但不包含任意以`rope`开始的词的行</summary>

```sql
SELECT * FROM productnotes WHERE Match(note_text) Against('heavy -rope*' IN BOOLEAN MODE);
```


</details>

<details>
<summary>匹配包含词`rabbit`和`bait`的行</summary>

```sql
SELECT * FROM productnotes WHERE Match(note_text) Against('+rabbit +bait' IN BOOLEAN MODE);
```


</details>

<details>
<summary>匹配`rabbit`和`bait`至少包含一个的行</summary>

```sql
SELECT * FROM productnotes WHERE Match(note_text) Against('rabbit bait' IN BOOLEAN MODE);
```


</details>

<details>
<summary>匹配短语`rabbit bait` 的行</summary>

```sql
SELECT * FROM productnotes WHERE Match(note_text) Against('"rabbit bait"' IN BOOLEAN MODE);
```


</details>

<details>
<summary>匹配`rabbit`和`carrot`，增加前者的等级，降低后者的等级。</summary>

```sql
SELECT * FROM productnotes WHERE Match(note_text) Against('>rabbit <carrot' IN BOOLEAN MODE);
```


</details>

<details>
<summary>搜索匹配词同时包含`safe`和`combination`，降低后者的等级</summary>

```sql
SELECT * FROM productnotes WHERE Match(note_text) Against('+safe +(<combination)' IN BOOLEAN MODE);
```


</details>


## 常用关键字

- SHOW：显示
- DATABASES：数据库
- TABLE：表
- COLUMN：列
- ROW：行
- PRIMARY KEY：主键
- CREATE：新建
- WHERE：哪个
- IS：是
- FROM：从哪里
- DELETE：删除数据
- LIKE：通配符匹配
- REGEXP：正则表达式匹配
- AS：设置别名
- GROUP BY：分组
- HVING：分组过滤
- INNER JOIN：联结
- LEFT OUTER JOIN
- RIGHT OUTER JOIN
- ON
- AND
- UNION：组合查询
- UNION ALL：组合查询不自动去重
- FULLTEXT：建立全文索引，算是一个方法，后面跟字段
- WITH QUERY EXPANSION：搜索扩展
- IN BOOLEAN MODE：布尔文本搜索
- 
