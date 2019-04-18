~~~shell
一、mysql中的编码

mysql> show variables like 'collation_%';  
mysql> show variables like 'character_set_%';
  
缺省是latin1编码，会导致中文乱码。
修改库的编码：
mysql> alter database db_name character set utf8;
修改表的编码：
mysql> ALTER TABLE table_name CONVERT TO CHARACTER SET utf8 COLLATE utf8_general_ci; 

可以在mysql中设置编码，单个设置 
mysql> set character_set_connection=utf8;
mysql> set character_set_database=utf8;
mysql> set character_set_results=utf8;
mysql> set character_set_server=utf8;
但重启后会失效。

可以修改配置文件：

[root@Hadoop48 ~]# vi /etc/my.cnf  
[mysql]  
default-character-set=utf8  
[client]  
default-character-set=utf8  
[mysqld]  
default-character-set=utf8  
character_set_server=utf8  
init_connect='SET NAMES utf8' 
重启mysql，这样确保缺省编码是utf8



连接命令
?useUnicode=true&characterEncoding=UTF-8
~~~

