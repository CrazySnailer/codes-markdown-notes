###怎样用命令查看Mysql数据库大小？ 

###1、进去指定schema 数据库（存放了其他的数据库的信息）
```    
use information_schema
```
###2、查询所有数据的大小
```  	
select concat(round(sum(DATA_LENGTH/1024/1024),2), 'MB') as data from TABLES
```
###3、查看指定数据库的大小
比如说 数据库apoyl

```  	
select concat(round(sum(DATA_LENGTH/1024/1024),2), 'MB') as data from TABLES where table_schema= 'apoyl' ;
```
###4、查看指定数据库的表的大小

比如说 数据库apoyl 中apoyl_test表
```  	
select concat(round(sum (DATA_LENGTH/1024/1024),2), 'MB') as
data from TABLES where table_schema= 'apoyl' and table_name= 'apoyl_test' ;
```
