Zipkin 是一款开源的分布式实时数据追踪系统（Distributed Tracking System），基于 Google Dapper 的论文设计而来，由 Twitter 公司开发贡献


# 启动
## Docker
> https://github.com/openzipkin/docker-zipkin
## Java
> https://search.maven.org/remote_content?g=io.zipkin.java&a=zipkin-server&v=LATEST&c=exec
```
java -jar zipkin.jar
```
## Source
> https://github.com/openzipkin/zipkin

```
./mvnw -DskipTests --also-make -pl zipkin-server clean install
java -jar ./zipkin-server/target/zipkin-server-*exec.jar
```

启动后访问：localhost:9411/

# 原理
![架构](http://zipkin.io/public/img/architecture-1.png '架构')

# 客户端Libraries
> https://github.com/openzipkin/brave
> https://github.com/openzipkin/zipkin-js
> https://github.com/apache/incubator-htrace/tree/master/htrace-zipkin
> ....

# 数据模型
## cs Client Start
## sr Server Receive
## ss Server Send
## cr Client Receive
## Trace Id 
## Span Id
## Parent Id

# Mysql集成
> https://github.com/openzipkin/zipkin/blob/master/zipkin-storage/mysql/src/main/resources/mysql.sql
## Cassandra集成
## Elasticsearch集成

# 参数配置
zipkin*.exec.jar里的BOOT-INF\classes\zipkin-server-shared.yml文件
```
java -DKAFKA_ZOOKEEPER=localhost:2181 -DSTORAGE_TYPE=cassandra -jar zipkin-server-1.19.2-exec.jar
```




# SpringMVC
```
<mvc:interceptors>
  <bean
    class="com.github.kristofa.brave.spring.ServletHandlerInterceptor">
    <constructor-argvalue="#{brave.serverRequestInterceptor()}"/>
    <constructor-argvalue="#{brave.serverResponseInterceptor()}"/>
    <constructor-arg>
      <bean
        class="com.github.kristofa.brave.http.DefaultSpanNameProvider"/>
    </constructor-arg>
    <constructor-argvalue="#{brave.serverSpanThreadBinder()}"/>
</bean>
</mvc:interceptors>
```

brave-mysql 模块在 JDBC 驱动层面添加了一些拦截器，可以对 MySQL 的查询进行监控
```
<bean
class="com.github.kristofa.brave.mysql.MySQLStatementInterceptorManagementBean" destroy-method="close">
  <constructor-argvalue="#{brave.clientTracer()}"/>
</bean>
```
