# Dubbo
> https://github.com/alibaba/dubbo
> https://github.com/dangdangdotcom/dubbox



## 打包Master遇到的问题
在pom.xml
中添加111行修改webx_version版本
```
<webx_version>3.1.6</webx_version>
<velocity_version>1.7</velocity_version>
```

289行添加
```
<dependency>
    <groupId>org.apache.velocity</groupId>
    <artifactId>velocity</artifactId>
    <version>${velocity_version}</version>
</dependency>
```

具体参见：
> https://github.com/alibaba/dubbo/issues/50


# Zookeeper
> http://zookeeper.apache.org/


# Spring集成
jar依赖
zookeeper.jar
zkclient.jar
slf4j-api.jar
slf4j-log4j.jar
netty.jar
log4j.jar
javassist.jar
具体参见dubbo的pom.xml


# Dubbo Monitor
下载简易监控中心	
> http://dubbo.io/Download-zh.htm
解压后修改conf/dubbo.properties;
./bin/start.sh
具体使用参见：
> http://dubbo.io/User+Guide-zh.htm


