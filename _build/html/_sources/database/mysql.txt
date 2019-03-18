Mysql
=========

其它
--------

远程连接mysql
''''''''''''''''''
mysql默认只有本地主机可以访问，远程连接步骤如下

1. 取消访问限制。将/etc/mysql/my.cnf（或者/etc/mysql/mysql.conf.d/mysqld.cnf）中的bind-address = 127.0.0.1注销
2. 重启mysql
3. 给予远程主机权限

.. code-block:: mysql

    mysql> use mysql
    mysql> grant all privileges on *.* to 'root'@'101.80.250.153' identified by '123';
    mysql> FLUSH PRIVILEGES;

    # 第一个*是数据库，可以改成允许访问的数据库名称
    # 第二个*是数据库的表名称，*代表允许访问任意的表
    # root代表远程登录使用的用户名，可以自定义
    # 101.80.250.153为要连接的远程主机
    # 123为远程登录时使用的密码，可以自定义
