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
