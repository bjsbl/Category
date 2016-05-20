# Hibernate xml


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
SessionFactory sfactory = cfg.buildSessionFactory();
...

