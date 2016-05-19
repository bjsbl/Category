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
<tx:adivce>
  <tx:attributes>
     <tx:method name="*" propagation="" read-only="" />
  </tx:attributes>
</tx:adivce>

***
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


* @RequestMapping(value="",method=Get/Post)
* @RequestParam
* @Valid  ( @Size、@Pattern、
* @PathVariable

# 文件上传fileupload
在Spring中注册multipart解析器,
```xml <bean id="multipartResolver"
		class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
		<property name="maxUploadSize" value="2048000" />
	</bean>```


