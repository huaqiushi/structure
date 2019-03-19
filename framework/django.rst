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
ListView
TemplateView
RedirectView

mixins
''''''''''''


管理文件
-------------
管理静态文件
''''''''''''''

管理用户上传的文件
''''''''''''''''''
在Model中，使用FileField或ImageField定义的字段存储了用户上传的文件（这个字段是一个File对象）
- MEDIA_ROOT：存储路径
- MEDIA_URL：访问路径


用户认证
-------------


缓存
---------


加密签名
------------


日志
--------


安全
-------

