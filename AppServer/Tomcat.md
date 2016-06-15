# JAVA_OPTS
JAVA_OPTS='-Xms1024m -Xmx2048m -XX:PermSize=256M -XX:MaxNewSize=256m -XX:MaxPermSize=256m'
-server  启用jdk 的 server 版；  
-Xms    java虚拟机初始化时的最小内存；  
-Xmx   java虚拟机可使用的最大内存；  
-XX:PermSize    内存永久保留区域  
-XX:MaxPermSize   内存最大永久保留区域     

# Server.xml
<Server port="8005" shutdown="SHUTDOWN">
<Executor name="tomcatThreadPool" namePrefix="catalina-exec-"  maxThreads="250" minSpareThreads="20"/>  
<Connector port="8081" connectionTimeout="20000" protocol="HTTP/1.1" URIEncoding="UTF-8" redirectPort="8443" ...>


