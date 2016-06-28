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
angular.module('name').directive(function(){return{}}); 第一个参数是指令名称，第二个参数是一个定义指令全部行为的对象
angular.module('directives',[]).directive('name',function(){
return {
restrict:'EACM',
template:''.
replace:'',
templateUrl:''
}	
})
* restrict : [E：元素   A：属性(默认)  C：类名(样式）  M：注释] 字符型
* priority : 优先级,同一优先级，优先调用前边声明的指令。同一指令优先级高的优先执行  数值型
* terminal : 停止运行当前元素上比本指令优先级低的指令，但同当前指令优先级相同的指令还是被执行  布尔型
* template : (element,attrs)  /一段html文本；   字符串/函数
* templateUrl : (element,attrs) / 一段html文本；[1.跨域问题，2.模板是异步加载,等待模板加载完成后才编译]   ($templateCache)  字符串/函数
* replace : 默认false,默认把模板当做子元素插入到调用指令的元素内部  布尔型
* scope : 
* transclude : 
* controller : 查找注册在应用中的控制器($scope,$element,$attrs,$transclude) 字符串/函数



## 内置指令
* ng-href  如果URL是由作用域动态创建时，应该有ng-href代替href,使用ng-href,angular会等到URL生效后再执行链接，如果href则不会加载链接。
* ng-src
* ng-disabled
* ng-checked
* ng-readonly
* ng-selected
* ng-class
* ng-style
* ng-include
* ng-switch 和ng-switch-when;ng-switch-default 配合使用
* ng-repeat  ($index,$first,$middle,$even,$odd)
* ng-view
* ng-if
* ng-bind 避免{{}} 渲染引起问题
* ng-cloak  同ng-bind
* ng-model 将表单中的input,select,textarea或是自定义表单中的属性进行绑定
* ng-show/ng-hide
* ng-change
* ng-click
* ng-select/ng-options

# 模块加载
* 配置
angular.module('app'[]).config(function(provider){})

* 运行块
angular.module('app',[]).run(function(){});

# 视图和路由
## ng-view
每次出发$routeChangeSuccess事件，视图就更新

## 路由
angular提供when和otherwise方法定义路由

app.module('app',[]).config(['$routeProvider',function($routeProvider){
$routerProvider.when('/',{
templateUrl:'views/index.html',
controller:'indexController'
}
}]

第一个参数是路径，$location.path;当前URL路径。
第二个参数是配置对象，决定路由具体做什么。

* controller
将当前路由与控制器的作用域进行关联。
* template 
把对象中的HTMl渲染到ng-view指令的DOM中
* templateUrl 
异步加载指定路径的视图（或是$templateCache中读取),把视图渲染到ng-view指令的DOM中。
* resolve
将列表中的元素注入到控制器中
* redirectTo:path  ; redirectTo:function(route,path,search)
目标跳转  
* reloadOnSearch

$routeParams 获取路由传递的参数(需要在控制器中注入)
app.controller('ctrl',function($scope,$routeParams){});
$location 对window.location封装  
不过$location不会重新加载整个页面，需要加载整个页面要用$window.location.href='/path'


## 路由模式
* 标签模式 (默认)
URl路径以#符号开头，http://localhost:63342/ui_pro/catalog/angular/index.html#/index
* HTML5模式 (链接地址必须是绝对路径 或是在head中加入<base url='' />)

## 路由事件
* $routeChangeStart
* $routeChangeSuccess
* $routeChangeError
* $routeUpdate
angular.module('app',[]).run(function($rootscope,$location){$rootScope.$on('$routeChangeError',function(current,previouse,rejection){})}));

# 服务 (service)
出于内存占用和性能的考虑，控制器只会在需要的时候实例化，并且不需要就销毁.每次切换路由或是重新加载视图时，angular会清除掉当前控制器  
服务是一个单例对象，每个应用中只被实例化一次，需要时才在家。用于数据的共享。  

## 注册服务
* factory(name,getFn)  第一个参数：服务名称，第二个参数：一个包含可被注入对象的数组或是函数
* service(name,constructor) 
* constant(name,value) 作为常量保存下来。 可以注入到函数中。
* value(value); 同constant,但不可以注入到函数中。
* provider



# 延迟接口 $q
* resolve(value) ——传入 value 解决派生的 promise。 如果 value 是一个通过 $q.reject 构造的拒绝对象(rejection) , 该promise 将被拒绝。  
* reject(reason) ——拒绝派生的promise,并提供原因 。 这相当于通过 $q.reject构造的拒绝对象(rejection)作为参数传递给 resolve。  
* notify(value)  ——在 promise 执行的过程中提供状态更新。 这在 promise 被解决或拒绝之前可能会被多次调用。  
deffered 对象的属性
promise – {Promise} —— 与延迟(deferred)相关联的 promise 对象。  

## $q
```
angular.module('job.models', [])
  .service('JobManager', ['$q', '$http', 'Job', function($q, $http, Job) {
    return {
      getAll: function(limit) {
        var deferred = $q.defer();

        $http.get('/api/jobs?limit=' + limit + '&full=true').success(function(data) {
          var jobs = [];
          for (var i = 0; i < data.objects.length; i ++) {
            jobs.push(new Job(data.objects[i]));
          }
          deferred.resolve(jobs);
        });

        return deferred.promise;
      }
    };
  }])
  .factory('Job', function() {
    function Job(data) {
      for (attr in data) {
        if (data.hasOwnProperty(attr))
          this[attr] = data[attr];
      }
    }

    Job.prototype.getResult = function() {
      if (this.status == 'complete') {
        if (this.passed === null) return "Finished";
        else if (this.passed === true) return "Pass";
        else if (this.passed === false) return "Fail";
      }
      else return "Running";
    };

    return Job;
  });
```

## $resource
```
angular.module('job.models', [])
  .factory('Job', ['$resource', function($resource) {
    var Job = $resource('/api/jobs/:jobId', { full: 'true', jobId: '@id' }, {
      query: {
        method: 'GET',
        isArray: false,
        transformResponse: function(data, header) {
          var wrapped = angular.fromJson(data);
          angular.forEach(wrapped.items, function(item, idx) {
            wrapped.items[idx] = new Job(item);
          });
          return wrapped;
        }
      }
    });

    Job.prototype.getResult = function() {
      if (this.status == 'complete') {
        if (this.passed === null) return "Finished";
        else if (this.passed === true) return "Pass";
        else if (this.passed === false) return "Fail";
      }
      else return "Running";
    };

    return Job;
  }]);
```
# 承诺接口 Promise
* then(successCallback, errorCallback, notifyCallback) ——不管 promise 是被处理还是被拒绝, 一旦结果可用,then 就会尽快地异步调用 成功/错误 回调函数 只要结果是可用的。这个方法 返回一个新的promise 对象, 根据 successCallback , errorCallback的返回值进行解决或拒绝 。 它还通过 notifyCallback 方法的返回值进行通知。
* catch(errorCallback) —— promise.then(null, errorCallback) 的快捷方式
* finally(callback) ——让你可以观察到一个 promise 是被执行还是被拒绝, 但这样做不用修改最后的 value值。 

#待续
# XHR

## promise对象
## $apply

angular.element($0).scope() 获取当前节点的scope
angular.fromJson(str);  将str转换json;
angular.toJson(obj,true);   将obj对象转换json字符串
