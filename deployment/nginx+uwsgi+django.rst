nginx+uwsgi+django
=======================

nginx
---------

uWSGI
----------

uWSGI是一个实现了WSGI协议、uwsgi协议、http协议的网关服务器。其会创建Unix套接字，通过uwsgi协议处理从web server传来的客户端的http请求，通过WSGI协议调用执行相应的django应用程序。

- WSGI：是一种通信协议，用于接收从web server传来的客户端的http请求，然后调用执行相应的django应用程序。总之，它用于规范web server与web application的通信
- uwsgi：是一种线路协议，用于规范uWSGI服务器与其它网络服务器的通信（是uWSGI服务器自有的协议）

    - 从前端到后端：the web client <--http--> the web server <--unix socket--> the uWSGI <----> Django application

nginx+uwsgi+django
------------------------

- nginx：处理静态文件；提高并发处理量；对多台uWSGI进行负载均衡；提高安全性
- uwsgi：web服务器和web程序之间的一种简单通用的接口，用于将HTTP协议转换为Python可以直接使用的WSGI协议。其包含的wsgi协议使得遵从此协议的web程序可以运行在任何web服务器上；uwsgi协议定义了传输信息的类型

从客户端发起请求到客户端收到响应的完整流程
    1. 浏览器请求
    2. nginx解包分析。如果是静态文件请求就根据nginx配置的静态文件目录返回请求的资源；如果是动态的请求，nginx通过配置文件将请求传递给uWSGI
    3. uWSGI 将接收到的包进行处理，并转发给wsgi
    4. wsgi根据请求调用django的某个view，view处理完后将返回值交给wsgi
    5. wsgi将返回值进行打包，转发给uWSGI，uWSGI接收后转发给nginx，nginx最终将返回值返回给浏览器

    - 注：不同的组件之间传递信息涉及到数据格式和协议的转换

部署步骤
''''''''''

1. 安装nginx、uwsgi
2. 写配置文件
	- uwsgi配置文件：

        .. code-block:: ini

            [uwsgi]
            chdir = /home/huaqiushi/run/running/  # 指向项目地址
            wsgi-file = running/wsgi.py  # 指向项目中的wsgi.py
            daemonize = /home/huaqiushi/run/running/uwsgi.log
            socket = 127.0.0.1:8001  # 用8001端口接收socket请求（此处若将socket改成http则可直接用uwsgi接收http请求）
            stats = 127.0.0.1:9090  # 状态发送至9090窗口
            processes = 4  # 最大进程是4
            threads = 2  # 最大线程是2
            master = true  # 启动主进程

	- nginx配置文件：

        https://blog.csdn.net/shu_8708/article/details/79031328


3. 启动uwsgi（路径切换到项目文件夹下）
	- uwsgi –http 127.0.0.1:8008 –wsgi-file test.py  启动uwsgi加载单个文件
	- uwsgi –http 127.0.0.1:8008 –module proj.wsgi  启动uwsgi加载django项目
	- uwsgi –ini uwsgi.ini  启动uwsgi加载django项目（用uwsgi配置文件启动）

- django中静态文件（css、js、img）的管理：python manage.py collectstatic——将所有应用的static文件夹中的静态文件拷贝到项目的static文件夹（即STATIC_ROOT）中
