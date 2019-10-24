django REST
==============

.. contents:: 目录

表现层状态转移：在网络上，一切皆资源，一个URI指向一个资源（表现层）；资源有多种表现形式（状态）；使用HTTP动词对资源进行CRUD（转移）

- 注：资源必须是名词。可以是一个实体，也可以是一种服务
- HATEOAS：在响应内容中给出下一步可以访问的url，使得用户只需记住一个url便可以发现其它url

序列化
---------------
序列化：将对象转换为一定格式的字节串（数据在网络之间以字节串的形式传输）

django中的serializer
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: py

  from django.core import serializers
  from user.models import Seller

  # 序列化
  queryset = Seller.objects.all()  # <QuerySet [<Seller: Seller object>, <Seller: Seller object>, ...]>
  data = serializers.serialize('json', queryset)

  # 反序列化
  for deserialized_object in serializers.deserialize("json", data):
      do_something_with(obj)
      if object_should_be_saved(deserialized_object):
          deserialized_object.save()

.. py:function:: serialize(format, queryset, **options):

    Serialize a queryset (or any iterator that returns database objects) using
    a certain serializer; format can be 'json', 'xml' or 'yaml'

- 注：结构化数据格式：json、xml、yaml；文本标记语言：sphinx、markdown

django REST中的Serializer
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

和django中的Form类的用途一样，都是将后端数据（model类）转换为前端数据（HTML、JSON）；用法也一样

- Serializer

  - 定义序列化字段
  - 实现create()和update()方法

- ModelSerializer

  - 只需指出要序列化的字段
  - 默认实现create()和update()方法


视图
------------

APIView
^^^^^^^^^^^^^
类视图，继承自django中的View，是django REST中提供的基本视图类

GenericAPIView
^^^^^^^^^^^^^^^^^^^^^^
类视图，继承自APIView

- 注：mixins：在GenericAPIView的基础上混入ListModelMixin/RetrieveModelMixin/CreateModelMixin/UpdateModelMixin/DestroyModelMixin

ViewSet
^^^^^^^^^^^^^^^
本质上是一种类视图，但是它不像类视图，提供get()、post()之类的method handlers，而是提供list(),retrieve(),create(),destroy()之类的 **actions**。

====================  ================  ====================================================  ======================================
      ViewSet             继承自                          提供的actions                                         备注
====================  ================  ====================================================  ======================================
ViewSet               APIView            无（需要定义actions）
GenericViewSet        GenericAPIView     无（需要添加mixin或者定义actions）
ModelViewSet          GenericAPIView     list/retrieve/create/update/partial_update/destroy   必须定义queryset,serializer_class属性
ReadOnlyModelViewSet  GenericAPIView     list/retrieve                                        必须定义queryset,serializer_class属性
====================  ================  ====================================================  ======================================

- 注：标准的actions：list/retrieve/create/update/partial_update/destroy；另外的actions——使用 **@action** 装饰器
- 注：自定义ViewSet：继承自GenericViewSet，然后添加mixin（必须定义queryset,serializer_class属性）
- 注：router：配合ViewSet使用，其会将请求分发给ViewSet中的某个action去处理
