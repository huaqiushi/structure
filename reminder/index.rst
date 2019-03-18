备忘录
=========

- 18-12-01

    - linux：scp命令。远程服务器和本地互传文件：scp [参数] 源文件 目标文件

        - 远程：qiushi@192.168.20.68
        - 本地：huaqiushi@ubuntu:~/PycharmProjects$

        1. 将本地文件传送到远程：在本地命令行里：scp /home/huaqiushi qiushi@192.168.20.68:/home/qiushi
        2. 将远程文件传送到本地：在本地命令行里：scp qiushi@192.168.20.68:/home/qiushi /home/huaqiushi

- 18-12-26

    - 网络：IP。虚拟机的IP、物理机的IP？登录阿里云时显示的本机IP（222.65.184.65）源自哪里？

        - 对于公司目前的网络组成而言，物理机处在局域网中，其IP由外网主机通过DHCP协议动态分配；虚拟机处在物理机中，其IP由物理主机通过DHCP协议动态分配
        - 无论是物理机还是虚拟机访问外网服务器，其IP都会被标记为给其分配IP的那个外网主机的IP（物理机和虚拟机登录阿里云时显示的IP是一样的），也就是说，IP之间的互访只存在于外网中

    - 网络：网络组成。端口、外网、内网、子网、常见的网络组成

        - 局域网地址：10.0.0.21, 192.168.91.1, 192.168.237.1
        - 保留地址：169.254.14.9, 169.254.79.117
        - 待续

    - 网络：网卡。网卡、DHCP协议、虚拟机的三种网卡（bridged、NAT、Host-only）

        - 待续

- 19-03-12

    - linux：service命令。redis为什么不能用service命令启动？（用redis-server /etc/redis/redis.conf可以启动）

        - 应用在注册成为系统服务（在/etc/init.d/中有shell脚本）后，才能使用service命令进行管理
        - 注：使用apt-get安装的应用会自动注册为系统服务
        - 注：service nginx status 与 /etc/init.d/nginx status等价

    - linux：find命令

- 19-03-13

    - linux：彻底删除nginx并重装

        1. sudo apt-get --purge remove nginx  移除包和配置文件
        2. sudo apt-get autoremove  自动移除无用的包
        3. sudo apt-get update  更新包列表
        4. sudo apt-get upgrade  升级包（在升级之前必须更新包列表）
        5. sudo apt-get install nginx  安装包

- 19-03-14

    - linux：创建符号链接。配置nginx时，在/etc/nginx/site-available/中创建配置文件，在/etc/nginx/site-enabled/中对要启用的配置文件创建符号链接

        1. 进入到要创建符号链接的文件夹下
        2. sudo ln -s  指向的源文件地址  符号链接的名称

    - linux：用户组和权限

- 19-03-18

    - 后续强化：
        1. 数据库：mysql, redis
        2. 完整项目：库存管理系统、独立站
