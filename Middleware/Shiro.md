# Apache Shiro

## Authentication (登录/验证身份)
principals 身份
credentials 凭证
Realm (数据源)
JDBC Realm
## Authorization  (授权)

## SessionManager

## Realm

## SessionDao

## CacheManager

## SecurityManager

# 授权方式
## if(){}else{}
## @RequiresRoles('admin') 
## <shiro:hasRole name='admin'>

# 权限
规则：“资源标识符：操作：对象实例 ID” 即对哪个资源的哪个实例可以进行什么操作。
其默认支持通配符权限字符串，“:”表示资源/操作/实例的分割；“,”表示操作的分割；“*”表示任意资源/操作/实例。
subject().checkPermissions("system:user:update");

