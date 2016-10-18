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

# Dubbo Provider

## XML
```
    <dubbo:application name="ktsoa.user" />

	<dubbo:registry address="zookeeper://192.168.137.128:2181" />

	<dubbo:protocol name="dubbo" port="20880" />


	<dubbo:service interface="ktsoa.service.ITest" ref="Itest" />

	 <bean id="Itest" class="ktsoa.service.impl.ITestImpl" />
```

## Annotation
```
    <dubbo:annotation />

	<dubbo:application name="ktsoa.user" />

	<dubbo:registry address="zookeeper://192.168.137.128:2181" />

	<dubbo:protocol name="dubbo" port="20880" />

	<context:component-scan base-package="ktsoa">
		<context:include-filter type="annotation"
			expression="com.alibaba.dubbo.config.annotation.Service" />
		<context:exclude-filter type="annotation"
			expression="org.springframework.stereotype.Controller" />
		<context:exclude-filter type="annotation"
			expression="org.springframework.web.bind.annotation.ControllerAdvice" />
	</context:component-scan>
```

注意service是dubbo的，不是spring的service;
```
package ktsoa.service.impl;

import com.alibaba.dubbo.config.annotation.Service;

import ktsoa.service.ITest;

@Service(version = "1.0")
public class ITestImpl implements ITest {

	@Override
	public String ITestService() {
		// TODO Auto-generated method stub
		return "Hello";
	}

}
```

# Dubbo consumer
## xml

```
	<dubbo:application name="ktsoa.user.consumer" />

	<dubbo:registry address="zookeeper://192.168.137.128:2181" />

	<dubbo:reference interface="ktsoa.dubbo.service._UserService" id="_UserService" version="1.0" />
```
注意：dubbo:reference的路径必须和provider的路径一致，否则会出错的！，consumer只需要定义接口，不需要实现。



# Dubbo Monitor
下载简易监控中心	
> http://dubbo.io/Download-zh.htm
解压后修改conf/dubbo.properties;
./bin/start.sh
具体使用参见：
> http://dubbo.io/User+Guide-zh.htm


