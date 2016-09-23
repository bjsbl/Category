f# Logstash
(Collect, Enrich & Transport Data) 收集、丰富、传输日志
## Input Plugin
### file
path=>["pathA","pathB"]    (必填)  数组
start_position=>"beginning|end"   (选填)  默认end; 字符串
type=>"nginx"   (选填)   字符串

### kafka
zk_connect 字符串 默认localhost:2181

## Filter Plugin
### grok
解析非格式化日志，解析成结构化数据
格式:%{SYNTAX:SEMANTIC}
match => {"message" => ["host":"","ip":""]}
match => {"message" => "%{IP:client} %{WORD:method}"}
### date
分析时间字段,成为事件的时间戳

## Output Plugin


# Elasticsearch
(Search & Analyze Data in Real Time) 实时分析查询

## 集群管理工具
> ./plugin install mobz/elasticsearch-head

# Kibana
(Explore & Visualize Your Data) 呈现数据

# Beat
(Data Shippers for Elasticsearch) 
## Packetbeat (Analyze network packet data.)
## Filebeat (Real-time insight into log data.)
## Topbeat (Get insights from infrastructure data.)
## Winlogbeat (Analyze Windows event logs.)

