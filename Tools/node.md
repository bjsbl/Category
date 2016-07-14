# uglifyjs 代码压缩
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

# jshint 代码验证，发现潜在问题
> npm install jshint -g
基本使用：
```
jshint xxx.js
```
配置参数 package.json 
> http://jshint.com/docs/


# clean-css 压缩合并CSS
* 要求 Node.js 4.0+ 

> https://github.com/jakubpawlowicz/clean-css

> npm install clean-css
> cleancss -o A-min.css A.css

参数：
-o, --output [output-file] 
-s, --skip-import
-d, --debug
-c, --compatibility [ie7|ie8]      

## Unix
> cat a.css b.css c.css | cleancss -o d.css

## window
> type a.css b.css c.css | cleancss -o d.css


# gulpjs 自动化构建
> npm install -g gulp

## gulp-cli
Task 可以通过 gulp <task> <othertask> 方式来执行。如果只运行 gulp 命令，则会执行所注册的名为 default 的 task，如果没有这个 task，那么 gulp 会报错。

