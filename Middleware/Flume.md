# Flume http://flume.apache.org/
Flume是Cloudera提供的一个高可用的，高可靠的，分布式的海量日志采集、聚合和传输的系统，Flume支持在日志系统中定制各类数据发送方，用于收集数据；同时，Flume提供对数据进行简单处理，并写到各种数据接受方（可定制）的能力。 

# 系统环境要求
* JDK1.6 或是更高
* 内存
* 磁盘空间
* 目录权限

# 启动agent;
> bin/flume-ng agent -n $agent_name -c conf -f conf/flume-conf.properties

## flume-conf.properties
```
a1.sources = r1
a1.sinks = k1
a1.channels = c1

# Describe/configure the source
a1.sources.r1.type = netcat
a1.sources.r1.bind = localhost
a1.sources.r1.port = 44444

# Describe the sink
a1.sinks.k1.type = logger

# Use a channel which buffers events in memory
a1.channels.c1.type = memory
a1.channels.c1.capacity = 1000
a1.channels.c1.transactionCapacity = 100

# Bind the source and sink to the channel
a1.sources.r1.channels = c1
a1.sinks.k1.channel = c1
``` 

# 数据接入
## RPC
## 可执行的命令行
## 网络数据流
* Avro
* Thrift
* Syslog
* Netcat

