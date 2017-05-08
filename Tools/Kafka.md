# Kafka


## 简介
Kafka没有提供企业级特性，比如‘消息确认’，‘消息分组’，在一定程度上不能保证消息的发送与接收的绝对可靠

Kafka对消息保存时根据Topic进行归类，发送消息者成为Producer,消息接受者成为Consumer,集群有多个Kafka实例组成，每个实例(server)成为broker.


主要特性：
 1）消息持久化
要从大数据中获取真正的价值，那么不能丢失任何信息。设计上是时间复杂度O(1)的磁盘结构，它提供了常量时间的性能，即使是存储海量的信息（TB级）。
2）高吞吐
记住大数据，Kafka的设计是工作在标准硬件之上，支持每秒数百万的消息。
3）分布式
Kafka明确支持在Kafka服务器上的消息分区，以及在消费机器集群上的分发消费，维护每个分区的排序语义。
4）多客户端支持
Kafka系统支持与来自不同平台（如java、.NET、PHP、Ruby或Python等）的客户端相集成。
5）实时
生产者线程产生的消息对消费者线程应该立即可见，此特性对基于事件的系统（比如CEP系统）是至关重要的。



 Kafka和JMS实现(activeMQ)不同的是:即使消息被消费,消息仍然不会被立即删除.日志文件将会根据broker中的配置要求,保留一定的时间之后删除;比如log文件保留2天,那么两天后,文件会被清除,无论其中的消息是否被消费.kafka通过这种简单的手段,来释放磁盘空间,以及减少消息消费之后对文件内容改动的磁盘IO开支



 ## 命令
 > 启动Server 依赖 ZK 服务
 > bin/kafka-server-start.sh config/server.properties &
 > 创建Topic
 > bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic page_visits
 > 查看命令
 > bin/kafka-topics.sh --list --zookeeper localhost:2181
 > 发送消息
 > bin/kafka-console-producer.sh --broker-list localhost:9092 --topic page_visits
 > 消费消息
 > bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic page_visits --from-beginning
 > 多 Broker 方式
 > bin/kafka-server-start.sh config/server-1.properties &
 > bin/kafka-server-start.sh config/server-2.properties &
 > bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 3 --partitions 1 --topic visits
 > bin/kafka-topics.sh --describe --zookeeper localhost:2181 --topic visits
 > bin/kafka-console-producer.sh --broker-list localhost:9092 --topic visits
 > my message test1
 > my message test2
 > 删除无用的topic
 > bin/kafka-run-class.sh kafka.admin.DeleteTopicCommand --topic visits --zookeeper sjxt-hd02:2181,sjxt-hd03:2181,sjxt-hd04:2181