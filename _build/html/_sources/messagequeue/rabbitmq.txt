RabbitMQ
=============

将消息通过队列分发给消费者

分发方式
-----------
round-robin dispatching
''''''''''''''''''''''''''''
默认的分发方式。有多个消费者时，RabbitMQ将消息循环分发给每个消费者
fair dispatch
''''''''''''''''''
为了均衡地使用消费者——保证每个消费者只有一个正在处理的消息，channel.basic_qos(prefetch_count=1)

异常处理
------------
消费者异常——message acknowledge
''''''''''''''''''''''''''''''''''''
消费者处理消息时死亡会导致消息丢失——消费者完成任务后，发送确认信息给生产者，ch.basic_ack(delivery_tag = method.delivery_tag)
RabbitMQ异常——message durability
''''''''''''''''''''''''''''''''''''''
RabbitMQ退出或崩溃时会导致队列和消息丢失——声明队列时传入durable=True、发布消息时传入delivery_mode=2
