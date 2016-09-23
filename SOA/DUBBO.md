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

