# 基础
bootstrap所有Javascript都依赖JQuery
bootstrap主要用max-width、min-width和and进行不同分辨率适配
@media(max-width:768px){}
@media(min-width:897px){}
@media(min-width:100px) and (max-with:800px){}

## 立即调用的函数表达式
(function(){})()
(function(){})(1)
(function(){}())
(function(){}(1))

## 原型
window.prototype.alert = function(){};

# CSS12栅格系统
屏幕尺寸 <768px       >=768px      >=992px      >=1200px
样式前缀 .col-xs-     .col-sm-      .col-md-     .col-lg-
最大列宽  自动          60px         78px         95px
padding  (每列左右15px)

## 浮动问题
<div class="clearfix visible-xs"></div>


* 基础样式 btn,alert
* 颜色样式 btn-info,alert-success
* 尺寸样式 btn-ns,btn-sm,btn-lg
* 状态样式 active,disabled
*

# 滚动监听 
Scrollspy
## 需要相对定位 position: relative;
## 通过 data 属性调用

 
# 待续



