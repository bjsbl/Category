
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
