# scp
# iptables
# find 

## 查看Linux登录和操作日志
> last      [last -x可查看用户登陆历史]
> more /var/log/secure   [用户登陆信息]
> who /var/log/wtmp  [用户每次登录进入和退出时间的永久纪录]
> 想看具体用户，su - username,然后history，默认最近1000条操作


## lrzsz 在linux里可代替ftp上传和下载
yum -y install lrzsz 程序会自动安装，
然后如要下载者sz [找到要下载的文件] 
如果要上传，者rz 浏览找到本机要上传的文件



## logrotate 日志分隔
/usr/bin/logrotate
/etc/logrotate.conf
```
/usr/local/nginx/logs/*.log {
    daily
    notifempty
    rotate 20
    minsize 100M
    size 300M
    sharedscripts
    postrotate
        /usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf -s reload
    endscript
}
```
更多参见 > logrotate 帮助信息。
