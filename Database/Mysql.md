
# Trigger
官方文档：
```
CREATE
    [DEFINER = { user | CURRENT_USER }]
    TRIGGER trigger_name
    trigger_time trigger_event
    ON tbl_name FOR EACH ROW
    [trigger_order]
    trigger_body

trigger_time: { BEFORE | AFTER }

trigger_event: { INSERT | UPDATE | DELETE }

trigger_order: { FOLLOWS | PRECEDES } other_trigger_name
```

来个Demo:
```
create table t_insert (name varchar(20);
create table t_insert_c (name varchar(20));
create trigger insert_trigger after insert on t_insert_c for each row
begin
 insert into t_iinsert_c (name) values (new.name);  /*new?old?*/
end 
```





# Event
官方文档：
```
CREATE
    [DEFINER = { user | CURRENT_USER }]
    EVENT
    [IF NOT EXISTS]
    event_name
    ON SCHEDULE schedule
    [ON COMPLETION [NOT] PRESERVE]
    [ENABLE | DISABLE | DISABLE ON SLAVE]
    [COMMENT 'comment']
    DO event_body;

schedule:
    AT timestamp [+ INTERVAL interval] ...
  | EVERY interval
    [STARTS timestamp [+ INTERVAL interval] ...]
    [ENDS timestamp [+ INTERVAL interval] ...]

interval:
    quantity {YEAR | QUARTER | MONTH | DAY | HOUR | MINUTE |
              WEEK | SECOND | YEAR_MONTH | DAY_HOUR | DAY_MINUTE |
              DAY_SECOND | HOUR_MINUTE | HOUR_SECOND | MINUTE_SECOND}
```

来个Demo:
```
set global event_scheduler=on;
show variables like 'event_scheduler';
use test;
create table t_insert (line timestamp);
create event a_insert on schedule every 1 second do insert into test.t_insert (line) values (now());
alter event a_insert disable;
alter event a_insert enable;
drop event if exists a_insert;
```

# Mysql优化
1.打开mysql慢查询"
Windows下开启MySQL慢查询
MySQL在Windows系统中的配置文件一般是是my.ini找到[mysqld]下面加上
log-slow-queries = F:\MySQL\log\mysqlslowquery.log
long_query_time = 2

Linux下启用MySQL慢查询
MySQL在Windows系统中的配置文件一般是是my.cnf找到[mysqld]下面加上
log-slow-queries=/data/mysqldata/slowquery.log
long_query_time=2


在my.cnf或者my.ini中添加log-queries-not-using-indexes参数，表示记录下没有使用索引的查询。比如：
log-slow-queries=/data/mysqldata/slowquery.log
long_query_time=2
log-queries-not-using-indexes

一般这个目录要有MySQL的运行帐号的可写权限，一般都将这个目录设置为MySQL的数据存放目录；
long_query_time=2中的2表示查询超过两秒才记录

2. mysqldumpslow
```
/path/mysqldumpslow -s c -t 10 /database/mysql/slow-log
```
这会输出记录次数最多的10条SQL语句，其中：
   -s, 是表示按照何种方式排序，c、t、l、r分别是按照记录次数、时间、查询时间、返回的记录数来排序，ac、at、al、ar，表示相应的倒叙；
   -t, 是top n的意思，即为返回前面多少条的数据；
   -g, 后边可以写一个正则匹配模式，大小写不敏感的；
比如
/path/mysqldumpslow -s r -t 10 /database/mysql/slow-log
得到返回记录集最多的10个查询。
/path/mysqldumpslow -s t -t 10 -g “left join” /database/mysql/slow-log
得到按照时间排序的前10条里面含有左连接的查询语句。

## pt-query-digest
pt-query-digest是用于分析mysql慢查询的一个工具，它可以分析binlog、General log、slowlog，也可以通过SHOWPROCESSLIST或者通过tcpdump抓取的MySQL协议数据来进行分析。可以把分析结果输出到文件中，分析过程是先对查询语句的条件进行参数化，然后对参数化以后的查询进行分组统计，统计出各查询的执行时间、次数、占比等，可以借助分析结果找出问题进行优化。
pt-query-digest是一个perl脚本，只需下载并赋权即可执行。
```
[root@test1 ]# wget percona.com/get/pt-query-digest 
[root@test1 ]# chmod u+x pt-query-digest
```