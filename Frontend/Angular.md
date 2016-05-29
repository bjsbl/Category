# ng-app
简单的数据绑定
# ng-model

# 模块 (module)
在angular中声明模块 angular.module('moduleName',['paramName']) ，第一个参数是模块名称，第二参数是依赖其他模块名称

# 作用域 (scope)
$scope是用来定义业务逻辑、控制器方法和视图;
作用域可以多层嵌套，子作用域继承父作用域，一直找到$rootscope，如果在$rootscope找不到，则视图就无法更新;

# 控制器 (controller)
var app = angular.module('app',[]);
app.controller('actrl',function($scope){...});


# 过滤器 (filter)
## 内置过滤器：
* currency
* date:'ymdhms'
* filter
* json
* limitTo
* lowercase
* number
* orderBy
* uppercase
## 自定义过滤器
angular.module('app.filter',[]).filter('name',function(){
return function(input){}
})

# 指令 (directive)
angular.module('directives',[]).directive('name',function(){
return {
restrict:'EACM',
template:''.
replace:'',
templateUrl:''
}	
})

E：元素
A：属性
C：类
M：注释
## 内置指令
* ng-href  如果URL是由作用域动态创建时，应该有ng-href代替href,使用ng-href,angular会等到URL生效后再执行链接，如果href则不会加载链接。
* ng-src
* ng-disabled
* ng-checked
* ng-readonly
* ng-selected
* ng-class
* ng-style





angular.element($0).scope() 获取当前节点的scope

