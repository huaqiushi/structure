备忘录
=========

- 2019-03-12

    - linux：service命令。redis为什么不能用service命令启动？（用redis-server /etc/redis/redis.conf可以启动）

        - 应用在注册成为系统服务（在/etc/init.d/中有shell脚本）后，才能使用service命令进行管理
        - 注：使用apt-get安装的应用会自动注册为系统服务

    - linux：find命令

- 2019-03-13

    - 彻底删除nginx并重装

        1. sudo apt-get --purge remove nginx  移除包和配置文件
        2. sudo apt-get autoremove  自动移除无用的包
        3. sudo apt-get update  更新包列表
        4. sudo apt-get upgrade  升级包（在升级之前必须更新包列表）
        5. sudo apt-get install nginx  安装包

    -