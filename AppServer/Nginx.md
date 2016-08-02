# nginx.conf

```

#user  nobody;
worker_processes  1;
error_log  logs/error.log;

pid        logs/nginx1.pid;

events {
    use epoll;
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;

    sendfile        on;
    tcp_nopush     on;
    tcp_nodelay on;

    keepalive_timeout  65;

    gzip  on;
    gzip_min_length 1k;
    gzip_buffers 4 16k;
    gzip_types text/plain text/css application/x-javascript;

    proxy_temp_path /tmp/nginx/temp;
    proxy_cache_path /tmp/nginx/cache/1 levels=1 keys_zone=one:10m;
    proxy_cache_path /tmp/nginx/cache/2 levels=2:1 keys_zone=two:100m;
    proxy_cache two;
    
    upstream tomcat{
        ip_hash;
        server 127.0.0.1:8001;
        server 127.0.0.1:8002;
    }
    
    server {
      listen 81;
      server_name 192.168.137.129;
      index index.jsp index.shtml index.html;
      location ~ .*\.(html|htm|gif|jpg|jpeg|bmp|png|ico|txt|js|css)$ {   
          root /opt/toms/html; 
          expires 3d;   
      }
      location / {
          proxy_pass http://tomcat;
          proxy_cache_valid 200 304 12h;
          proxy_cache_key $host$uri$is_args$args; 
          proxy_set_header Host $host;
          proxy_set_header X-Real-IP $remote_addr;
          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      }
    }
}

```

## Instruction

upstream 支持的负载均衡算法
Nginx的负载均衡模块目前支持4种调度算法，其中后两项属于第三方调度算法。  
1.轮询（默认）。每个请求按时间顺序逐一分配到不同的后端服务器，如果后端某台服务器宕机，故障系统被自动剔除，使用户访问不受影响。Weight 指定轮询权值，Weight值越大，分配到的访问机率越高，主要用于后端每个服务器性能不均的情况下。
2.ip_hash。每个请求按访问IP的hash结果分配，这样来自同一个IP的访客固定访问一个后端服务器，有效解决了动态网页存在的session共享问题。
3.fair。这是比上面两个更加智能的负载均衡算法。此种算法可以依据页面大小和加载时间长短智能地进行负载均衡，也就是根据后端服务器的响应时间来分配请求，响应时间短的优先分配。Nginx本身是不支持fair的，如果需要使用这种调度算法，必须下载Nginx的upstream_fair模块。
4.url_hash。此方法按访问url的hash结果来分配请求，使每个url定向到同一个后端服务器，可以进一步提高后端缓存服务器的效率。Nginx本身是不支持url_hash的，如果需要使用这种调度算法，必须安装Nginx 的hash软件包。

upstream 支持的状态参数
1.down，表示当前的server暂时不参与负载均衡。
2.backup，预留的备份机器。当其他所有的非backup机器出现故障或者忙的时候，才会请求backup机器，因此这台机器的压力最轻。
3.max_fails，允许请求失败的次数，默认为1。当超过最大次数时，返回proxy_next_upstream 模块定义的错误。
4.fail_timeout，在经历了max_fails次失败后，暂停服务的时间。max_fails可以和fail_timeout一起使用。
注，当负载调度算法为ip_hash时，后端服务器在负载均衡调度中的状态不能是weight和backup。


语法：proxy_cache_path path [levels=number] keys_zone=zone_name:zone_size [inactive=time] [max_size=size];  
语法：proxy_cache zone_name;  
语法：proxy_cache_valid reply_code [reply_code …] time;  

===========================================================================================================================
openssl
tar -xvzf /usr/local/openssl-0.9.8zg.tar.gz
cd /usr/local/openssl-0.9.8zg
./config --prefix=/usr/local/openssl
./config -t
make depend
make install
cd /usr/local
ln -s openssl ssl
在/etc/ld.so.conf文件的最后面，添加如下内容：/usr/local/openssl/lib
ldconfig
# vi /etc/profile
在/etc/profile的最后一行，添加：
export OPENSSL=/usr/local/openssl/bin
export PATH=$OPENSSL:$PATH:$HOME/bin
ldd /usr/local/openssl/bin/openssl
openssl version
===========================================================================================================================

./configure --prefix=/usr/local/nginx --sbin-path=/usr/sbin/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --pid-path=/var/run/nginx/nginx.pid --lock-path=/var/lock/nginx.lock --with-http_ssl_module --with-http_flv_module --with-http_stub_status_module --with-http_gzip_static_module --http-client-body-temp-path=/var/tmp/nginx/client/ --http-proxy-temp-path=/var/tmp/nginx/proxy/ --http-fastcgi-temp-path=/var/tmp/nginx/fcgi/ --http-uwsgi-temp-path=/var/tmp/nginx/uwsgi --http-scgi-temp-path=/var/tmp/nginx/scgi 

===========================================================================================================================
启动nginx提示：error while loading shared libraries: libpcre.so.1: cannot open shared object file: No such file or directory，意思是找不到libpcre.so.1这个模块，而导致启动失败。
---------------------------------------------------------------------------------------------------------------------------
如果是32位系统
[root@lee ~]#  ln -s /usr/local/lib/libpcre.so.1 /lib
如果是64位系统
[root@lee ~]#  ln -s /usr/local/lib/libpcre.so.1 /lib64
然后在启动nginx就OK了
[root@lee ~]# /usr/local/webserver/nginx/sbin/nginx
===========================================================================================================================

location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$
{
     expires 30d;
}

location ~ .*\.(js|css)?$
{
     expires 1h;
}   
