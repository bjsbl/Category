# Hibernate xml  

Model.hbm.xml  
  <property>  
     insert  默认true    
     update  默认true  
  <class>
     dynamic-insert  动态创建insert,默认false
     dynamic-update  动态创建update,默认false  
    
Hibernate.properties

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
 
## Session缓存
sessionFactory.setFlushMode(FlushModel.Auto);