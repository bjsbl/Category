# Hibernate xml  

Model.hbm.xml  
  <property>  
     insert  默认true    
     update  默认true  
  <class>
     dynamic-insert  动态创建insert,默认false
     dynamic-update  动态创建update,默认false  
    
Hibernate.properties  
hibernate.jdbc.batch_size=20; 
hibernate.connection.autocommit=false; (默认false) 


Hibernate.cfg.xml


Configuration cfg = new Configuration();   默认读取文件路径下的hibernate.properties配置文件。
SessionFacotry sessionFactory = cfg.buildSessionFactory();


# Hibernate Annotation

@Entity
@Table(name='xx')
@Id
@GenerateValue
@Column(name='xxx')
 

AnnotationConfiguration cfg = new AnnotationConfiguration();
...
cfg.addAnnotation(Bean.class);
...
SessionFactory sessionFactory = cfg.buildSessionFactory();
...


# 主键生成策略
* increment
* identify
* sequence
* hilo
* native
* uuid.hex
* assigned
* select
* foreign


Mysql : identify,increment,hilo,native
Oracle : sequence,hilo,incremnt,native
跨数据库： native


## 多对一单向(N-1)
<many-to-one name='' column='' class='' lazy='' not-null='' cascade='' />  
 cascade : save-update 更新当前对象时会级联保存和更新与它关联的对象。  
 

## 一对多双向(1-N)
<set name='' cascade='' inverse=''>  
  <key column='' />  
  <one-to-many class='' />  
</set>

 cascade : delete 级联删除关联对象。
         : all-delete-orphan
 
## 一对一
<one-to-one name='' class='' property-ref='' cascade='' />

## 多对多(单向)
<set name='' table='' lazy='' cascade=''>  
  <key='' />  
  <many-to-many class='' column='' />  
</set>  

## 多对多(双向)    
双向配置<set>,其中一端的inverse设置为true   （可以将多对多分解为两个一对多的关联）



## Session缓存
sessionFactory.setFlushMode(FlushModel.Auto);

FlushModel.auto  (优先)
FlushModel.commit
FlushModel.never

### Load和Get

load()如果找不到数据抛出ObjectNotFoundException;   (延迟检索,lazy)
get() 不抛出异常   (立即检索)

## delete,saveorupdate,update,merge

# 级联操作
 casecade  
* none  （忽略关联对象，默认）  
* save-update   (save,update,saveorupdate时级联操作对象,并且包括游离对象)  
* delete (delete时级联操作对象)  
* all (包括save-update,delete,refresh,evict)  
* evict (当session的evict清除对象时)  
* refresh (当session的refresh刷新对象时)  
* delete-orphan  
* all-delete-orphan  (包含all和delete-orphan)  

# 集合Set,List,Map


# 数据库事物
Transaction tx = session.beginTransaction();  
tx.setTimeout(seconds);    
tx.rollback();  
tx.commit();  

## 悲观锁,乐观锁
  



 