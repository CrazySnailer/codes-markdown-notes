###Linux下查看文件和文件夹大小

当磁盘大小超过标准时会有报警提示，这时如果掌握df和du命令是非常明智的选择。

    df可以查看一级文件夹大小、使用比例、档案系统及其挂入点，但对文件却无能为力。
    du可以查看文件及文件夹的大小。

    两者配合使用，非常有效。比如用df查看哪个一级目录过大，然后用df查看文件夹或文件的大小，如此便可迅速确定症结。

    下面分别简要介绍

    df命令可以显示目前所有文件系统的可用空间及使用情形，请看下列这个例子：
    
```    
[yayug@yayu ~]$ df -h
Filesystem            Size  Used Avail Use% Mounted on
/dev/sda1             3.9G  300M  3.4G   8% /
/dev/sda7             100G  188M   95G   1% /data0
/dev/sdb1             133G   80G   47G  64% /data1
/dev/sda6             7.8G  218M  7.2G   3% /var
/dev/sda5             7.8G  166M  7.2G   3% /tmp
/dev/sda3             9.7G  2.5G  6.8G  27% /usr
tmpfs                 2.0G     0  2.0G   0% /dev/shm
```

```
[root@bsso yayu]# du -h --max-depth=1 work/testing
27M     work/testing/logs
35M     work/testing

[root@bsso yayu]# du -h --max-depth=1 work/testing/*
8.0K    work/testing/func.php
27M     work/testing/logs
8.1M    work/testing/nohup.out
8.0K    work/testing/testing_c.php
12K     work/testing/testing_func_reg.php
8.0K    work/testing/testing_get.php
8.0K    work/testing/testing_g.php
8.0K    work/testing/var.php
```

```
[root@bsso yayu]# du -h --max-depth=1 work/testing/logs/
27M     work/testing/logs/

[root@bsso yayu]# du -h --max-depth=1 work/testing/logs/*
24K     work/testing/logs/errdate.log_show.log
8.0K    work/testing/logs/pertime_show.log
27M     work/testing/logs/show.log

```

###参考

http://www.cnblogs.com/benio/archive/2010/10/13/1849946.html
