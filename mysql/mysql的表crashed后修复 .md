###mysql的表crashed后修复


mysql的表在大量访问和写入环境下有可能损坏，报错如下：

```
    ERROR 144 (HY000): Table './snort/acid_event' is marked as crashed and last (automatic?) repair failed
```

解决办法是用myisamchk命令进行修复。
在ubuntu8.10中，mysql的数据存放的路径在/var/lib/mysql(我的是/home/mysql),假如有个数据库叫twittercrawler，twittercrawler中有个表tweet_info损坏了,
那么在/var/lib/mysql/twittercrawler/下有个文件叫tweet_info.MYI,修复办法是

```
    cd /var/lib/mysql/twittercrawler/
    myisamchk -c -r tweet_info.MYI
```

错误产生原因，有人说是频繁查询和更新表造成的索引错误。还有说法为是MYSQL数据库因为某种原因而受到了损坏，
如：数据库服务器突发性的断电、在提在数据库表提供服务时对表的原文件进行某种操作都有可 
能导致MYSQL数据库表被损坏而无法读取数据。总之就是因为某些不可测的问题造成表的损坏。


###备注

要进入数据库表目录，要在root权限下操作。
上述方法不好用时可以按照提示进行恢复操作。例如 myisamchk -o -f tweet_info.MYI


###另外一种方式
MySQL数据库出错:Table ... is marked as crashed and should be repaired

用“REPAIR TABLE table_name;”命令修复

登录mysql进入报错的数据库

```
mysql> use twittercrawler;
Database changed

mysql> repair table tweet_info;
```
