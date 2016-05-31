# Mongodb
是介于关系型和非关系型数据库之间，是非关系型数据库中最想关系型数据库的。数据格式类似json,mongodb里边叫bjson;

#安全
* 修改默认端口27017
* bind_ip
* 创建用户和口令
> db.addUser('user','password',true) //true:readonly,默认false
> db.auth('user','password')


# 安装
## window
服务端：
> mongod.exe  --dbpath=c:\db  --logpath=c:\db\log --install --fork
> mongod.exe -f mongodb.cnf
客户端：
> mongo

## Linux 
> mongod --dbpath=/data/db --logpath=/data/db/log --fork
> mongod -f /data/etc/mongodb.cnf

# 结构
## 文档 document (对比关系型：row)

## 集合 collection (对比关系型：table)

## 数据库 database (对比关系型：database)

# mongodb.cnf
* dbpath
* logpath
* logappend
* bind_ip
* port
* fork
* journal
* syncdelay
* directoryperdb
* maxconns
* repairpath


## oplog可以达到 5%的磁盘空间。 oplog 的大小是可以通过 mongod 的参数”—oplogSize”来改变 oplog 的日志大小。

# 常用工具
* mongo
* mongod
* mongodump/mongorestore
* mongoimport/mongoexport
* mongos
* mongostat
* mongofiles (GridFS)

# 查询
* 条件查询 $gt,$lt,$gte,$lte,(>,<,>=,<=),$all,$exists,null,$mod,$ne(!=),$in,$nin,$size,$count,skip,limit,sort
* 存储过程 eval

# 索引
索引信息保存在system.indexes，默认是_id
## 基础索引
> db.collection.ensureIndex({key:1/-1},{background:true})

(1升序/-1降序)  数据量较大时，可以添加background:true在后台执行索引
## 文档索引
## 组合索引
> db.collection.ensureIndex({keyA:1,keyB:1});
## 唯一索引
> db.collection.ensureIndex({key:1/-1},{unique:true});
## 强制索引
> db.collection.hint({key:1})
## 删除索引
> db.collection.dropIndexes();
> db.collection.dropIndex({key:1})



# MapReduce
## Map emit(key,value)
遍历collection的所有记录，把key和value传递给reduce
## Reduce
```
db.runCommand({
mapreduce:<collection>,
map:<function>,
reduce:<function>,
...
...
})
```

* mapreduce: 要操作的目标集合。
* map: 映射函数 (生成键值对序列，作为 reduce 函数参数)。
* reduce: 统计函数。
* query: 目标记录过滤。
* sort: 目标记录排序。
* limit: 限制目标记录数量。
* out: 统计结果存放集合 (不指定则使用临时集合，在客户端断开后自动删除)。
* keeptemp: 是否保留临时集合。
* finalize: 最终处理函数 (对 reduce 返回结果进行最终整理后存入结果集合)。
* scope: 向 map、 reduce、 finalize 导入外部变量。
* verbose: 显示详细的时间统计信息


## mongoexport
> ./mongoexport -d my_mongodb -c user -o user.dat
* -d 指明使用的库, 本例中为” my_mongodb”
* -c 指明要导出的表, 本例中为”user”
* -o 指明要导出的文件名, 本例中为”user.dat”


> ./mongoexport -d my_mongodb -c user --csv -f uid,username,age -o user_csv.dat
* -csv 指要要导出为 csv 格式
* -f 指明需要导出哪些例

## mongoimport
> ./mongoimport -d my_mongodb -c user user.dat

> ./mongoimport -d my_mongodb -c user --type csv --headerline --file user_csv.dat
* -type 指明要导入的文件格式
* -headerline 批明不导入第一行，因为第一行是列名
* -file 指明要导入的文件路径

# mongodump/mongorestore
> ./mongodump -d my_mongodb -o my_mongodb_dump
> ./mongorestore -d my_mongodb my_mongodb_dump/*

# 管理
## 活动进程
> db.currentOp();
## 结束进程
> db.killOp(opid)
## 慢查询
> db.setProfilingLevel(2)
* 0 不开启
* 1 记录慢命令 默认>100ms
* 2 记录所有命令

# ReplicaSets
## Master-Slave
在master服务器后加--master参数，在slave机器上添加--source参数就可以实现主备复制.
## 读写分离
让从库可以读，分担主库的压力
> db.getMongo().setSlaveOk()
## Replica Sets
### 创建目录

> mkdir -p /data/r0
> mkdir -p /data/r1
> mkdir -p /data/r2
> mkdir -p /data/r3
> mkdir -p /data/log

### 启动实例
> mongod --replSet rs1 --fork --port 28010 --dbpath /data/r0 --logpath=/data/log/r0.log --logappend
> mongod --replSet rs1 --fork --port 28011 --dbpath /data/r1 --logpath=/data/log/r1.log --logappend
> mongod --replSet rs1 --fork --port 28012 --dbpath /data/r2 --logpath=/data/log/r2.log --logappend
> mongod --replSet rs1 --fork --port 28013 --dbpath /data/r3 --logpath=/data/log/r3.log --logappend

### 初始化Replica Sets
```
mongo -port 28010
config_rs1 = {_id: 'rs1', members: [
{_id: 0, host: 'localhost:28010', priority:1}, --成员 IP 及端口， priority=1 指 PRIMARY
{_id: 1, host: 'localhost:28011'},
{_id: 2, host: 'localhost:28012'}]
}
rs.initiate(config_rs1);                   --初始化配置
rs.status()                                --查看复制集状态
rs.isMaster()
rs.add("localhost:28013")                  --添加新节点到现有的 Replica Sets
rs.remove("localhost:28014")               --减少节点
mongo/bin/mongo -port 28013                --登录到节点机器   
rs1:SECONDARY>rs.slaveOk()                 
```

## Sharding
### Shard Server
每个 Shard 可以是一个 mongod 实例，也可以是一组 mongod 实例构成的 Replica Set
### Config Server
所有 shard 节点的配置信息、每个 chunk 的 shard key 范围、 chunk 在各 shard 的分布情况、该集群中所有 DB 和 collection 的 sharding 配置信息
### Route Server
前端路由，客户端由此接入，然后询问 Config Servers 需要到哪个 Shard 上查询或保存记录，再连接相应的 Shard 进行操作，最后将结果返回给客户端

#### 创建目录
mkdir -p /data/shard/s0 --创建数据目录
mkdir -p /data/shard/s1
mkdir -p /data/shard/log

mongod --shardsvr --port 20000 --dbpath /data/shard/s0 --fork --logpath /data/shard/log/s0.log --directoryperdb
mongod --shardsvr --port 20001 --dbpath /data/shard/s1 --fork --logpath /data/shard/log/s1.log --directoryperdb
mkdir -p /data/shard/config --创建数据目录
mongod --configsvr --port 30000 --dbpath /data/shard/config --fork --logpath /data/shard/log/config.log --directoryperdb
mongos --port 40000 --configdb localhost:30000 --fork --logpath /data/shard/log/route.log --chunkSize 1 --启动 Route Server 实例
> chunkSize 这一项是用来指定 chunk 的大小的，单位是 MB，默认大小为 200MB，
配置 Sharding
mongo admin --port 40000 --此操作需要连接 admin 库 
db.runCommand({ addshard:"localhost:20000" }) --添加 Shard Server
db.runCommand({ addshard:"localhost:20001" })
db.runCommand({ enablesharding:"test" }) --设置分片存储的数据库
db.runCommand({ shardcollection: "test.users", key: { _id:1 }}) --设置分片的集合名称，且必须指定 Shard Key，系统会自动创建索引

db.runCommand({ listshards: 1 }) --列出所有的 Shard Server
printShardingStatus() --查看 Sharding 信息
db.runCommand({ isdbgrid:1 })

db.runCommand({"removeshard" : "localhost:20002"});    --移除 Shard Server

# Replica Sets + Sharding