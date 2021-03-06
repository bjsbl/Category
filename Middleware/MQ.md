# JMS & AMQP
JMS是sun提出消息同一操作的API,包括create,send,receive;常见的消息队列大部分已经实现了JMS Api;包括ActiveMQ,RabbitMq,支持的消息类型包括textMessage,BytesMessage,ObjectMessage等   
  
AMQP是一种协议，专门解决不同平台之间的消息传递问题，AMQP不是从API层限定，而是直接定义网络交换的数据格式。比JMS多了exchange和binding两个角色。支持的消息类型只有byte[],复杂的对象可以进行序列化处理。  





我们将消息的发布（publish）暂时称作producer，将消息的订阅（subscribe）表述为consumer，将中间的存储阵列称作broker   
# producer---->broker<------consumer  




# 因
随着系统前端服务越来越多样化，对于后端的灵活性邀请越来越高，所以在系统架构方面应该考虑使用消息队列来支持系统。

* 跨系统
* 异步通信
* 降低耦合
* 提高扩展性
* 数据缓冲

# 果

## ActiveMQ 
> http://activemq.apache.org/
Apache ActiveMQ ™ is the most popular and powerful open source messaging and Integration Patterns server.


## Getting Started
### 安装
> JRE 1.7 (1.6 for version <=5.10.0)
> 配置JAVA_HOME,下载tar.gz解压进入bin目录运行
管理接口
http://127.0.0.1:8161/admin/
ActiveMQ's default port is 61616

### 集群
#### 静态发现(通过配置固定的broker uri来发现彼此) 
```
static:(uri1,uri2,uri3,...)?options
```
> http://activemq.apache.org/static-transport-reference.html  

#### 动态发现(在各个broker启动时通过Fanout transport来发现彼此)
```
<broker name="foo">
  <transportConnectors>
    <transportConnector uri="tcp://localhost:0" discoveryUri="multicast://default"/>
  </transportConnectors>
 
  ...
</broker>
```
> http://activemq.apache.org/discovery-transport-reference.html

# Master / Slave
## Shared File System Master Slave (支持N个AMQ实例组网，基于kahadb存储策略，亦可以部署在分布式文件系统上，应用灵活、高效且安全)
> http://activemq.apache.org/shared-file-system-master-slave.html
## JDBC Master Slave (支持N个AMQ实例组网，但他的性能会受限于数据库)
> http://activemq.apache.org/jdbc-master-slave.html
## Replicated LevelDB Store (需要一个ZooKeeper server)
> http://activemq.apache.org/replicated-leveldb-store.html

(zookeeper配置参加)





# 集成Spring
```
<bean id="connectinFactory" class="org.apache.activemq.ActiveMQConnectionFactory">
  <property name="brokerURL" value="tcp://192.168.1.79:61616" />
</bean>

<bean id="cachingConnectionFactory" class="org.springframework.jms.connection.CachingConnectionFactory">
  <property name="targetConnectionFactory" ref="connectinFactory"></property>
  <property name="sessionCacheSize" value="10"></property>
</bean>

<bean id="notifyQueue" class="org.apache.activemq.command.ActiveMQQueue">
  <constructor-arg value="q.notify"></constructor-arg>
</bean>

<bean id="notifyTopic" class="org.apache.activemq.command.ActiveMQTopic">
  <constructor-arg value="t.notify"></constructor-arg>
</bean>

<bean id="jmsTemplate" class="org.springframework.jms.core.JmsTemplate">
  <property name="connectionFactory" ref="cachingConnectionFactory" />
</bean>
 <!-- 使用Spring JmsTemplate 的消息生产者 -->
<bean id="queueMessageProducer" class="com.common.jms.QueueMessageProducer">
  <property name="jmsTemplate" ref="jmsTemplate"></property>
  <property name="notifyQueue" ref="notifyQueue"></property>
  <property name="messageConverter" ref="messageConverter"></property>
</bean>
<bean id="topicMessageProducer" class="com.common.jms.TopicMessageProducer">
  <property name="jmsTemplate" ref="jmsTemplate"></property>
  <property name="notifyTopic" ref="notifyTopic"></property>
  <property name="messageConverter" ref="messageConverter"></property>
</bean>

 <!-- 消息消费者 一般使用spring的MDP异步接收Queue模式 -->
 <!-- 消息监听容器 -->
<bean id="queueContainer" class="org.springframework.jms.listener.DefaultMessageListenerContainer">
  <property name="connectionFactory" ref="connectinFactory"></property>
  <property name="destination" ref="notifyQueue"></property>
  <property name="messageListener" ref="queueMessageListener"></property>
</bean>
 <!-- 消息监听容器 -->
<bean id="topicContainer" class="org.springframework.jms.listener.DefaultMessageListenerContainer">
  <property name="connectionFactory" ref="connectinFactory"></property>
  <property name="destination" ref="notifyTopic"></property>
  <property name="messageListener" ref="topicMessageListener"></property>
  <!-- 发布订阅模式 -->
 <property name="pubSubDomain" value="true" />

 </bean>
 <!-- 异步接收消息处理类 -->
<bean id="queueMessageListener" class="com.common.jms.QueueMessageListener">
  <property name="messageConverter" ref="messageConverter"></property>
</bean>
<bean id="topicMessageListener" class="com.common.jms.TopicMessageListener">
  <property name="messageConverter" ref="messageConverter"></property>
</bean>
<bean id="messageConverter" class="com.common.jms.NotifyMessageConverter">
</bean>
```
## Kafka 
> http://kafka.apache.org/
> http://zookeeper.apache.org/

Apache Kafka is publish-subscribe messaging rethought as a distributed commit log.

### Producers
> bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test
### Consumers
> kafka-console-consumer.sh --zookeeper localhost:2181 --topic test --from-beginning
### brokers

### 消息传输机制
* 最多一次，发送一次，无论成功失败，都不会重发。 (at monst once)  
* 消息至少发送一次,如果消息未能接受成功，可能会重发，直到接受成功。(at least once)
* 消息只会发一次 (exactly once)

### Cluster 
1.配置zookeeper
2.配置每个server.properties;确保broker.id=N唯一性；
3.配置producer.properties的bootstrap.servers=localhost:9092
4.配置consumer.properties的zookeeper.connect=127.0.0.1:2181



## Redis
> http://redis.io/


## RabbitMQ
> http://www.rabbitmq.com/


## ZeroMQ
> http://zeromq.org/