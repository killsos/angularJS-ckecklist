## 1 简介

1. HTML标签中尖括号的英文为angular brackets 这便是AngularJS名称的来源

2. ng-app
> 启动angular框架  告诉angular框架从ng-app指令所在标签的开始标签到结束标签之间的所有DOM元素由angular框架进行管理

3. {{}} 表达式形式

4. angular构造要素

* model 模型  展现页面上数据

* view 视图 angular指令与表达式解析后的DOM元素

* controller 控制器  处理业务逻辑

* scope 作用域 可以理解为容器 这个容器存放着模型数据  控制器可以访问的容器

* directive 指令 扩展的HTML属性或标签 根据不同指令执行相应的动作

* expression 表达式 用于页面输出信息

* 模板 template HTML片段

5. angularjs 表达式

* 表达式的定义

```javascript
{{expression}}
```

* 表达式中四则运算

表达式支持加减乘除四则运算 字符串拼接运算

* 表达式支持逻辑运算

* 表达式可以访问作用域中的数据

## 2 双向数据绑定

1. 数据绑定是angular框架在视图与作用域之间建立的数据同步机制

> 所谓双向 指界面的操作能够实时同步到作用域中,作用域中的数据修改也能够实时回显到页面中。  

> 作用域可以视为一个容器 里面有一些基于key-value的数据  

2. ng-model 指令

只能用在表单元素 input

> angular遇到ng-app指令时就会创建一个名为$rootScope的作用域 该作用域为angular应用的根作用域

3. ng-bind 指令

> angular没有加载完成的时候不会执行

## 3 angular与MVC

1. MVC简介

> MVC是一种软件架构模式 独立于任何一门语言 1970 起源于smalltalk语言  

> MVC是model 模型 view 视图 controller 控制器

> 核心思想是数据的管理 业务逻辑 数据展示 使程序的逻辑性和可维护性更强

2. angular mvw

> mvw model-view-whatever $scope可以认为是由一个方法controller包装后的viewmodel mvvw

3. angular 控制器 controller

> 控制器是构造器方法 控制器附在model上 

> 控制器名称 匿名函数(依赖对象)

> 控制器实例化使用指令ng-controller  当angular框架遇到ng-controller指令时会根据控制器名称 去找控制器的构造方法 然后实例化控制器 并将控制器依赖的对象注入控制器对象中

> ng-controller指令还支持使用as语法指定控制器的名称

> 需要注意是 每个控制器对应的作用域对象只能与ng-controller指令所在开始标签与结束标签之间DOM元素建立数据绑定

## 4 angular模块

1. angular框架在window对象下新增一个全局angular对象 

2. angular对象调用module方法返回一个模块实例

```javascript
// 定义一个无依赖模块
angular.module('app', []);

// 定义一个依赖module1 module2的模块
angular.module('app', ['module1', 'module2']);
```

3. 模块下可以调用controller directive filter等方法

## 4 作用域与事件

1. angular启动自动会创建一个$rootScope根作用域 controller实例化时候 会创建$scope子作用域 子作用域的原型是根作用域  

2. 作用域继承

* 构造方法命名是帕斯卡 每个单词首字母全部大写

* 函数命名是驼峰 每个单词首字母全部大写 但是首字母小写

* 构造方法原型继承

* apply call实现继承

* 对象实例间继承 Object.create() Object.getPrototypeOf()

3. angular作用域构造方法提供$new()方法 用于创建一个子作用域
 
4. angular作用域解析

* angular作用域构造器中提供一个$new方法 用于创建子作用域

* 所用作用域对象都是$rootScope的孩子

* ng-controller嵌套解析
  1. angular框架遍历DOM元素 查找到ng-app指令时启动应用 创建$rootScope作用域

  2. angular框架遇到第一个ng-controller 会创建一个controller实例 同时调用$rootScope.$new()方法 以原型继承的方式创建$rootScope作用域的子作用域对象$scope1

  3. 当angular继续遍历DOM元素 如果遇到控制器 会再创建一个controller实例 同时调用$scope1.$new()方法 生成一个$scope2实例 $scope2以原型方式继承$scope1.... 以此类推

5. $watch监视方法

* 当angular的scope发生修改时候会内部启动一次$digest循环就会运行一次,然后执行watch的方法

* 当angular的watch方法中,对基本类型与引用类型有所不同

* watch函数三个参数 属性名称 回调函数 引用监视(false)

* 引用监视 reference watch 就是说只要监视对象的引用没有发生变化 就不算发生变化

* 引用监视设为true 全等监视 equality watch 只要监视对象的属性发生变化

* 每次digest之前使用Angular.copy()方法将整个作用域对象深复制一遍,然后在运行之后用Angular.equal()将前后的作用域对象进行对比

* watchCollection 不会监控数组内容变化 只监控数组的长度

* watch方法会一个watchID 便于解除监控

* digest循环 周期性运行一个函数来检查scope模型中的数据是否发生变化这就是所谓digest循环

* digest循环什么时候开始？ 当调用$scope.$digest()后 $digest循环就开始了，当ng-click指令对应处理方法更改scope上数据 此时angular会自动调用digest来触发一轮digest循环。 当digest循环开始后 会触发每一个watcher

* angular内置指令和内置服务来让更改作用域的数据后会自动触发一次digest循环

6. $apply

* 当angular作用域中的模型数据发生变化时，angular会自动触发digest循环 从而达到自动更新视图的目的

* 但有情况下, 模型数据修改后需要手动调用apply方法来触发digest循环，将修改数据方法封装到函数中 而这个函数就是apply的参数

7. $timeout $interval

* 内置指令或服务会自动apply方法

8. 作用域事件路由与广播

* angular作用域有事件转播机制

* angular作用域支持事件传播方式:
    1. 事件从子作用域路由到父作用域
    2. 事件从父作用域路由到子作用域

* $emit 子到父

* $broadcast 父到子

* $on 注册事件 function event data 

* event.name event.targetScope event.currentScope event.stopPropagation()  event.preventDefault() 设置 event.defaultPrevented

## 6 路由与多视图

1. $routerProvider对象用于创建路由映射

* $routerProvider提供when  otherwise方法

2. when(path, route) 

> path

> route 对象类型 该对象用于配置映射信息  controller controllerAs template templateUrl  resolve---用于指定注入控制器的内容

3. otherwise 

4. angular路由模块作为一个单独的模块 模块名称为ngRoute 需要添加ngRoute模块依赖

```javascript
var routeModule = angular.module('routeModule', ['ngRoute']);
```

5. $location

* search方法

* hash方法

* changestart  调用preventDefault方法 不会触发changeSucces方法

* changeSuccess

6. $route

* changestart

* changesuccess

* changeerror

7. ng-include指令


8. UI Router 

* 是基于angular的 用于编写单页面应用的路由框架 支持多视图嵌套和多个命名视图

* 注入[ui.router]

* $stateProvider $urlProvider 

* $stateProvider url templateUrl controller 

## 7 表单

## 8 angular指令

1. 指令形式 元素 属性 样式 注释

2. 内置指令 ng开头 ng-app ng-model ng-init ng-controller ng-disabled ng-checked ng-change ng-class ng-show/hide ng-bind ng-if ng-switch ng-repeat ng-href/src ng-include

3. 自定义指令

* 模块对象有一个directive方法实现自定义指令

* directive 第一个参数指令名称 采用驼峰式命名法 第二个参数为指令定义方法 返回一个对象 

* restrict  元素 属性 样式 注释  EACM

* replace 指定是否使用template属性定义的HTML模板内容替换指令所在的HTML元素

* template 用于指定HTML模板

* templateUrl

4. link方法

* 三个参数 scope elem attrs 

* elem 是JQLite封装对象

* attrs 对象

* 需要获取或修改自定义指令属性

* 当指令需要监视angular作用域模型数据变化

* 指令需要响应HTML模板中元素单击 鼠标移动等时间

5. compile方法

* 浏览器开始渲染HTML页面时,首选加载HTML元素，创建文档对象模型(DOM),加载完成后会触发onload事件，通过script标签将angular引入HTML页面中, angular会监听onload事件 然后从DOM元素中查找ng-app指令 如果找到就启动angular 接着从ng-app指令所在的标签开始使用$compile服务遍历DOM元素. 我们使用的指令directive方法注册的指令都会保存一个容器中,angular会从这些DOM元素中识别哪些属于指令元素,angular会根据指令定义对象compile方法。

* 所有指令的compile方法只会在angular框架启动时调用一次

* compile 两个参数 elem---指令所在元素 attrs 指令元素的所有属性列表

* compile与link如果有冲突 link方法可以由compile方法作为返回值返回 如果没有指定compile方法 就可以正常使用link方法

* compile作用是link方法执行之前对DOM元素进行修改


## 9 scope属性与指令作用域

1. 默认情况下 指令直接使用父作用域

2. 某个指令对作用域模型数据的修改会其他指令有影响 我们希望指令能够彻底摆脱父控制器的作用域，这样我们就可以对作用域中的数据进行任意修改，而且在一些情况下我们需要在作用域中添加一些模型数据仅供指令内部使用

3. 摆脱父作用域: 1 使用子作用域从父作用域原型继承   2 使用孤立作用域 即创建一个新的作用域对象和父作用域没有任何关系

```javascript
scope: true 是第一种

scope: {} 是第二种
```

4. 孤立作用域与父作用域模型数据绑定

* @符号建立基于属性绑定

* =符号建立双向绑定

* &调用父作用域的方法

5. transclusion

* 是指将整个或部分文档通过超文本引用包含到其他单个或多个文档中

* 指令定义属性transclude设为true element

* link方法第三个参数 transclusion

* link方法第四个参数 $ctrl

## 10 service factory provider

1. service

* service是封装了一些特定业务逻辑的单例对象, 单例对象就意味着在每个应用只会被实例化一次(由$injector实例化),并且是延迟加载(需要时才会被创建),它对外提供一些方法供其他组件调用。例如$timeout对象 angularjs30个内置对service象 

* module的service方法 名称 service对象的构造方法

2. factory

* factroy是angular一种可注入类型

* module的Factory方法 本质与service没太大的区别

* service方法中调用factory方法,在factory方法中通过$injector的instantiate()方法实例化service对象


3. provider

* provider是服务提供者 是一种灵活的可注入的类型 在使用之前我们可以调用模块实例的config()方法对provider进行配置


4. value与constant

* 模块实例的value和constant两者方法


## 11 过滤器

1. 表达式中使用过滤器

2. 指令中使用过滤器

3. controller或服务service factory provider中过滤器

4. $filter服务

5. 模块实例的filter()方法

6. 自定义 funtion(){
  return function (input) {
    return value;
  }
}

## 12 angular的依赖注入

1. 依赖注入 DI dependency injection  与 控制反转 inversion of control IoC

2. 控制反转是一种软件设计思想 而依赖注入是实现控制反转的最直接 最简单方法 当然控制反转也不一定非要通过依赖注入这种方式实现不可

3. 所谓依赖注入 就是当你在一个组件中需要依赖其他组件时 不需要你自己创建这些组件 而是通过注入的方式直接把这些组件提供给你

4. 一般情况下 获取依赖可以通过3种方式完成,分别为创建依赖 全局查找依赖 依赖注入 具体如下:

* 使用new操作符创建依赖

* 通过全局变量查找依赖

* 依赖需要时被注入

5. 依赖注入的实现

* 1 首先就要知道 作为一个构造方法 依赖那些对象 这一点我们可以从构造方法的参数得知 因此我们第一步就是要获取构造方法的参数名称

* 2 调用toString()方法时,返回函数的源码字符串

* 3 通过正则表达式匹配函数的参数可以获取参数名称

* 4 依赖容器对象  Bottle.js  Di.js 

6. 三种依赖注入方式

* 1 通过数组标注在方法的参数声明依赖

* 2 $inject属性注入 控制器构造函数添加一个$inject属性

* 3 隐式声明依赖

7. $provide服务

* $provide.provider()方法 const value service factory 

* $provide.provider(name,  function() {
  this.$get = function() {
    return function(){}
  }
})

* mod.config(function($provide){
  $provide.service(name, function(){

  })
})

* mod.service(name, function(){
    
})

8. $injector 

* $injector服务实际上就一个IoC容器 当我们创建一个新的可注入类型 例如service  factroy等 这些可注入类型会注册到IoC容器中

* angular通过$injector服务队这些可注入类型进行集中管理 这也就意味着我们可以通过$injector服务获取所有的可注入类型

* $injector服务提供get()方法用于从IoC容器中获取可注入对象,使用方法 $injector.get(servicename)

## 13 cookie
0. angular-cookie.js

1. ngCookies


## 14 promise

1. promise概念最初被提出是E语言中

2. $q $q.defer()获取derferred对象

3. derferred对象有resolve reject notify 

## 15 $http 

1. method url params  data headers ....

## 16 $resource

1. $resource是对$http的封装

## 17 angular UI

1. angular-ui-bootstrap

