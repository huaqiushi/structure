Redis
==========

在Python中使用redis
-----------------------
Python的第三方模块redis提供了两个类：StrictRedis和Redis。前者用于实现大部分官方的命令，后者是前者的子类，用于向后兼容旧版本的redis

使用Redis类操作redis
'''''''''''''''''''''''

.. code-block:: py

    import redis
    r = redis.Redis(host='127.0.0.1', port=6379, db=0)
    r.set('age', '25')

使用StrictRedis类操作redis
'''''''''''''''''''''''''''''

.. code-block:: py

    import redis
    r = redis.StrictRedis(host='127.0.0.1', port=6379)
    pipe = r.pipeline(transaction=False)
    pipe.set('age', '25')
    pipe.set('sex', 'male')
    pipe.execute()

连接池
''''''''''
用来实现多个Redis实例共享一个连接。避免每次都建立、释放连接

.. code-block:: py

    import redis
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)
    r = redis.Redis(connection_pool=pool)
    r.set('age', '25')


五种数据类型
---------------

String： { key: value }
'''''''''''''''''''''''''''
- set(key, value, ex=None, px=None, nx=False, xx=False)：设置key的value（若key不存在则创建、存在则修改）

    - ex 过期时间，单位为秒
    - px 过期时间，单位为毫秒
    - nx 若设置为True，则只有key不存在时才执行当前set操作
    - xx 若设置为True，则只有key存在时才执行当前set操作

- mset(*args, **kwargs)：批量设置值
- get(key)：获取值
- mget(keys, *args)：批量获取值
- getset(key, value)：设置新值并获取原来的值
- getrange(key, start, end)：根据字节获取子序列（从第start个字节开始到第end个字节结束）
- setrange(key, offset, value)：从第offset个字节向后，替换为value
- incr(self, key, amount=1)：自增key对应的值。当key不存在时，创建key=amount；若存在，则自增amount
- append(key, value)：在key的值后追加value

Hash： { key: {field: value, field: value, …} }
'''''''''''''''''''''''''''''''''''''''''''''''''''
- hset(key, field, value)：向key对应的hash中添加一个field。不存在创建，存在则修改
- hsetnx(key, field, value)：向key对应的hash中添加一个field。不存在创建。
- hmset(key, mapping)：向key对应的hash中添加多个field
- hget(key, field)
- hmget(key, field, field, …)
- hkeys(key)
- hvals(key)
- hexists(key, field)
- hincrby(key, field, amount=1)
- hscan(key, cursor=0, match=None, count=None)：增量式迭代获取。用于大数据量时分批获取值

List： { key: [value, value, …] }
''''''''''''''''''''''''''''''''''
- rpush(key, value, value, …)：向列表的右边追加value。若key存在则追加，不存在则创建并追加
- rpushx(key, value)：向列表的右边追加value。若key存在则追加
- rpop(key)：在列表的右边弹出一个元素
- lpush/lpushx/lpop

Set： { key: [menber, member, …] } （member不允许重复）
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''
- sadd(key, menber, member, …)
- scard(key)
- spop(key)

Sort Set： 有序的set
'''''''''''''''''''''''
- zadd(key, score, member, score, member, …)


对于不同数据类型通用的操作
---------------------------

- delete(key, key, …)
- exists(key)
- keys(pattern=’*’)
- expire(key, time)
- move(key, db)：将key移动到指定db下


在django中使用redis缓存
----------------------------
1. 安装django-redis
2. 在setting.py中增加

.. code-block:: py

    CACHES = {
        "default": {
            "BACKEND": "django_redis.cache.RedisCache",
            "LOCATION": "redis://127.0.0.1:6379/1",
            "OPTIONS": {
                "CLIENT_CLASS": "django_redis.client.DefaultClient",
            }
        }
    }
    SESSION_ENGINE = "django.contrib.sessions.backends.cache"
    SESSION_CACHE_ALIAS = "default"

3. 在views.py中

.. code-block:: py

    from django.core.cache import cache
    cache.set('key', '123')
    cache.get('key')


进程间通信
--------------
