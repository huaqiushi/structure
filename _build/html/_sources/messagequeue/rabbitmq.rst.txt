RabbitMQ
=============

将消息通过队列分发给消费者

.. image:: ../.img/RabbitMQ.JPG

- producer：发送消息给exchange
- exchange：接收生产者的消息并按路线发送（route）到队列中。exchange有四种类型：direct, topic, headers, fanout；每一种类型下具体的匹配规则称为binding

    - fanout：分发给每个消费者
    - direct：通过两个routing_key之间的匹配关系进行分发（生产者发布消息时的routing_key、队列绑定交换机时的routing_key）

        - 例：routing_key：'orange'
        - 注：RabbitMQ默认的exchange是direct：exchange为空字符串时，RabbitMQ会为每个队列绑定一个值为队列名的routing_key

    - topic：与direct相比，routing_key变为多个属性

        - 例：routing_key： ' * .orange. * ', ' * . * .rabbit', 'lazy.#'

    - headers：很少使用

- queue：存储消息（和交换机绑定以存储需要的信息）
- consumer：从某一个队列中获取消息并处理

AMQP
--------
RabbitMQ是用Erlang语言开发、基于AMQP的一个broker server

connection
'''''''''''''''
一个application和broker server之间的连接（是基于TCP的长连接）

channel
''''''''''''
一个application和broker server有多个连接时，每一个连接即一个channel（这些channel共用一个connection）

virtual host
'''''''''''''''''
一个broker server可以创建多个隔离的AMQP环境（拥有自己的队列、绑定和交换机），每一个AMQP环境即一个virtual host

分发方式
-----------
round-robin dispatching
''''''''''''''''''''''''''''
默认的分发方式。有多个消费者时，RabbitMQ将队列中的消息循环分发给每个消费者

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
