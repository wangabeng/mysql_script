# mysql_script
mysql脚本  

创建表  
```
CREATE TABLE IF NOT EXISTS `user`(
  id INT AUTO_INCREMENT PRIMARY KEY,
  account_id VARCHAR(100),
  name VARCHAR(50),
  token CHAR(36),
  gmt_create BIGINT,
  gmt_modified BIGINT
);
```
# mysql中怎样把购物车的多个商品放到同一个订单里
外键关联就可以了。简单地说，比如这么设计：  

t_order 表为订单信息表，其中包含了订单创建者、创建时间、状态等，主键为订单号，但不包含商品的任何信息  

t_order_item 表为订单详细表，其中记录着购买的商品id、数量、规格等，通过订单号字段与t_order的主键做外键关联，买了多少种商品就新增多少条记录  

# mysql数据库默认排序问题
mysql官方回答：
对于innodb引擎表来说，在相同的情况下，select 不带order by，会根据主键来排序，从小到大   
  
SELECT * FROM tbl -- this will do a "table scan". If the table has never had any DELETEs/REPLACEs/UPDATEs, the records will happen to be in the insertion order, hence what you observed.  
大致意思为，一个myisam引擎表在没有任何的删除，修改操作下，执行 select 不带order by，那么会按照插入顺序进行排序。  
  
If you had done the same statement with an InnoDB table, they would have been delivered in PRIMARY KEY order, not INSERT order. Again, this is an artifact of the underlying implementation, not something to depend on.
对于innodb引擎表来说，在相同的情况下，select 不带order by，会根据主键来排序，从小到大  

# 查询当前记录上一条与下一条记录的原理：
上一条的sql语句，从table表里按从大到小的顺序（正序ASC）选择一条比当前ID小的记录。  
下一条的sql语句，从news表里按从小到大的顺序（倒序DESC）选择一条比当前ID大的新闻。  
其中ID为表table的主键   
```
方式一：
	上一条：
	select * from table where id = (select id from table where id < {$id} order by id desc limit 1); 
	下一条：
	select * from table where id = (select id from table where id > {$id} order by id asc limit 1);
方式二：
	上一条：
 	select * from table where id = (select MAX( id) from table where id < {$id} ); 
 	下一条：
 	select * from table where id = (select  MIN( id)  from table where id > {$id} );
```
