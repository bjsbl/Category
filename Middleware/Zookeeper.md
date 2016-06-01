# zookeeper
zookeeper推荐最低三台配置

tar -xvzf zookeeper.tar.gz
mv conf/zoo_sample.cfg conf/zoo.cfg

dataDir=/users/me/zookeeper
dataLogDir=/home/amqbroker/zkdir/log  
initLimit=10  
yncLimit=5  
maxClientCnxns=60 
clientPort=2181  
server.1=192.168.137.240:2888:3888  
server.2=192.168.137.241:2888:3888  
server.3=192.168.137.242:2888:3888 


The client tries to connect to localhost/127.0.0.1:2181.
