# uglifyjs
> http://lisperator.net/uglifyjs/
```
npm install uglify-js -g
uglifyjs inet.js -m -o inet-min.js
```
-o导出文件名称
-m参数所以就是把变量名变成a, b, c, d, ...

928KB  --> 240KB

## 批处理压缩js

```
@echo off
:: 设置压缩JS文件的根目录，脚本会自动按树层次查找和压缩所有的JS
SET JSFOLDER=C:\wxzj\js
echo 正在查找JS文件
chdir /d %JSFOLDER%
for /r . %%a in (*.js) do (
    @echo 正在压缩 %%~a ...
    uglifyjs %%~fa  -m -o %%~fa
)
echo 完成!
pause & exit
```

# jshint
> npm install jshint -g
基本使用：
```
jshint xxx.js
```
配置参数 package.json 
> http://jshint.com/docs/



