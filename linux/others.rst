其它
=======

文件系统
-----------
FHS(Filesystem Hierarchy Standard)
'''''''''''''''''''''''''''''''''''''''
- /bin：必要的可执行程序（如：ls, cat）
    - 注：bin为binary的缩写，sbin中的s为superuser的缩写

- /etc：(Editable Text Configuration)配置文件

- /usr：用户文件
    - /usr/bin：非必要的可执行程序（如：python, mysql）
    - /usr/share：静态文件

- /var：在正常运行的系统中其内容不断变化的文件
    - /var/log：日志文件
    - /var/lib/：程序在运行时维护的持久性数据。例如：数据库的系统元数据

权限管理
'''''''''''



软件包的安装与管理
-------------------
几种常用的安装软件包的方法
'''''''''''''''''''''''''''
1. apt-get install
    apt-get是Debian Linux系统的包管理工具
2.


环境变量
-----------
1. os.environ
PATH /home/huaqiushi/bin:/home/huaqiushi/.local/bin:/usr/local/sbin:/usr/

命令
-------
- dpkg -l --显示已安装软件包列表
-
