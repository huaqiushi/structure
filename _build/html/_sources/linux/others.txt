其它
=======

文件系统
-----------
FHS（Filesystem Hierarchy Standard）
'''''''''''''''''''''''''''''''''''''''
- /bin：对于操作系统而言，必要的可执行程序（如：ls, cat）
    - 注：bin为binary的缩写，sbin中的s为superuser的缩写

- /etc：配置文件
    - 注：etc为Editable Text Configuration的缩写

- /usr：用户文件
    - /usr/bin：对于操作系统而言，非必要的可执行程序（如：python, mysql）
    - /usr/share：静态文件

- /var：在正常运行的系统中其内容不断变化的文件
    - /var/log：日志文件
    - /var/lib/：程序在运行时维护的持久性数据。例如：数据库的系统元数据

文件名的颜色
'''''''''''''''
- 蓝色：文件夹（带有绿色阴影的是获得最高权限的文件夹）
- 浅蓝色：链接文件
- 白色：普通文件
- 绿色：可执行文件
- 红色：压缩文件
- 黄色：设备文件

权限管理
'''''''''''


软件包的安装与管理
-------------------
安装软件包
'''''''''''''''''''''''''''
1. APT安装（Advanced Package Tool）
    - apt-get是Debian Linux系统的包管理工具

2. 源码安装
    - 下载源文件：wget
    - 解压
    - 编译：make
    - 安装：sudo make install

环境变量
-----------
1. os.environ
PATH /home/huaqiushi/bin:/home/huaqiushi/.local/bin:/usr/local/sbin:/usr/

命令
-------
- dpkg -l --显示已安装软件包列表
