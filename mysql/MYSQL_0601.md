# 查看数据





```mysql
SHOW COLUMNS FROM [table];
# 快捷方式：DESCRIBE [table];
```



```mysql
SHOW STATUS; # 显示服务器状态信息
SHOW CREATE TABLE BASE and SHOW CREATE TABLE;
# 分别用来显示创建特定数据库或表
SHOW GRANTS; # 显示授予用户的安全权限(所有用户)
SHOW ERRORS/WARNINGS；# 显示服务器错误或警告消息
```



# 检索数据



```mysql
SELECT A, B , E FROM table; # 检索多个列
SELECT * FROM table; # 所有列
SELECT DISTINCT column FROM table; # 返回不同值(唯一)
```



```mysql
# 限制结果
SELECT columns FROM some_table LIMIT 5; # 限制结果为5行
SELECT columns FROM some_table LIMIT 5,5; # 返回从行5开始的5行，第一个数为开始位置，第二个数为要检索的行
# 带一个值的LIMIT总是从第一行开始检索，给出的数为返回的行数。带两个值的LIMIT可以指定从行号为第一个值的位置开始

LIMIT 4 OFFSET 3; # 替代写法,作用相同
```

##当检索的行数大于表的行数时，mysql将返回它所能返回的最大行数



```mysql
# 使用完全限定的表名
SELECT table.columns FROM database.table;

```



排序检索数据

```mysql
SELECT prod_id,prod_price,prod_name
FROM products 
ORDER BY prod_price,prod_name;
# 对表的prod_id行进行排序(如果price,name有重复的行)
# 默认排序为字母A-Z顺序
# DESC 为降序 SELECT columns FROM table ORDER BY columns DESC;

# 指定多个排序
SELECT con1,con2,con3 
FROM table1
ORDER BY con2 DESC,con3;
# 对con2进行降序排序，然后con3仍然升序排序(升序关键字为ASC)

```





# 过滤数据



```mysql
SELECT column1 
FROM table1
where column1 = 4;

# 在与order by同时使用时where应该位于order by之前，否则会发生错误
```

where 的操作符

除了BETWEEN之外其他的操作符都与基本数学运算操作符相同，使用between时必须加and关键字

```mysql
SELECT prod_name, prod_price
FROM products
WHERE prod_price BETWEEN 5 AND 10;
```



空值检查

```mysql
SELECT prod_name
FROM products
WHERE prod_price IS NULL;
# 返回包含空值的所有行

```

















