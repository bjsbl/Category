背景
一切都要从Bean开始
为了解决java初期开发的复杂性，降低代码的耦合度
Spring做了什么？
轻量级pojo
依赖注入
切面、声明式编程

> 接口编程

#spring配置

上下文
* ClasspathXmlApplication  从类路径读取配置文件
* FileSystemXmlApplication   从文件系统读取配置文件
* XmlWebApplication   从web应用读取配置文件

Bean生命周期
* Spring初始化bean
* Spring对bean进行注入
* 检测接口（BeanNameware、BeanFacotryWare、ApplicationContextWare、BeanPostProcessor、InitialzingBean、DisablableBean)
* 准备就绪，直到上下文销毁

Bean作用域
Spring默认都是单例（总是返回Bean的同一个实例)
scope
* prototype
* singleton
* request
* session
* global-session

Bean注入
自动装配
* byName
* byType
* constructor
* autodetect  (默认）
* @autowired   注释装配（Spring2.5后） 类似ByType   需要在context命名空间设置 > <context:annotation-config>  
*    
 
<context:annotation-config>  自动检测Bean中的注解
<context:component-scan base-package=""> 除了有annotation-config同样的功能外，还可以自动定义Bean。
<context:include-filter>
<context:exclude-filter>

* @Component   通用型组件
* @Controller   数据控制
* @Repository    数据持久
* @Service     数据服务

> @autowired 自动装配类似byType方式，如果bean不存在就提示nosuchbeandefinitionException,在@autowired 添加@Qualifier() 就变成byName,可是指定bean的名字

Spring命名空间
* aop
* beans
* context
* jee
* jms
* lang
* mvc
* oxm
* tx
* util


# AOP切面
* AspectJ
* JBoss AOP
* Spring AOP


execution(返回类型 包路径.方法(参数))

<aop:advisor>
<aop:after>
<aop:after-returning>
<aop:after-throwing>
<aop:aspect>
<aop:pointcut>
<aop:before>
<aop:config> 顶层aop配置元素


需要在aop命名空间设置 <aop:aspectj-autoproxy>
@Aspect
@Pointcut
@Before
@AfterThrowing
@AfterReturning


#ORM 数据库访问

JdbcTemplate  jdbc
SimpleJdbcTemplate  java5特性
NamedParameterJdbcTemplate 命名参数
HibernateTemplate  hibernate
SqlMapClientTemplate   ibatis
JpaTemplate   jpa

DataSource
* JNDI 
* 连接池(DBCP...)   org.apache.commons.dbcp.BasicDataSource
* JDBC驱动   org.springframework.jdbc.datasource.DriverMangerDataSource

spring==
ParameterizedRowMapper  jdbctemplate查询的每一条记录都会调用maprow()

hibernate==
LocalSessionFacotryBean
AnnotationSessionFactoryBean
  packagesToScan

jpa==
LocalEntityManagerFactoryBean
LocalContainerEntityFactoryBean


#事物Transaction

## PlateformTransactionManager
    JpaTransactionManager
    JtaTransactionManager
    DataSourceTransactionManager
    HibernateTransactionManager


## <tx:annotation-driven>
propagation 事物传播规则
isolation 事物隔离级别
read-only 只读
timeout 事物超时时间
rollback-for 事物回滚不提交
`<tx:adivce>`
`   <tx:attributes>`
`       <tx:method name="*" propagation="" read-only="" />`
`   </tx:attributes>`
`</tx:adivce>`

# MVC
## xml
DispatcherServlet
<mvc:resources mapping="" location="" />

## Annotation
<mvc:annotation-driven />
<context:component-scan />

## View
* org.springframework.web.servlet.view.FreeMarkerViewResolver
* org.springframework.web.servlet.view.UrlBasedViewResolver
* org.springframework.web.servlet.view.BeanNameViewResolver
* org.springframework.web.servlet.view.InternalResourceViewResolver   (*)

# 加载Spring上下文
ContextLoaderListener 是一个servlet监听器，除了DispatherServlet创建上下文，同时可以加载其他配置文件到Spring容器里,
默认查找/WEB-INF/applicationContext.xml。也可以通过contextConfigLocation参数指定路径


* @RequestMapping(value="",method=RequestMethod.Get/Post/Delete/Head/put/Trace/options)
* @RequestParam
* @Valid  ( @Size、@Pattern..)
* @PathVariable

# 文件上传fileupload
在Spring中注册multipart解析器
``` <bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
		<property name="maxUploadSize" value="2048000" />
	</bean>
```


#Spring RMI

## 利弊
* 很难穿越不同网络的防火墙
* 客户端和服务端都必须采用Java,序列化问题，两端的版本必须相同。

### hessian&burlap
> 都是基于http,解决防火墙端口的问题，对于复杂的数据来说，hession和burlap的序列化支持不是很好
#### 服务端注册服务
hessian 与RMI类似，使用二进制传输数据，效率相当，只不过它支持的语言包括PHP,Python,c++,c#,java,flash,ruby....
> http://hessian.caucho.com/

导出一个hessian服务，只需要在xml中声明HessianServiceExporter，其实作为一个springMVC 控制器，在web.xml中配置DispatherServlet的<servlet-mapping />，然后把DispatcherServlet的请求转给hessian的服务，可以使用SimpleUrlHandlerMapping就可以实现。注册相应服务实现即可。

burlap 是基于xml协议传输，所以比hessian的阅读性更好，也不需要定义wsdl或idl
(同hessian类似)

#### 客户端访问服务
* hessian HessianProxyFacotryBean (serivceUrl,serivceInterface)
* burlap BurlapProxyFactoryBean (serivceUrl,serivceInterface)

### Spring HttpInvoker
服务端：HttpInvokerServiceExporter (serivceUrl,serivceInterface)
客户端：HttpInvokerProxyFactoryBean (serivceUrl,serivceInterface)

> 看完之后是不是觉得像是三胞胎...


# Spring REST
* http信息转化器

# Spring JMS
 ActiveMQ
* 创建连接工厂
ActiveMQConnectionFactory

* 传输目的地
可以是一个队列或是一个主题，看需求而定。ActiveMQQueue/ActiveMQTopic

* JmsTemlate接收、发送

* 消息监听MessageListener

