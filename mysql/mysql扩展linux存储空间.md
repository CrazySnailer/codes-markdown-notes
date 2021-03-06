###mysql扩展linux存储空间（InnoDB数据文件管理）



如果你使用InnoDB存储引擎，那么InnoDB数据文件管理将是你要面临的一个问题，

下面介绍如何正确的添加、删除数据文件以及添加数据文件时常见问题解决。

###  添加InnoDB数据文件

了解了InnoDB表空间的配置方法后，我们来尝试增加表空间的数据文件，在通常情况下，我们会遇到一个问题就是一个表空间的某个数据文件所在的磁盘空间磁盘紧张，这时需要为表空间增加一个新位置的新数据文件，同时关闭原来数据文件的自动扩展，这样才能保证不会因为磁盘满导致MySQL出现问题。

举例：
```

innodb_data_home_dir =

innodb_data_file_path = /ibdata/ibdata1:10M:autoextend
```

假设/ibdata/下可用空间为1G ,这个数据文件过一段时间已经长到988MB。这必须添加一个新位置的新数据文件，来保证充裕的表空间，下面是添加一个可扩展数据文件之后的配置行：

```
innodb_data_home_dir =

innodb_data_file_path = /ibdata/ibdata1:988M;/disk2/ibdata2:50M:autoextend
```

添加完成后，重启MySQL服务，这时会停止对/ibdata/ibdata1数据文件的扩展，并创建新的数据文件/disk2/ibdata2。

MySQL重启时会看到如下日志：

--日志内容--
```

080909 19:09:26  InnoDB: Data file /disk2/ibdata2 did not exist: new to be created

080909 19:09:26  InnoDB: Setting file /disk2/ibdata2 size to 50 MB

InnoDB: Database physically writes the file full: wait...
```

另外，很多网友在增加表空间的数据文件时通常会遇到下面的问题，导致MySQL无法启动或启动后无法正常工作。

现象: 在MySQL日志中出现如下提示
```

080909 19:07:12  mysqld started

InnoDB: Error: data file /ibdata/ibdata1 is of a different size

InnoDB: 63872 pages (rounded down to MB)

InnoDB: than specified in the .cnf file 63872 pages!

InnoDB: Could not open or create data files.
```

出现上述问题的主要原因是“innodb_data_file_path = /ibdata/ibdata1:900M”中数据文件大小指定不正确，这里给出了一个计算公式可以解决网友的这个问题

计算公式：

```
64pages相当于1M
     63872/64=988M
     
```

所以，设置为 innodb_data_file_path = /ibdata/ibdata1: 988M 就可以避免上述错误出现。


Ubuntu就开始使用一种安全软件叫做AppArmor，这个安全软件会在你的文件系统中创建一个允许应用程序访问的区域（专业术语：应 用程序访问控制）。如果不为MySQL修改AppArmor配置文件，永远也无法为新设置的数据库存储位置启动数据库服务。

###配置AppArmor
```
$sudo vi /etc/apparmor.d/usr.sbin.mysqld 
```
添加上下面内容
```
/disk2/ r,
/disk2/** rwk,
```
###保存后退出，执行命令
```
$sudo /etc/init.d/apparmor reload
```
###给/home/mysql文件添加root权限
```
sudo chmod -（代表类型）×××（所有者）×××（组用户）×××（其他用户）

sudo chown -R mysql:mysql /disk2/


```

###重启MySQL服务
```
$sudo /etc/init.d/mysql start
```

###注意
* 整个操作不能在root用户下,只能在其他用户下，因为root用户设置的权限，其他用户用不了
* 数据库新位置需要绝对路径，不能做软链接
* 数据文件夹的用户组为mysql，mysql的根目录权限需要为root权限
