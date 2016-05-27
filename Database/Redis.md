# 数据结构
* string
* hashe
* list
* set
* sorted set
* bitmap
* geo
* hyperloglog

# 目录命名
## Keys
* del
* keys
* rename
* exists

## String
* append
* get
* incr
* set
* strlen
## Hash
## List
## Set
## SortedSet
## HyperLogLog
## GEO
## Pub/Sub
## Transaction
## Script
## Connection
## Server
* client list
* dbsize
* flushall
* flushdb
* info
* client kill
* monitor
* slaveof
* sync
* time
* config set [key] [vlaue]   动态调整配置，不用重启

# Sentinel
用于管理多个redis实例，主要用于监控、提醒、故障迁移
## 启动
> redis-sentinel /path/to/sentinel.conf  
> redis-server /path/to/sentinel.conf --sentinel
## 配置
``` xml 
sentinel monitor mymaster 127.0.0.1 6379 2
sentinel down-after-milliseconds mymaster 60000
sentinel failover-timeout mymaster 180000
sentinel parallel-syncs mymaster 1
sentinel monitor resque 192.168.1.3 6380 4
sentinel down-after-milliseconds resque 10000
sentinel failover-timeout resque 180000
sentinel parallel-syncs resque 5
```

配置Sentinel 去监视一个名为 mymaster 的主服务器， 这个主服务器的 IP 地址为 127.0.0.1 ， 端口号为 6379 ， 而将这个主服务器判断为失效至少需要 2 个 Sentinel 同意 （只要同意 Sentinel 的数量不达标，自动故障迁移就不会执行）。
不过要注意， 无论你设置要多少个 Sentinel 同意才能判断一个服务器失效， 一个 Sentinel 都需要获得系统中多数（majority） Sentinel 的支持， 才能发起一次自动故障迁移， 并预留一个给定的配置纪元 （configuration Epoch ，一个配置纪元就是一个新主服务器配置的版本号）。
换句话说， 在只有少数（minority） Sentinel 进程正常运作的情况下， Sentinel 是不能执行自动故障迁移的。

# Cluster
## 配置
```
port 7000
cluster-enabled yes
cluster-config-file nodes.conf
cluster-node-timeout 5000
appendonly yes
```

## 启动
```
mkdir cluster-test
cd cluster-test
mkdir 7000 7001 7002 7003 7004 7005

cd 7000
../redis-server ./redis.conf

./redis-trib.rb create --replicas 1 127.0.0.1:7000 127.0.0.1:7001 \
127.0.0.1:7002 127.0.0.1:7003 127.0.0.1:7004 127.0.0.1:7005
```

## 对集群分片
```
$ ./redis-trib.rb reshard 127.0.0.1:7000
```



  
