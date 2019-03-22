django
===========

.. contents:: 目录

ORM
-------

聚合
''''''''''
django提供了五种聚合：Avg, Max, Min, Sum, Count；两种生成聚合的方法：aggregate, annotate

================  ========================  ===============  ==================
生成聚合的方法      进行聚合的对象               返回值            是否是终结子句
================  ========================  ===============  ==================
aggregate         整个查询结果集               一个字典          是
annotate          查询结果集里的每个对象        查询结果集         否
================  ========================  ===============  ==================

- 注：annotate会生成新的字段“注释”到每一个对象上

aggregate
^^^^^^^^^^^^^

.. code-block:: py

    Book.objects.aggregate(Avg('price'))   # {'price__avg': 11.99}

annotate
^^^^^^^^^^^^^

.. code-block:: py

    """annotate的用法有两种"""

    # 第一种：直接使用
    Book.objects.annotate(Count('authors'))  # 'authors'为Book中的引用字段

    # 第二种：基于values使用（此时values的作用是分组）
    Case.objects.values('currency').annotate(Sum('amount'))



处理HTTP请求
----------------

中间件
''''''''''


表单类
---------


类视图
---------

基本类视图
'''''''''''''
View

通用类视图
'''''''''''''
通用类视图均继承自View

- ListView
- FormView
- TemplateView
- RedirectView

对基本类视图的拓展
'''''''''''''''''''
1. mixin：基于一个通用类视图进行混入
2. 装饰类视图

    - 装饰类视图的dispatch方法

    .. code-block:: py

        from django.contrib.auth.decorators import login_required
        from django.utils.decorators import method_decorator
        from django.views.generic import TemplateView

        class ProtectedView(TemplateView):
            template_name = 'secret.html'

            @method_decorator(login_required)
            def dispatch(self, *args, **kwargs):
                return super(ProtectedView, self).dispatch(*args, **kwargs)


    - 直接装饰类视图

    .. code-block:: py

        from django.contrib.auth.decorators import login_required
        from django.utils.decorators import method_decorator
        from django.views.generic import TemplateView

        @method_decorator(login_required, name='dispatch')
        class ProtectedView(TemplateView):
            template_name = 'secret.html'


管理文件
-------------
管理静态文件
''''''''''''''
在模板中，使用static标签生成静态文件的访问路径

- STATIC_URL：静态文件访问路径。模板中加载静态文件时，通过此路径访问到STATICFILES_DIRS
- STATICFILES_DIRS：静态文件存储路径（在collectstatic后，这里面的文件会被收集到STATIC_ROOT中）

.. code-block:: py

    STATIC_URL = '/static/'  # http://127.0.0.1:9999/static/

    STATICFILES_DIRS = [
        os.path.join(BASE_DIR, 'static'),  # /home/huaqiushi/Desktop/UniversalPlugin/static
        '/var/www/static/',
    ]


管理用户上传的文件
''''''''''''''''''
在模板中，使用<input type="file">接收用户上传的文件（在Model中，使用FileField或ImageField定义的字段（是一个File对象）存储用户上传的文件）

- MEDIA_URL：用户文件访问路径
- MEDIA_ROOT：用户文件存储路径


用户认证和授权
-----------------


缓存
---------


加密签名
------------
将字符串或者复杂数据类型转变为无意义的字符串（默认使用settings中的SECRET_KEY生成签名）

- 两个常见的使用场景：生成“重置密码”的URL；生成一个只可以访问一次的URL（例如：用户下载付费文件时）


日志
--------


安全
-------
