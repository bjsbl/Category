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

