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
