

初始化脚本：

########################################
# MySQL Crash Course
# http://www.forta.com/books/0672327120/
# Example table creation scripts
########################################


########################
# Create customers table
########################
CREATE TABLE customers
(
  cust_id      int       NOT NULL AUTO_INCREMENT,
  cust_name    char(50)  NOT NULL ,
  cust_address char(50)  NULL ,
  cust_city    char(50)  NULL ,
  cust_state   char(5)   NULL ,
  cust_zip     char(10)  NULL ,
  cust_country char(50)  NULL ,
  cust_contact char(50)  NULL ,
  cust_email   char(255) NULL ,
  PRIMARY KEY (cust_id)
) ENGINE=InnoDB;

#########################
# Create orderitems table
#########################
CREATE TABLE orderitems
(
  order_num  int          NOT NULL ,
  order_item int          NOT NULL ,
  prod_id    char(10)     NOT NULL ,
  quantity   int          NOT NULL ,
  item_price decimal(8,2) NOT NULL ,
  PRIMARY KEY (order_num, order_item)
) ENGINE=InnoDB;


#####################
# Create orders table
#####################
CREATE TABLE orders
(
  order_num  int      NOT NULL AUTO_INCREMENT,
  order_date datetime NOT NULL ,
  cust_id    int      NOT NULL ,
  PRIMARY KEY (order_num)
) ENGINE=InnoDB;

#######################
# Create products table
#######################
CREATE TABLE products
(
  prod_id    char(10)      NOT NULL,
  vend_id    int           NOT NULL ,
  prod_name  char(255)     NOT NULL ,
  prod_price decimal(8,2)  NOT NULL ,
  prod_desc  text          NULL ,
  PRIMARY KEY(prod_id)
) ENGINE=InnoDB;

######################
# Create vendors table
######################
CREATE TABLE vendors
(
  vend_id      int      NOT NULL AUTO_INCREMENT,
  vend_name    char(50) NOT NULL ,
  vend_address char(50) NULL ,
  vend_city    char(50) NULL ,
  vend_state   char(5)  NULL ,
  vend_zip     char(10) NULL ,
  vend_country char(50) NULL ,
  PRIMARY KEY (vend_id)
) ENGINE=InnoDB;

###########################
# Create productnotes table
###########################
CREATE TABLE productnotes
(
  note_id    int           NOT NULL AUTO_INCREMENT,
  prod_id    char(10)      NOT NULL,
  note_date datetime       NOT NULL,
  note_text  text          NULL ,
  PRIMARY KEY(note_id),
  FULLTEXT(note_text)
) ENGINE=MyISAM;


#####################
# Define foreign keys
#####################
ALTER TABLE orderitems ADD CONSTRAINT fk_orderitems_orders FOREIGN KEY (order_num) REFERENCES orders (order_num);
ALTER TABLE orderitems ADD CONSTRAINT fk_orderitems_products FOREIGN KEY (prod_id) REFERENCES products (prod_id);
ALTER TABLE orders ADD CONSTRAINT fk_orders_customers FOREIGN KEY (cust_id) REFERENCES customers (cust_id);
ALTER TABLE products ADD CONSTRAINT fk_products_vendors FOREIGN KEY (vend_id) REFERENCES vendors (vend_id);





populate:



########################################
# MySQL Crash Course
# http://www.forta.com/books/0672327120/
# Example table population scripts
########################################


##########################
# Populate customers table
##########################
INSERT INTO customers(cust_id, cust_name, cust_address, cust_city, cust_state, cust_zip, cust_country, cust_contact, cust_email)
VALUES(10001, 'Coyote Inc.', '200 Maple Lane', 'Detroit', 'MI', '44444', 'USA', 'Y Lee', 'ylee@coyote.com');
INSERT INTO customers(cust_id, cust_name, cust_address, cust_city, cust_state, cust_zip, cust_country, cust_contact)
VALUES(10002, 'Mouse House', '333 Fromage Lane', 'Columbus', 'OH', '43333', 'USA', 'Jerry Mouse');
INSERT INTO customers(cust_id, cust_name, cust_address, cust_city, cust_state, cust_zip, cust_country, cust_contact, cust_email)
VALUES(10003, 'Wascals', '1 Sunny Place', 'Muncie', 'IN', '42222', 'USA', 'Jim Jones', 'rabbit@wascally.com');
INSERT INTO customers(cust_id, cust_name, cust_address, cust_city, cust_state, cust_zip, cust_country, cust_contact, cust_email)
VALUES(10004, 'Yosemite Place', '829 Riverside Drive', 'Phoenix', 'AZ', '88888', 'USA', 'Y Sam', 'sam@yosemite.com');
INSERT INTO customers(cust_id, cust_name, cust_address, cust_city, cust_state, cust_zip, cust_country, cust_contact)
VALUES(10005, 'E Fudd', '4545 53rd Street', 'Chicago', 'IL', '54545', 'USA', 'E Fudd');


########################
# Populate vendors table
########################
INSERT INTO vendors(vend_id, vend_name, vend_address, vend_city, vend_state, vend_zip, vend_country)
VALUES(1001,'Anvils R Us','123 Main Street','Southfield','MI','48075', 'USA');
INSERT INTO vendors(vend_id, vend_name, vend_address, vend_city, vend_state, vend_zip, vend_country)
VALUES(1002,'LT Supplies','500 Park Street','Anytown','OH','44333', 'USA');
INSERT INTO vendors(vend_id, vend_name, vend_address, vend_city, vend_state, vend_zip, vend_country)
VALUES(1003,'ACME','555 High Street','Los Angeles','CA','90046', 'USA');
INSERT INTO vendors(vend_id, vend_name, vend_address, vend_city, vend_state, vend_zip, vend_country)
VALUES(1004,'Furball Inc.','1000 5th Avenue','New York','NY','11111', 'USA');
INSERT INTO vendors(vend_id, vend_name, vend_address, vend_city, vend_state, vend_zip, vend_country)
VALUES(1005,'Jet Set','42 Galaxy Road','London', NULL,'N16 6PS', 'England');
INSERT INTO vendors(vend_id, vend_name, vend_address, vend_city, vend_state, vend_zip, vend_country)
VALUES(1006,'Jouets Et Ours','1 Rue Amusement','Paris', NULL,'45678', 'France');


#########################
# Populate products table
#########################
INSERT INTO products(prod_id, vend_id, prod_name, prod_price, prod_desc)
VALUES('ANV01', 1001, '.5 ton anvil', 5.99, '.5 ton anvil, black, complete with handy hook');
INSERT INTO products(prod_id, vend_id, prod_name, prod_price, prod_desc)
VALUES('ANV02', 1001, '1 ton anvil', 9.99, '1 ton anvil, black, complete with handy hook and carrying case');
INSERT INTO products(prod_id, vend_id, prod_name, prod_price, prod_desc)
VALUES('ANV03', 1001, '2 ton anvil', 14.99, '2 ton anvil, black, complete with handy hook and carrying case');
INSERT INTO products(prod_id, vend_id, prod_name, prod_price, prod_desc)
VALUES('OL1', 1002, 'Oil can', 8.99, 'Oil can, red');
INSERT INTO products(prod_id, vend_id, prod_name, prod_price, prod_desc)
VALUES('FU1', 1002, 'Fuses', 3.42, '1 dozen, extra long');
INSERT INTO products(prod_id, vend_id, prod_name, prod_price, prod_desc)
VALUES('SLING', 1003, 'Sling', 4.49, 'Sling, one size fits all');
INSERT INTO products(prod_id, vend_id, prod_name, prod_price, prod_desc)
VALUES('TNT1', 1003, 'TNT (1 stick)', 2.50, 'TNT, red, single stick');
INSERT INTO products(prod_id, vend_id, prod_name, prod_price, prod_desc)
VALUES('TNT2', 1003, 'TNT (5 sticks)', 10, 'TNT, red, pack of 10 sticks');
INSERT INTO products(prod_id, vend_id, prod_name, prod_price, prod_desc)
VALUES('FB', 1003, 'Bird seed', 10, 'Large bag (suitable for road runners)');
INSERT INTO products(prod_id, vend_id, prod_name, prod_price, prod_desc)
VALUES('FC', 1003, 'Carrots', 2.50, 'Carrots (rabbit hunting season only)');
INSERT INTO products(prod_id, vend_id, prod_name, prod_price, prod_desc)
VALUES('SAFE', 1003, 'Safe', 50, 'Safe with combination lock');
INSERT INTO products(prod_id, vend_id, prod_name, prod_price, prod_desc)
VALUES('DTNTR', 1003, 'Detonator', 13, 'Detonator (plunger powered), fuses not included');
INSERT INTO products(prod_id, vend_id, prod_name, prod_price, prod_desc)
VALUES('JP1000', 1005, 'JetPack 1000', 35, 'JetPack 1000, intended for single use');
INSERT INTO products(prod_id, vend_id, prod_name, prod_price, prod_desc)
VALUES('JP2000', 1005, 'JetPack 2000', 55, 'JetPack 2000, multi-use');



#######################
# Populate orders table
#######################
INSERT INTO orders(order_num, order_date, cust_id)
VALUES(20005, '2005-09-01', 10001);
INSERT INTO orders(order_num, order_date, cust_id)
VALUES(20006, '2005-09-12', 10003);
INSERT INTO orders(order_num, order_date, cust_id)
VALUES(20007, '2005-09-30', 10004);
INSERT INTO orders(order_num, order_date, cust_id)
VALUES(20008, '2005-10-03', 10005);
INSERT INTO orders(order_num, order_date, cust_id)
VALUES(20009, '2005-10-08', 10001);


###########################
# Populate orderitems table
###########################
INSERT INTO orderitems(order_num, order_item, prod_id, quantity, item_price)
VALUES(20005, 1, 'ANV01', 10, 5.99);
INSERT INTO orderitems(order_num, order_item, prod_id, quantity, item_price)
VALUES(20005, 2, 'ANV02', 3, 9.99);
INSERT INTO orderitems(order_num, order_item, prod_id, quantity, item_price)
VALUES(20005, 3, 'TNT2', 5, 10);
INSERT INTO orderitems(order_num, order_item, prod_id, quantity, item_price)
VALUES(20005, 4, 'FB', 1, 10);
INSERT INTO orderitems(order_num, order_item, prod_id, quantity, item_price)
VALUES(20006, 1, 'JP2000', 1, 55);
INSERT INTO orderitems(order_num, order_item, prod_id, quantity, item_price)
VALUES(20007, 1, 'TNT2', 100, 10);
INSERT INTO orderitems(order_num, order_item, prod_id, quantity, item_price)
VALUES(20008, 1, 'FC', 50, 2.50);
INSERT INTO orderitems(order_num, order_item, prod_id, quantity, item_price)
VALUES(20009, 1, 'FB', 1, 10);
INSERT INTO orderitems(order_num, order_item, prod_id, quantity, item_price)
VALUES(20009, 2, 'OL1', 1, 8.99);
INSERT INTO orderitems(order_num, order_item, prod_id, quantity, item_price)
VALUES(20009, 3, 'SLING', 1, 4.49);
INSERT INTO orderitems(order_num, order_item, prod_id, quantity, item_price)
VALUES(20009, 4, 'ANV03', 1, 14.99);

#############################
# Populate productnotes table
#############################
INSERT INTO productnotes(note_id, prod_id, note_date, note_text)
VALUES(101, 'TNT2', '2005-08-17',
'Customer complaint:
Sticks not individually wrapped, too easy to mistakenly detonate all at once.
Recommend individual wrapping.'
);
INSERT INTO productnotes(note_id, prod_id, note_date, note_text)
VALUES(102, 'OL1', '2005-08-18',
'Can shipped full, refills not available.
Need to order new can if refill needed.'
);
INSERT INTO productnotes(note_id, prod_id, note_date, note_text)
VALUES(103, 'SAFE', '2005-08-18',
'Safe is combination locked, combination not provided with safe.
This is rarely a problem as safes are typically blown up or dropped by customers.'
);
INSERT INTO productnotes(note_id, prod_id, note_date, note_text)
VALUES(104, 'FC', '2005-08-19',
'Quantity varies, sold by the sack load.
All guaranteed to be bright and orange, and suitable for use as rabbit bait.'
);
INSERT INTO productnotes(note_id, prod_id, note_date, note_text)
VALUES(105, 'TNT2', '2005-08-20',
'Included fuses are short and have been known to detonate too quickly for some customers.
Longer fuses are available (item FU1) and should be recommended.'
);
INSERT INTO productnotes(note_id, prod_id, note_date, note_text)
VALUES(106, 'TNT2', '2005-08-22',
'Matches not included, recommend purchase of matches or detonator (item DTNTR).'
);
INSERT INTO productnotes(note_id, prod_id, note_date, note_text)
VALUES(107, 'SAFE', '2005-08-23',
'Please note that no returns will be accepted if safe opened using explosives.'
);
INSERT INTO productnotes(note_id, prod_id, note_date, note_text)
VALUES(108, 'ANV01', '2005-08-25',
'Multiple customer returns, anvils failing to drop fast enough or falling backwards on purchaser. Recommend that customer considers using heavier anvils.'
);
INSERT INTO productnotes(note_id, prod_id, note_date, note_text)
VALUES(109, 'ANV03', '2005-09-01',
'Item is extremely heavy. Designed for dropping, not recommended for use with slings, ropes, pulleys, or tightropes.'
);
INSERT INTO productnotes(note_id, prod_id, note_date, note_text)
VALUES(110, 'FC', '2005-09-01',
'Customer complaint: rabbit has been able to detect trap, food apparently less effective now.'
);
INSERT INTO productnotes(note_id, prod_id, note_date, note_text)
VALUES(111, 'SLING', '2005-09-02',
'Shipped unassembled, requires common tools (including oversized hammer).'
);
INSERT INTO productnotes(note_id, prod_id, note_date, note_text)
VALUES(112, 'SAFE', '2005-09-02',
'Customer complaint:
Circular hole in safe floor can apparently be easily cut with handsaw.'
);
INSERT INTO productnotes(note_id, prod_id, note_date, note_text)
VALUES(113, 'ANV01', '2005-09-05',
'Customer complaint:
Not heavy enough to generate flying stars around head of victim. If being purchased for dropping, recommend ANV02 or ANV03 instead.'
);
INSERT INTO productnotes(note_id, prod_id, note_date, note_text)
VALUES(114, 'SAFE', '2005-09-07',
'Call from individual trapped in safe plummeting to the ground, suggests an escape hatch be added.
Comment forwarded to vendor.'
);







# Mysql-crashcourse

## Mysql基础学习笔记

- Chapter1 了解SQL
- Chapter2 MySQL简介
- Chapter3 使用MySQL
- Chapter4 检索数据
- Chapter5 排序检索数据
- Chapter6 过滤数据
- Chapter7 数据过滤
- Chapter8 用通配符进行过滤
- Chapter9 用正则表达式进行搜索
- Chapter10 创建计算字段
- Chapter11 使用数据处理函数
- Chapter12 汇总数据
- Chapter13 分组数据
- Chapter14 使用子查询
- Chapter15 联结表
- Chapter16 创建高级联结
- Chapter17 组合查询
- Chapter18 全文本搜索
- Chapter19 插入数据
- Chapter20 更新和删除数据源
- Chapter21 创建和操纵表
- Chapter22 使用视图
- Chapter23 使用存储过程
- Chapter24 使用游标
- Chapter25 使用触发器
- Chapter26 管理事务处理
- Chapter27 全球化和本地化
- Chapter28 安全管理
- Chapter29 数据库维护
- Chapter30 改善性能









-- 1.1.1 数据库database
show DATABASES;
-- 1.1.2 表table
show tables;
-- 1.1.3 列和数据类型 column
-- 1.1.4 行 row
-- 1.1.5 主键 primary key



-- Chapter2 MySQL简介
-- 本章看书即可，没有具体SQL语法教程



-- 为了使用crashcourse
use crashcourse;
-- 数据库、表、列、用户、权限等的信息被存储在数据库和表中，MySQL的SHOW命令来显示这些信息(MySQL从内部表中提取这些信息)
show DATABASES;
show TABLES;
-- SHOW也可以用来显示表列
show COLUMNS from customers;
-- 用于显示广泛的服务器状态信息
show STATUS;
-- 显示授予用户的安全权限
show GRANTS;
-- 显示服务器错误
show ERRORS;
-- 显示警告信息
show WARNINGS;







-- 检索单个列
SELECT prod_name from products;
-- 检索多个列
SELECT prod_id,prod_name,prod_price from products;
-- 检索所有列,'*'通配符返回表中所有列
SELECT * from products;
-- 检索不同的行
SELECT vend_id from products;
-- DISTINCT关键字指示MySQL只返回不同的值，去重作用
SELECT DISTINCT vend_id from products;
-- LIMIT 5指示MySQL返回指定的行数,5行
SELECT prod_name from products LIMIT 5;
-- LIMIT 5,5指示MySQL返回从行5开始的5行。第一个数为开始位置，第二个数为要检索的行数。检索出来的第一行为行0，而不是行1
SELECT prod_name from products LIMIT 5,5;
-- 使用完全限定的名字来引用列，限定列名
SELECT products.prod_name from products;
-- 限定表名
SELECT products.prod_name from crashcourse.products;







-- 排序检索数据
-- 为了明确地排序用SELECT语句检索出的数据，可使用ORDER BY子句。ORDER BY子句取一个或多个列的名字，据此对输出进行排序
-- 对prod_name列以字母顺序排序数据的ORDER BY子句
SELECT prod_name from products ORDER BY prod_name;
-- 按多个列排序
-- 下面的代码检索3个列，并按其中两个列对结果进行排序，首先按照prod_price，然后再按prod_name排序
SELECT prod_id,prod_price,prod_name from products ORDER BY prod_price,prod_name;
-- 指定排序方向。数据排序不限于升序排序(从A到Z)。这只是默认的排序顺序，还可以使用ORDER BY子句以降序(从Z到A)顺序排序。为了进行降序排序，必须指定DESC关键字
-- 按价格以降序排序产品
SELECT prod_id,prod_price,prod_name from products ORDER BY prod_price DESC;
-- 以降序排序产品价格，然后再对产品名升序排序。DESC关键字只应用到直接位于其前面的列名。下面代码中只对prod_price列指定DESC，对prod_name列不指定
-- 如果想在多个列上进行降序排序，必须对每个列指定DESC关键字
SELECT prod_id,prod_price,prod_name from products ORDER BY prod_price DESC,prod_name;
-- 使用order by和LIMIT组合，能够找出一个列中最高或最低的值。
SELECT prod_price from products ORDER BY prod_price DESC LIMIT 1;



-- 过滤数据
-- 使用WHERE子句，指定搜索条件，也称为过滤条件
-- 这个语句从products表中检索两个列，但不返回所有行，只返回prod_price值为2.50的行
SELECT prod_name,prod_price from products WHERE prod_price=2.5;
-- 检查单个值
-- 检查WHERE prod_name='fuses'语句，它返回prod_name的值为Fuses的一行。MySQL在执行匹配时默认不区分大小写，所以fuses与Fuses匹配
SELECT prod_name,prod_price from products WHERE prod_name='fuses';
-- 列出价格小于10美元的所有产品
SELECT prod_name,prod_price FROM products WHERE prod_price <10;
-- 下一条语句检索价格小于等于10美元的所有产品
SELECT prod_name,prod_price FROM products WHERE prod_price <= 10;
-- 不匹配检查,列出不是由供应商1003制造的所有产品
SELECT vend_id,prod_name from products WHERE vend_id <> 1003;
-- 下面是相同的例子，其中使用!=而不是<>操作符
SELECT vend_id,prod_name from products WHERE vend_id != 1003;
-- 范围值检查,检索价格在5美元和10美元之间的所有产品。BETWEEN匹配范围中所有的值，包括指定的开始值和结束值
SELECT prod_name,prod_price FROM products WHERE prod_price BETWEEN 5 AND 10;
-- 空值检查,IS NULL子句用来检查具有NULL值得列。这条语句返回没有价格(空prod_price字段，不是价格为0)的所有产品，由于表中没有这样的行，所有没有返回数据
SELECT prod_name from products WHERE prod_price IS NULL;
SELECT cust_id from customers where cust_email IS NULL;



-- 高级数据过滤
-- 组合WHERE子句
-- AND操作符：这条SELECT语句中的WHERE子句包含两个条件，并且用AND关键字联结它们。
SELECT prod_id,prod_price,prod_name from products WHERE vend_id = 1003 AND prod_price <= 10;
-- OR操作符：指示MySQL检索匹配任一条件的行
SELECT prod_name,prod_price from products WHERE vend_id = 1002 OR vend_id = 1003;
-- 计算次序：WHERE可包含任意数目的AND和OR操作符。允许两者以进行复杂和高级的过滤
-- 但是组合AND和OR也带来了一个有趣的问题,SQL在处理OR操作符前，优先处理AND操作符。
SELECT vend_id,prod_name,prod_price from products WHERE vend_id=1002 OR vend_id = 1003 AND prod_price>=10;
-- 此问题的解决方法是使用圆括号明确地分组相应的操作符
SELECT prod_name,prod_price from products WHERE (vend_id=1002 OR vend_id=1003) AND prod_price>=10;
-- IN操作符:IN操作符用来指定条件范围，范围中的每个条件都可以进行匹配。IN取合法值的由逗号分隔的清单，全部在圆括号中
SELECT prod_name,prod_price from products WHERE vend_id IN (1002,1003) ORDER BY prod_name;
-- IN操作符完成与OR相同的功能
SELECT prod_name,prod_price from products WHERE vend_id=1002 OR vend_id=1003 ORDER BY prod_name;
-- NOT操作符：为了列出除1002和1003之外的所有供应商制造的产品，可编写以下代码
SELECT prod_name,prod_price from products WHERE vend_id NOT IN (1002,1003) ORDER BY prod_name;



-- 用通配符进行过滤
-- LIKE操作符
-- 百分号(%)通配符：%表示任何字符出现任意次数
SELECT prod_id,prod_name from products WHERE prod_name LIKE 'jet%';
-- 通配符可在搜索模式中任意位置使用，并且可以使用多个通配符
SELECT prod_id,prod_name from products WHERE prod_name LIKE '%anvil%';
-- 通配符也可以出现在搜索模式的中间
SELECT prod_name from products WHERE prod_name LIKE 's%e';
-- 下划线(_)通配符:只匹配单个字符而不是多个字符
SELECT prod_id,prod_name from products WHERE prod_name LIKE '_ ton anvil';



-- 用正则表达式进行搜索
-- 正则表达式的作用是匹配文本，将一个模式与一个文本串进行比较。MySQL用WHERE子句对正则表达式提供了初步的支持，允许你指定正则表达式，过滤SELECT检索出的数据
SELECT prod_name from products WHERE prod_name REGEXP '1000' ORDER BY prod_name;
-- 下面的代码中使用了正则表达式.000。.是正则表达式中一个特殊的字符，它表示匹配任意一个字符，因此1000和2000都匹配且返回
SELECT prod_name FROM products WHERE prod_name REGEXP '.000' ORDER BY prod_name;
-- 进行OR匹配:|为正则表达式的OR操作符，它表示匹配其中之一
SELECT prod_name FROM products WHERE prod_name REGEXP '1000|2000' ORDER BY prod_name;
-- 匹配几个字符之一:这里使用了正则表达式[123] Ton。[123]定义一组字符，它的意思是匹配1或2或3.因此1 ton和2 ton都匹配且返回
SELECT prod_name FROM products WHERE prod_name REGEXP '[123] Ton' ORDER BY prod_name;
-- []是另一种形式的OR语句
SELECT prod_name FROM products WHERE prod_name REGEXP '1|2|3 Ton' ORDER BY prod_name;
-- 匹配范围：集合可用来定义要匹配的一个或多个字符
SELECT prod_name FROM products WHERE prod_name REGEXP '[1-5] Ton' ORDER BY prod_name;
-- 匹配特殊字符:这不是期望的输出，.匹配任意字符，因此每个行都被检索出来
SELECT vend_name FROM vendors WHERE vend_name REGEXP '.' ORDER BY vend_name;
-- 为了匹配特殊字符，必须用\\为前导。\\-表示查找-，\\.表示查找.
SELECT vend_name FROM vendors WHERE vend_name REGEXP '\\.' ORDER BY vend_name;
-- 匹配字符类,匹配多个实例
SELECT prod_name FROM products WHERE prod_name REGEXP '\\([0-9] sticks?\\)';
SELECT prod_name FROM products WHERE prod_name REGEXP '[[0-9]]{4}';
-- 定位符
-- 如果想找出一个数(包括以小数点开始的数)开始的所有产品，简单搜索[0-9\\.](或[[0-9]\\.])不行，因为它将在文本内任意位置查找匹配。解决办法是使用^定位符。
SELECT prod_name from products WHERE prod_name REGEXP '^[0-9\\.]' ORDER BY prod_name;



-- 创建计算字段
-- 拼接字段Concat()函数来拼接两个列：Concat()拼接串，即把多个串连接起来形成一个较长的串。各个串之间用逗号分隔
SELECT CONCAT(vend_name,'(',vend_country,')') FROM vendors ORDER BY vend_name;
-- RTrim()函数删除数据右侧多余的空格来整理数据
SELECT Concat(RTRIM(vend_name),'(',RTRIM(vend_country),')') FROM vendors ORDER BY vend_name;
-- 使用别名
SELECT Concat(RTRIM(vend_name),'(',RTRIM(vend_country),')') AS vend_title FROM vendors ORDER BY vend_name;
-- 执行算术计算
SELECT prod_id,quantity,item_price FROM orderitems WHERE order_num = 20005;
SELECT prod_id,quantity,item_price,quantity*item_price AS expanded_price FROM orderitems WHERE order_num=20005;



-- 使用数据处理函数
-- 文本处理函数:Upper()函数将文本转换为大写
SELECT vend_name,UPPER(vend_name) AS vend_name_upcase FROM vendors ORDER BY vend_name;
-- 日期和事件处理函数
SELECT cust_id,order_num FROM orders WHERE order_date='2005-09-01';
-- 如果要的是日期，请使用Date()
SELECT cust_id,order_num FROM orders WHERE DATE(order_date)='2005-09-01';
SELECT cust_id,order_num FROM orders WHERE DATE(order_date) BETWEEN '2005-09-01' AND '2005-09-30';
SELECT cust_id,order_num FROM orders WHERE YEAR(order_date)=2005 AND MONTH(order_date)=9;



-- 汇总数据
-- 聚集函数 aggregate function
-- AVG函数:使用AVG()返回products表中所有产品的平均价格
SELECT AVG(prod_price) AS avg_price FROM products;
-- AVG()也可以用来确定特定列或行的平均值
SELECT AVG(prod_price) AS avg_price FROM products WHERE vend_id=1003;
-- COUNT函数
SELECT COUNT(*) AS num_cust FROM customers;
-- 对cust_email列中有值得行进行计数
SELECT COUNT(cust_email) AS num_cust FROM customers;
-- MAX函数
SELECT MAX(prod_price) AS max_price FROM products;
-- MIN函数
SELECT MIN(prod_price) AS min_price FROM products;
-- SUM函数:SUM()用来返回指定列值的和
SELECT SUM(quantity) AS items_ordered FROM orderitems WHERE order_num=20005;
-- SUM()也可以用来合计计算值
SELECT SUM(item_price*quantity) AS total_price FROM orderitems WHERE order_num=20005;
-- 聚集不同值
SELECT AVG(DISTINCT prod_price) AS avg_price FROM products WHERE vend_id=1003;
-- 组合聚集函数
SELECT COUNT(*) AS num_items,MIN(prod_price) AS price_min,MAX(prod_price) AS price_max,AVG(prod_price) AS price_avg FROM products;



-- 分组数据
-- 创建分组：分组是在SELECT语句的GROUP BY子句中建立的
SELECT vend_id,COUNT(*) AS num_prods FROM products GROUP BY vend_id;
-- 过滤分组：WHERE过滤行，HAVING过滤分组
SELECT cust_id,COUNT(*) AS orders FROM orders GROUP BY cust_id HAVING COUNT(*)>=2;
-- HAVING和WHERE的差别。WHERE在数据分组前进行过滤，HAVING在数据分组后进行过滤。WHERE排除的行不包括在分组中
SELECT vend_id,COUNT(*) AS num_prods FROM products WHERE prod_price>=10 GROUP BY vend_id HAVING COUNT(*)>=2;
SELECT vend_id,COUNT(*) AS num_prods FROM products GROUP BY vend_id HAVING COUNT(*) >=2;
-- 分组和排序
-- 一般在使用GROUP BY子句时，应该也给出ORDER BY子句。这是保证数据正确排序的唯一方法。千万不要仅依赖GROUP BY排序数据
SELECT order_num,SUM(quantity*item_price) AS ordertotal FROM orderitems GROUP BY order_num HAVING SUM(quantity*item_price)>=50;
-- 为按总计订单价格排序输出，需要添加ORDER BY子句
SELECT order_num,SUM(quantity*item_price) AS ordertotal FROM orderitems GROUP BY order_num HAVING SUM(quantity*item_price)>=50 ORDER BY ordertotal;



-- 使用子查询
-- 利用子查询进行过滤
SELECT order_num FROM orderitems WHERE prod_id='TNT2';
SELECT cust_id FROM orders WHERE order_num IN (20005,20007);
SELECT cust_id from orders WHERE order_num IN (SELECT order_num FROM orderitems WHERE prod_id='TNT2');
SELECT cust_name,cust_contact FROM customers WHERE cust_id IN (SELECT cust_id FROM orders WHERE order_num IN (SELECT order_num FROM orderitems WHERE prod_id='TNT2'));
-- 作为计算字段使用子查询
SELECT COUNT(*) AS orders FROM orders WHERE cust_id=10001;
SELECT cust_name,cust_state,(SELECT COUNT(*) FROM orders WHERE orders.cust_id=customers.cust_id) AS orders FROM customers ORDER BY cust_name;



-- 联结表
-- 创建联结
SELECT vend_name,prod_name,prod_price from vendors,products WHERE vendors.vend_id = products.vend_id ORDER BY vend_name,prod_name;
-- 内部联结
SELECT vend_name,prod_name,prod_price from vendors INNER JOIN products ON vendors.vend_id=products.vend_id;
-- 联结多个表
SELECT prod_name,vend_name,prod_price,quantity from orderitems,products,vendors WHERE products.vend_id=vendors.vend_id AND orderitems.prod_id=products.prod_id AND order_num =20005;



-- 创建高级联结
-- 使用表别名
SELECT cust_name,cust_contact FROM customers AS C,orders AS o,orderitems AS oi WHERE c.cust_id=o.cust_id AND oi.order_num = o.order_num AND prod_id='TNT2';
-- 使用不同类型的联结:自联结、自然联结和外部联结
-- 自联结
SELECT prod_id,prod_name from products WHERE vend_id=(SELECT vend_id from products WHERE prod_id='DTNTR');
SELECT p1.prod_id,p1.prod_name FROM products AS p1,products AS p2 WHERE p1.vend_id=p2.vend_id AND p2.prod_id='DTNTR';
-- 自然联结:你只能选择那些唯一的列。这一般是通过对表使用通配符(SELECT *)，对所有其他表的列使用明确地子集来完成的
SELECT c.*,o.order_num,o.order_date,oi.prod_id,oi.quantity,oi.item_price from customers AS c,orders AS o,orderitems AS oi WHERE c.cust_id=o.cust_id AND oi.order_num=o.order_num AND prod_id='FB';
-- 事实上，目前为止我们建立的每个内部联结都是自然联结，很可能我们永远都不会用到不是自然联结的内部联结
-- 外部联结:联结包含了那些在相关表中没有关联行的行
SELECT customers.cust_id,orders.order_num FROM customers INNER JOIN orders ON customers.cust_id=orders.cust_id;
-- 这条语句使用了关键字OUTER JOIN来指定联结的类型。但是与内部联结关联两个表中的行不同的是，外部联结还包括没有关联行的行。在使用OUTER JOIN语法时，必须使用RIGHT或LEFT关键字指定包括其所有行的表(RIGHT指出的是OUTER JOIN右边的表，而LEFT指出的是OUTER JOIN左边的表)
-- 下面的代码中使用LEFT OUTER JOIN从FROM子句的左边表中选择所有行。为了从右边的表中选择所有行，应该使用RIGHT OUTER JOIN
SELECT customers.cust_id,orders.order_num FROM customers LEFT OUTER JOIN orders ON customers.cust_id=orders.cust_id;
-- 使用带聚集函数的联结
SELECT customers.cust_name,customers.cust_id,COUNT(orders.order_num) AS num_ord FROM customers INNER JOIN orders ON customers.cust_id=orders.cust_id GROUP BY customers.cust_id;
-- 使用左外部联结来包含所有客户，甚至包含那些没有任何下订单的客户
SELECT customers.cust_name,customers.cust_id,COUNT(orders.order_num) AS num_ord FROM customers LEFT OUTER JOIN orders ON customers.cust_id=orders.cust_id GROUP BY customers.cust_id;



-- 组合查询
-- 多数SQL查询都只包含从一个或多个表返回数据的单条SELECT语句。MySQL也允许执行多个查询，并将结果作为单个查询结果集返回
-- 这些组合查询通常称为并(union)或复合查询(compound query)
-- 创建组合查询：可用UNION操作符来组合数条SQL查询。利用UNION可给出多条SELECT语句，将它们的结果组合成单个结果集
-- 使用UNION
SELECT vend_id,prod_id,prod_price FROM products WHERE prod_price<=5 UNION SELECT vend_id,prod_id,prod_price FROM products WHERE vend_id IN (1001,1002);
-- 作为参考，这里给出使用多条WHERE子句而不是使用UNION的相同查询
SELECT vend_id,prod_id,prod_price FROM products WHERE prod_price <=5 OR vend_id IN (1001,1002);
-- 包含或取消重复的行
-- UNION从查询结果集中自动去除了重复的行。在使用UNION时，重复的行被自动取消。这是UNION的默认行为，但是如果需要，可以改变它。事实上，如果想返回所有匹配行，可使用UNION ALL而不是UNION
SELECT vend_id,prod_id,prod_price FROM products WHERE prod_price <= 5 UNION ALL SELECT vend_id,prod_id,prod_price FROM products WHERE vend_id IN (1001,1002);
-- 对组合查询结果排序
-- 在用UNION组合查询时，只能使用一条ORDER BY子句，它必须出现在最后一条SELECT语句之后。对于结果集，不存在用一种方式排序一部分，而又用另一种方式排序另一部分的情况，因此不允许使用多条ORDER BY子句
SELECT vend_id,prod_id,prod_price FROM products WHERE prod_price <= 5 UNION SELECT vend_id,prod_id,prod_price FROM products WHERE vend_id IN (1001,1002) ORDER BY vend_id,prod_price;



-- 全文本搜索
-- MySQL支持几种基本的数据库引擎。并非所有的引擎都支持本书所描述的全文本搜索。两个最常使用的引擎为MyISAM和InnoDB，前者支持全文本搜索，而后者不支持。如果你的应用中需要全文本搜索功能，应该记住这一点
-- 为了进行全文本搜索，必须索引被搜索的列，而且要随着数据的改变不断地重新索引。在对表列进行适当设计后，MySQL会自动进行所有的索引和重新索引
-- 在索引之后，SELECT可与Match()和Against()一起使用以实际执行搜索
-- 启动全文本搜索支持，一般在创建表时启动全文本搜索
-- 进行全文本搜索，使用两个函数Match()和Against()执行全文本搜索，其中Match()指定被搜索的列，Against()指定要使用的搜索表达式
SELECT
	note_text 
FROM
	productnotes 
WHERE
	MATCH ( note_text ) Against ( 'anvils' );
SELECT note_text from productnotes WHERE Match(note_text) Against('anvils' WITH QUERY EXPANSION);
SELECT note_text from productnotes WHERE Match(note_text) Against('heavy -rope*' IN BOOLEAN MODE);
SELECT note_text FROM productnotes WHERE Match(note_text) Against('+rabbit +bait' IN BOOLEAN MODE);



-- 插入数据
-- 插入完整的行
INSERT INTO customers VALUES(NULL,'Pep E. LaPew','100 Main Street','Los Angeles','CA','90046','USA',NULL,NULL);
-- 插入多个行
INSERT INTO customers(cust_name,cust_address,cust_city,cust_state,cust_zip,cust_country) VALUES('Pep E. LaPew','100 Main Street','Los Angeles','CA','90046','USA'),('M. Martian','42 Galaxy Way','New York','NY','11213','USA');
SELECT * from customers;



-- 创建和操纵表
-- 创建表
create table customers
(
	cust_id int		not null auto_increment,
	cust_name char(50) not null,
	cust_address char(50) null,
	cust_city char(50) null,
	cust_state char(50) null,
	cust_zip char(50) null,
	cust_country char(50) null,
	cust_contact char(50) null,
	cust_email char(255) null,
	PRIMARY KEY (cust_id)
) ENGINE=INNODB;
create table orders
(
	order_num int not null auto_increment,
	order_state datetime not null,
	cust_id int not null,
	PRIMARY KEY (order_num)
)ENGINE=INNODB;
create table vendors
(
	vend_id	int	not null auto_increment,
	vend_name char(50)	not null,
	vend_address	char(50)	null,
	vend_city char(50)	null,
	vend_state char(5)	null,
	vend_zip	char(10)	null,
	vend_country	char(50) null,
	PRIMARY KEY (vend_id)
)ENGINE=INNODB;
-- 理解NULL，不要把NULL值与空串相混淆。NULL值是没有值，它不是空串。如果指定''(两个单引号，其间没有字符)，这在NOT NULL列中是允许的。空串是一个有效的值，它不是无值。NULL值用关键字NULL而不是空串指定
-- 主键介绍
-- 为创建由多个列组成的主键，应该以逗号分隔的列表给出各列名
create table orderitems
(
	order_num	INT	NOT	NULL,
	order_item	INT	NOT	NULL,
	prod_id	CHAR(10)	NOT	NULL,
	quantity	INT	NOT	NULL,
	item_price	DECIMAL(8,2)	NOT	NULL,
	PRIMARY	KEY (order_num,order_item)
) ENGINE=INNODB;

-- 使用AUTO_INCREMENT
-- AUTO_INCREMENT告诉MySQL，本列每当增加一行时自动增量。每次执行一个INSERT操作时，MySQL自动对该列增量，给该列赋予下一个可用的值。这样给每个行分配一个唯一的cust_id，从而可以用作主键值。
-- 每个表只允许一个AUTO_INCREMENT列，而且它必须被索引
-- 指定默认值
CREATE	TABLE	orderitems
(
	order_num	INT	NOT	NULL,
	order_item	INT	NOT	NULL,
	prod_id	CHAR(10)	NOT	NULL DEFAULT 1,
	item_price DECIMAL(8,2)	NOT	NULL,
	PRIMARY	KEY	(order_num,order_item)
) ENGINE=INNODB;

-- 引擎类型
-- InnoDB是一个可靠的事务处理引擎，它不支持全文本搜索
-- MEMORY在功能等同于MyISAM，但由于数据存储在内存(不是磁盘)中，速度很快（特别适合于临时表）
-- MyISAM是一个性能极高的引擎，它支持全文本搜索，但不支持事务处理。
-- 更新表
-- 这条语句给vendors表增加一个名为vend_phone的列，必须明确其数据类型
ALTER	TABLE	vendors	ADD	vend_phone CHAR(20);
-- 删除刚刚添加的列，可以这样做：
ALTER	TABLE	vendors	DROP	COLUMN	vend_phone;
-- ALTER TABLE的一种常见用途是定义外键
ALTER	TABLE	orderitems	ADD	CONSTRAINT fk_orderitems_orders FOREIGN	KEY	(order_num) REFERENCES	orders	(order_num);

-- 删除表
DROP TABLE customers2;
-- 重命名表
RENAME	TABLE	customers2 TO	customers;



-- 使用视图
-- 视图是虚拟的表。与包含数据的表不一样，视图只包含使用时动态检索数据的查询
SELECT
	cust_name,
	cust_contact 
FROM
	customers,
	orders,
	orderitems 
WHERE
	customers.cust_id = orders.cust_id 
	AND orderitems.order_num = orders.order_num 
	AND prod_id = 'TNT2';
-- 视图性能问题：因为视图不包含数据，所以每次使用视图时，都必须处理执行时所需的任一个检索。如果你用多个联结和过滤创建了复杂的视图或者嵌套了视图，可能会发现性能下降得很厉害。因此，在部署使用了大量视图的应用前，应当进行测试
-- 视图是数据库数据的特定子集。可以禁止所有用户访问数据表，而要求用户只能通过视图操作数据，这种方法可以保护用户和应用程序不受某些数据库修改的影响。
-- 视图是抽象的，它在使用时，从表里提取出数据，形成虚的表。不过对它的操作有很多的限制
-- 视图是永远不会自己消失的，除非手动删除它
-- 视图有时会对提高效率有帮助，一般随该数据库存放在一起，临时表永远都是在tempdb里。视图适合于多表连接浏览时使用；不适合增、删、改，这样可以提高执行效率
SELECT
	cust_name,
	cust_contact 
FROM
	productcustomers 
WHERE
	prod_id = 'TNT2';
-- 用视图重新格式化检索出的数据
SELECT	CONCAT(RTRIM(vend_name),'(',RTRIM(vend_country),')') AS	vend_title FROM	vendors	ORDER BY	vend_name;

SELECT	*	FROM	vendorlocations;

-- 用视图过滤不想要的数据
SELECT	*	FROM	customeremaillist;
-- 使用视图与计算字段
SELECT	*	FROM	orderitemsexpanded	WHERE	order_num=20005;



-- 使用存储过程
-- 存储过程就是为以后的使用而保存的一条或多条MySQL语句的集合。可将其视为批文件，虽然它们的作用不仅限于批处理
-- 存储过程通过把处理封装在容易使用的单元中，简化复杂的操作；由于不要求反复建立一系列处理步骤，这保证了数据的完整性。如果所有开发人员和应用程序都使用同一存储过程，则所使用的代码都是相同的；简化对变动的管理。如果表名、列名或业务逻辑有变化，只需要更改存储过程的代码。使用它的人员不需要知道这些变化
-- 提高性能。使用存储过程比使用单独的SQL语句快
-- 创建存储过程
-- 使用参数
DROP	PROCEDURE	productpricing;
CREATE	PROCEDURE	productpricing(OUT	p1 DECIMAL(8,2),OUT ph	DECIMAL(8,2),OUT pa DECIMAL(8,2))
BEGIN	
	SELECT	Min(prod_price)
	INTO p1
	FROM products;
	SELECT	Max(prod_price)
	INTO	ph
	FROM	products;
	SELECT	AVG(prod_price)
	INTO pa
	FROM	products;
END;
CALL productpricing(@pricelow,@pricehigh,@priceaverage);
SELECT @priceaverage;
SELECT	@pricehigh,@pricelow,@priceaverage;
DROP	PROCEDURE	ordertotal;
CREATE	PROCEDURE	ordertotal(IN	onumber INT,OUT	ototal DECIMAL(8,2))
BEGIN
	SELECT	SUM(item_price*quantity)
	FROM	orderitems
	WHERE	order_num=onumber
	INTO	ototal;
END;
CALL	ordertotal(20005,@total);
SELECT	@total;

DROP	PROCEDURE	ordertotal;

-- Name:ordertotal
-- Parameters:onumber=order number
-- 						taxable= 0 if not taxable,1 if taxable
-- 						ototal= order total variable
CREATE	PROCEDURE	ordertotal(IN	onumber INT,IN taxable BOOLEAN,OUT ototal DECIMAL(8,2)) COMMENT 'Obtain order total,optionally adding tax'
BEGIN
	-- Declare variable for total
	DECLARE	total DECIMAL(8,2);
	-- Declare tax percentage
	DECLARE	taxrate INT	DEFAULT 6;
	
	-- Get the order total
	SELECT	SUM(item_price*quantity)
	FROM orderitems
	WHERE	order_num=onumber
	INTO	total;
	
	-- Is this taxable?
	IF taxable THEN
		-- Yes,so add taxarate to the total
		SELECT	total+(total/100*taxrate) INTO	total;
	END IF;
	-- And finally,save to out variable
	SELECT	total INTO	ototal;
END;
CALL	ordertotal(20005,0,@total);
SELECT	@total;
CALL	ordertotal(20005,1,@total);
SELECT	@total;
-- 检查存储过程
SHOW	CREATE	PROCEDURE	ordertotal;



-- 使用游标
-- cursor是一个存储在MySQL服务器上的数据库查询，它不是一条SELECT语句，而是被该语句检索出来的结果集。在存储了游标之后，应用程序可以感觉需要滚动或浏览其中的数据。
-- MySQL游标只能用于存储过程
-- 创建游标
-- 为了把这些内容组织起来，下面给出我们的游标存储过程样例的更进一步修改的版本，这次对取出的数据进行某种实际的处理：
DROP	PROCEDURE	processorders;
CREATE TABLE ordertotals (order_num INT,total DECIMAL ( 8, 2 ));
CREATE PROCEDURE processorders () BEGIN-- Declare local variables
	DECLARE
		done BOOLEAN DEFAULT 0;
	DECLARE
		o INT;
	DECLARE
		t DECIMAL ( 8, 2 );-- Declare the cursor
	DECLARE
		ordernumbers CURSOR FOR SELECT
		order_num 
	FROM
		orders;-- Declare continue handler
	DECLARE
		CONTINUE HANDLER FOR SQLSTATE '02000' 
		SET done = 1;-- Create a table to store the results
	-- Open the cursor
	OPEN ordernumbers;-- Loop through all rows;
	REPEAT-- Get order number
		FETCH ordernumbers INTO o;-- Get the total for this order
		CALL ordertotal ( o, 1, t );-- Insert order and total into ordertotals
		INSERT INTO ordertotals ( order_num, total )
		VALUES
			( o, t );-- End of Loop
		UNTIL done 
	END REPEAT;
	CLOSE ordernumbers;
	
END;
SHOW TABLES;
SELECT

	* FROM
ordertotals;



-- 使用触发器
-- 触发器是MySQL响应以下任意语句而自动执行的一条MySQL语句(或位于BEGIN和END语句之间的一组语句)
-- DELETE;INSERT;UPDATE
-- 创建触发器
-- 创建触发器，需要给出4条信息
-- 唯一的触发器名；触发器关联的表；触发器应该响应的活动(DELETE、INSERT、UPDATE)；触发器何时执行
-- 触发器用CREATE TRIGGER语句创建
CREATE TRIGGER	newproduct AFTER	INSERT	ON	products FOR	EACH	ROW	SELECT	'Product added' INTO	@asd;
SELECT @asd;
DROP	TRIGGER	newproduct;
-- 使用触发器
DROP	TRIGGER	neworder;
CREATE	TRIGGER	neworder after insert on orders for each row select NEW.order_num INTO	@ee;
insert into orders(order_date,cust_id) VALUES(NOW(),10001);
SELECT	@ee;
-- DELETE触发器
CREATE	TRIGGER	deleteorder BEFORE	DELETE	ON	orders for each row
BEGIN
	INSERT	INTO	archive_prders(order_num,order_date,cust_id) values (old.order_num,old.order_date,old.cust_id);
END;
-- UPDATE触发器
CREATE	TRIGGER	updatevendor BEFORE	UPDATE	ON	vendors for each row SET	NEW.vend_state = UPPER(NEW.vend_state);





-- 管理事务处理
-- 并非所有引擎都支持事务处理。MyISAM和InnoDB是两种最常使用的引擎。前者不支持明确地事务处理管理，而后者支持。
-- 事务处理(transaction processing)可以用来维护数据库的完整性，它保证成批的MySQL操作要么完全执行，要么完全不执行
 -- 事务处理是一种机制，用来管理必须成批执行的MySQL操作，以保证数据库不包含不完整的操作结果。利用事务处理，可以保证一组操作不会中途停止，它们或者作为整体执行，或者完全不执行。如果没有错误发生，整租语句提交给数据库表。如果发生错误，则进行回退以恢复数据库到某个已知且安全的状态
 -- 控制事务处理
 -- MySQL使用下面的语句来标识事务的开始
 -- START TRANSACTION	
 SELECT	* FROM	ordertotals;
 START	TRANSACTION;
 DELETE	FROM	ordertotals;
 SELECT	* FROM	ordertotals;
 ROLLBACK;
 SELECT	* FROM	ordertotals;
 -- 使用COMMIT
 -- 一般的MySQL语句都是直接针对数据库执行和编写的。这就是所谓的隐含提交，即提交操作是自动进行的。
 -- 但是在事务处理中，提交不会隐含地进行。为进行明确地提交，使用COMMIT语句
 START	TRANSACTION;
 DELETE	FROM	orderitems	WHERE	order_num=20010;
 DELETE	FROM	orders	WHERE	order_num=20010;
 COMMIT;
 -- 使用保留点
 -- 简单的ROLLBACK和COMMIT语句就可以写入或撤销整个事务处理。但是，只是对简单的事务处理才能这样做，更复杂的事务处理可能需要部分提交或回退
 -- 为了支持回退部分事务处理，必须能在事务处理块中合适的位置放置占位符。这样如果需要回退，可以回退到某个占位符
 -- 这些占位符称为保留点。为了创建占位符，可如下使用SAVEPOINT语句
 SAVEPOINT delete1;
 -- 每个保留点都取标识它的唯一名字，以便在回退时，MySQL知道要回退到何处。为了回退到本例给出的保留点，可如下进行：
 ROLLBACK	TO	delete1;
 -- 更改默认的提交行为
 -- 默认的MySQL行为是自动提交所有更改。任何时候你执行一条MySQL语句，该语句实际上都是针对表执行的，而且所做的更改立即生效。为指示MySQL不自动提交更改，需要使用以下语句：
 SET	autocommit=0;
 -- autocommit标志决定是否自动提交更改，不管有没有COMMIT语句。设置autocommit=0指示MySQL不自动提交更改



-- 全球化和本地化
-- 字符集为字母和符号的集合；编码为某个字符集成员的内部表示；校对为规定字符如何比较的指令
-- 为查看所支持的字符集完整列表，使用以下语句：这条语句显示所有可用的字符集以及每个字符集的描述和默认校对
show CHARACTER	SET;
-- 为了查看所支持校对的完整列表，使用以下语句：
SHOW	COLLATION;
-- 为了给表指定字符集和校对，可使用带子句的CREATE TABLE
CREATE	TABLE	mytable
(
	column1 INT,
	column2 VARCHAR(10)
)DEFAULT	CHARACTER	SET	hebrew COLLATE	hebrew_general_ci;
-- 此语句创建一个包含两列的表，并且指定一个字符集和一个校对顺序
-- 除了能指定字符集和校队的表范围外，MySQL还允许对每个列设置它们，如下所示：
CREATE	TABLE	mytable
(
	column1 INT,
	column2 VARCHAR(10),
	column3 VARCHAR(10) CHARACTER	SET	latin1 COLLATE	latin1_general_ci
)DEFAULT	CHARACTER	SET	hebrew COLLATE	hebrew_general_ci;



-- 安全管理
-- 访问控制
-- MySQL用户账号和信息存储在名为mysql的MySQL数据库中。一般不需要直接访问mysql数据库和表，但有时需要直接访问。需要直接访问它的时机之一是在需要获得所有用户账号列表时。为此，可以使用以下代码：
USE	mysql;
SELECT	user from user;
-- 创建用户账号
CREATE	USER	ben IDENTIFIED	by 'p@$$w0rd';
-- 重命名一个用户账号，使用RENAME USER语句
RENAME	USER	ben TO	bforta;
-- 删除用户账号
DROP	USER	bforta;
-- 设置访问权限
SHOW	GRANTS	FOR	bforta;
-- GRANT用法
GRANT	SELECT	ON	crashcourse.* TO	bforta;
-- SHOW GRANTS反映这个更改
SHOW	GRANTS	FOR	bforta;
-- GRANT的反操作为REVOKE，撤销特定权限
REVOKE	SELECT	ON	crashcourse.* FROM	bforta;
-- 更改口令
SET	PASSWORD FOR	bforta=Password('n3w p@$$w0rd');
-- SET PASSWORD还可以用来设置你自己的口令
SET PASSWORD = Password('n3w p@$$w0rd');



-- 数据库维护
-- MySQL提供了一系列的语句，可以用来保证数据库正确和正常运行
-- ANALYZE TABLE，用来检查表键是否正确。
ANALYZE	TABLE	orders;
-- CHECK TABLE用来针对许多问题对表进行检查。在MyISAM表上还对索引进行检查。CHECK TABLE支持一系列的用于MyISAM表的方式。CHANGED检查自最后一次检查以来改动过的表
-- EXTENDED执行最后彻底的检查，FAST只检查未正常关闭的表，MEDIUM检查所有被删除的链接并进行键检验，QUICK只进行快速扫描。
CHECK	TABLE	orders,orderitems;
-- 查看日志文件
-- MySQL维护管理员依赖的一系列日志文件。主要日志文件有以下几种
-- 错误日志：它包含启动和关闭问题以及任意关键错误的细节。此日志通常名为hostname.err，位于data目录中。此日志名可用--log-error命令行选项更改
-- 查询日志：它记录所有MySQL活动，在诊断问题时非常有用。此日志文件可能会很快地变得非常大，因此不应该长期使用它。此日志通常名为hostname.log,位于data目录中。此名字可以用--log命令行选项更改
-- 二进制日志。它记录更新过数据的所有语句。此日志通常名为hostname-bin，位于data目录内。此名字可以用--log-bin命令行选项更改。注意，这个日志文件是MySQL5中添加的，以前的MySQL版本中使用的是更新日志
-- 缓慢查询日志。此日志记录执行缓慢的任何查询。这个日志在确定数据库何处需要优化很有用。此日志通常名为hostname-slow.log，位于data目录中。此名字可以用--log-slow-queries命令行选项更改
-- 在使用日志时，可用FLUSH LOGS语句来刷新和重新开始所有日志文件。



-- 改善性能
-- MySQL是用一系列的默认设置预先配置的，从这些设置开始通常是很好的。但过一段时间你可能需要调整内存分配、缓冲区大小等
-- MySQL一个多用户多线程的DBMS。它经常同时执行多个任务。如果这些任务中的某一个执行缓慢，则所有请求都会执行缓慢。如果你遇到显著的性能不良，可以使用SHOW PROCESSLIST显示所有活动进程。
-- 总是有不止一种方法编写同一条SELECT语句。应该试验联结、并、子查询等，找出最佳方法
-- 使用EXPLAIN语句让MySQL解释它将如何执行一条SELECT语句
-- 一般来说，存储过程执行得比一条一条地执行其中的各条MySQL语句快
-- 必须索引数据库表以改善数据检索的功能。确定索引什么不是一件微不足道的任务，需要分析使用的SELECT语句以找出重复的WHERE和ORDER BY子句
-- 索引改善数据检索的功能，但是损害数据插入、删除和更新的性能。如果你有一些表，它们手机数据且不经常被搜索，则在有必要之前不要索引它们。
-- LIKE很慢。一般来说，最好是使用FULLTEXT而不是LIKE



