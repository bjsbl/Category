# weinre

## 调试https请求的页面，使用weinre无法解决


前端开发的时候会遇到一些‘无法解释’的问题，这时需要一些debug方法找问题。
用chrome自带的调试工具或是firebug有时也很难找到问题，这时需要weinre登场。

> http://people.apache.org/~pmuellr/weinre/docs/latest/Home.html

安装方式：

```
 npm -g install weinre
```

使用：
```
weinre --bound -all- --httpPort 8888
(默认8080)

```

1. ‘Target Script’  把下方的Example代码copy到项目中。
2. 进入‘debug client user interface’  
3. 在Elements与Console中调试移动端的页面了。