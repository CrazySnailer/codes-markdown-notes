###Linux常用命令


###linux强制删除目录命令rm -rf 


```

rm -rf 目录名字
-r 就是向下递归，不管有多少级目录，一并删除
-f 就是直接强行删除，不作任何提示的意思
```

删除文件夹实例：
```
    #rm -rf /opt/real/RealPlayer
```

将会删除/opt/real/RealPlayer目录以及其下所有文件、文件夹

需要提醒的是：使用这个rm -rf的时候一定要格外小心，linux没有回收站的
