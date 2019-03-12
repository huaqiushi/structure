celery
==========
一个用于异步或定时任务的分布式任务队列（是Python的一个第三方库）。由producer, beat, broker, worker和backend组成（关于broker，官方推荐选择rabbitmq）

使用
-------
1. 创建Celery实例（定义broker和backend）
2. 创建task（将其纳入celery管理）
3. 在视图中调用task
