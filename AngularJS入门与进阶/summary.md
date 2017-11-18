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
