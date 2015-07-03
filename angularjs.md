title: angularjs
author:
  name: Jordan Scales
  url: http://jordanscales.com
output: basic.html
--

# Angularjs
##由Google创建的一种JS框架，使用它可以扩展应用程序中的HTML词汇，从而在web应用程序中使用HTML声明动态内容。

--
##概念
模块、控制器、服务、过滤器和指令
依赖注入（DI），注入器（Injector）和服务提供者（Providers）

依赖注入是AngularJS的核心特性，所以你必须要知道一点这家伙是怎么工作的。
依赖注入（DI）是一个软件设计模式，处理代码如何得到它所依赖的资源。
--

##模块 
```
angular.module('yourAppName', ['yourAppDep']);
```

--

##指令
对指令使用app专用的前缀，这有助于避免与第三方的组件重名。
```
angular.module('yourAppDep').directive('btlaControlPanel', function () {
     // ...
});
```
--
##service controller directive
那么我们什么时候应该使用service呢？答案是：无论何时，当我们需要在不同的域中共享数据的时候。另外，多亏了Angular的依赖注入系统，实现这一点是很容易并且很清晰的。

[**何时应该使用Directive、Controller、Service](http://damoqiongqiu.iteye.com/blog/1971204)
--
##常用方法
$apply() $watch  $comple()编译函数  $digest  link()连接函数

    scope.$watch(attr.currentTime, function (value) {
        scope.format = value;
        updateTime();
    });
link function负责注册DOM事件监听器，也可以进行DOM的更新操作。link function会在模版克隆操作完毕之后执行。这里存放着directive大多数的逻辑。
--
##服务
```
angular.module('yourAppDep').service('MyCtrl', function () {
     // ...
});
```
--
##事件监听

[事件监听](http://damoqiongqiu.iteye.com/blog/1971204)
--
##模型
AngularJS作为JavaScript框架，其独到之处就在于让你可以完全掌控模型层
```
angular.module('yourAppDep').controller('MyCtrl', function () {
     // ...
});
```

--
##scope
关联的scope，我们可以在console中输入：angular.element($0).scope()
--
##directive(指示器)
restrict - EACM的子集的字符串，它限制directive为指定的声明方式。如果省略的话，directive将仅仅允许通过属性声明：
 

E - 元素名称： <my-directive></my-directive>
 

A - 属性名： <div my-directive=”exp”></div>
 

C - class名： <div class=”my-directive:exp;”></div>
 

M - 注释 ： <!-- directive: my-directive exp -->

[directive定义对象说明](http://www.cnblogs.com/lcllao/archive/2012/09/09/2677190.html)
[demo](http://msf.tudou.com/ng/directive_time.html)
--
##HTML“编译”的三个步骤：
```
　　1. 首先，通过浏览器的标准API，将HTML转换为DOM对象。这是很重要的一步。因为模版必须是可解析（符合规范）的HTML。这里可以跟大多数的模版系统做对比，它们一般是基于字符串的，而不是基于DOM元素的。

　　2. 对DOM的编译（compilation）是通过调用$comple()方法完成的。这个方法遍历DOM，对directive进行匹配。如果匹配成功，那么它将与对应的DOM一起，加入到directive列表中。只要所有与指定DOM关联的directive被识别出来，他们将按照优先级排序，并按照这个顺序执行他们的compile() 函数。directive的编译函数（compile function），拥有一个修改DOM结构的机会，并负责产生link() function的解析。$compile()方法返回一个组合的linking function，是所有directive自身的compile function返回的linking function的集合。

　　3. 通过上一步返回的linking function，将模版与scope连接起来。这反过来会调用directive自身的linking function，允许它们在元素上注册一些监听器（listener），以及与scope一起建立一些watches。这样得出的结果，是在scope与DOM之间的一个双向、即时的绑定。scope发生改变时，DOM会得到对应的响应。
```
--
##区别
AngularJS与标准AJAX应用程序不同，您不需要另外编写侦听器或DOM控制器，因为它们已经内置到AngularJS中了

Angular编译器（compiler）通过directives处理DOM，而不是通过处理字符串模版。处理结果是一个与scope model组合并生成实时模版的链接函数（linking function）。

视图与scope model的绑定对我们来说是透明的。
--
##基础
双向数据绑定
`文本输入指令<input ng-model="yourname" />`绑定到一个叫yourname的模型变量。
--
##绑定
--
##脚本
*ng-app指令标记了AngularJS脚本的作用域
*AngularJS的作用域理论非常重要：一个作用域可以视作模板、模型和控制器协同工作的粘接器

*视图，路由和布局模板(深链接)
AngularJS中应用的路由通过$routeProvider来声明，它是$route服务的提供者。这项服务使得控制器、视图模板与当前浏览器的URL可以轻易集成。

$route服务通常和ngView指令一起使用。ngView指令的角色是为当前路由把对应的视图模板载入到布局模板中
--
##环境
Yeoman是由Paul Irish、Addy Osmani、Sindre Sorhus、Mickael Daniel、Eric Bidelman和Yeoman社区共同开发的一个项目.
它旨在为开发者提供一系列健壮的工具、程序库和工作流，帮助他们快速构建出漂亮、引人注目的Web应用。
[yeoman](http://yeoman.io/learning/index.html)

--
##实战练习

[实战练习](http://localhost:8000/app/index.html)
[git](https://github.com/angular/angular-phonecat)
npm start

--
##注意
作为一个命名习惯，AngularJS内建服务，作用域方法，以及一些其他的AngularJS API都在名字前面使用一个‘$’前缀。
不要使用‘$’前缀来命名你自己的服务和模型，否则可能会产生名字冲突。

由于AngularJS是通过控制器构造函数的参数名字来推断依赖服务名称的。所以如果你要压缩PhoneListCtrl控制器的JS代码，它所有的参数也同时会被压缩，这时候依赖注入系统就不能正确的识别出服务了。


只要是在Angular execution context 里面执行的操作，都拥有angular data-binding、异常处理（exception handling）、属性监视（property watching）等能力。我们可以通过在javascript使用$apply()，进入Angular execution context。
--
##参考
[入门教程](http://www.ituring.com.cn/article/13471)
[angular Runtime](http://www.cnblogs.com/lcllao/archive/2012/09/07/2671227.html)
[angularjs learning](https://github.com/jmcunningham/AngularJS-Learning/blob/master/ZH-CN.md)
