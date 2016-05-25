# npm
node的包管理器 
npm <cmd> -h   (-g 全局范围,默认当前路径) 
access, add-user, adduser, apihelp, author, bin, bugs, c,cache, completion, config, ddp, dedupe, deprecate, dist-tag,
dist-tags, docs, edit, explore, faq, find, find-dupes, get,help, help-search, home, i, info, init, install,
install-test, issues, it, la, link, list, ll, ln, login,logout, ls, outdated, owner, pack, ping, prefix, prune,
publish, r, rb, rebuild, remove, repo, restart, rm, root,run-script, s, se, search, set, show, shrinkwrap, star,
stars, start, stop, t, tag, team, test, tst, un, uninstall,unlink, unpublish, unstar, up, update, upgrade, v, verison,
version, view, whoami

目前用到的有
* install  
* outdated
* search
* start/stop
* test
* update
* version
* init
* help  

# Express
## 第一步
> npm init   (创建package.json)
> npm install --save express    (更新package.json)
> var express = require('express'); 
> var app = new express();
> app.set('port',process.env.PORT || 3000);
> app.use(function(req,res){
>     res.type('text/html');
>     res.status(404);
>     res.send('not found');
> })

## 第二步
视图与布局
jade,类似Java中的freemarker，视图模板语言

## 第三步
静态文件
> app.use(express.static(__static__+'/public/');


# Request&Response
## Request
* req.params
* req.param(name)
* req.query
* req.body
* req.route
* req.cookies/req.singedCookies
* req.headers
* req.accepts([types])
* req.ip
* req.path
* req.host
* req.xhr
* req.protocol
* req.secure
* req.url/req.originalUrl
* req.acceptLanguage
## Response
* res.status(code)
* res.set(name,value)
* res.cookie(name,value,[options])/res.clearCookie(name,[options])
* res.redirect([status],url)
* res.send(body)/res.send(status,body)
* res.json(json)/res.json(status,json)
* res.jsonp(json)/res.jsonp(status,json)
* res.type(type)  相当于res.set('Conteng-type','type')
* res.format(object)
* res.attachment([filename],res.download(path,[filename],[callback])
* res.sendFile(path,[option],[callback]
* res.links(links)
* res.locals/res.render(view,[locals],callback)


# Form
get  --> req.query
post --> req.body  (body-parser) 
> npm --install body-parser --save   
## 文件上传
<form ... enctype='multipart/form-data' method='post' ..>
> npm --install formidable --save

JqueryFileUpload
> npm install jquery-file-upload-middleware

# Cookie
> npm install cookie-parser --save

# Session
> npm install express-session --save

# Email
> npm install nodemailer

# Logger
> npm install express-logger --save

# Test
> npm install loadtest --save

# ORM持久
Mongodb
驱动mongoose
> npm install mongoose --save

# Route
Express中的路由默认不会处理子域名
> npm install vhost --save

#跨域
> app.use(require('cors')());

#REST
> npm install connect-rest --save


