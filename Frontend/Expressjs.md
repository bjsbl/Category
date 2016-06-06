# Epxress 4.x
> npm install express --save

## 静态文件和视图
> app.use(epxress.static(__dirname+'/public'));

## 请求体
一般post请求体常见媒体类型是application/x-www-form-urlendcoded;
post上传文件的媒体类型是multipart/form-data;
ajax的媒体类型是application/json;

## request
req.params
req.param(name)
req.query
req.body
req.route
req.header
req.ip
req.accept([type])
req.path
req.host
req.protocol
req.secure
req.xhr
## response
res.status(code)
res.set(name,value)
res.cookie(name,value)
res.direct([status],url)
res.send(body)/res.send(status,body)
res.json(json)/res.json(status,json)
..
.


