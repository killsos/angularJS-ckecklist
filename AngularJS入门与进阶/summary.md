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

```
{{expression}}
```

* 表达式中四则运算

表达式支持加减乘除四则运算 字符串拼接运算

* 表达式支持逻辑运算

* 表达式可以访问作用域中的数据
