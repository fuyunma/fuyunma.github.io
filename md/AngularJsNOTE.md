#AngularJS
##1.AngularJS 调试工具为Chrome 添加扩展功能 AngularJS Batarang
    Chrome 浏览器打开 ———— 设置 ———— 扩展程序 ———— 输入AngularJS Batarang安装
##2.sublime 装上 AngularJS  同款工具webstorm
##3.Grunt 代码合并和混淆工具
    先按装node.js ———— npm install grunt
    网址 www.gruntjs.net
    grunt 插件  grunt-contrib-uglify 对代码进行混淆
                grunt-contrib-concat 合并代码
                grunt-contrib-watch  监视文件变化 
##4.bower 依赖管理工具
    网址：http://bower.io
    1.自动安装依赖的组件
    2.组件之间的依赖检查
    3.版本兼容性自动检测
    第一步npm install bower
    第二步bower install jquery
-------------------------------------------------------------------------------
### MVC 框架
    model 模块 view 视图 controller 控制器
##controller 
    1.不要视图复用controller ,一个控制器一般只是负责一小块视图；
    2.不要在controller中操作DOM，这不是控制器的职责；
    3.不要在controller中做数据格式化，ng有很好用的表单控件；
    4.不要在controller中做数据过滤工作，ng有$filter服务
    5.一般来说controller是不会互相调用的，控制器之间的交互会通过事件来进行
##AngularJS中的MVC是借助于 $scope 实现的
    1.$scope 是一个POJO  （plain Old javascript object）
    2.$scope 提供了$watch()/$apply()
    3.$scope 是表达式的执行环境（或者叫作用域）
    4.$scope 是一个树型结构，与DOM标签平行
    5.子$scope对象会继承父$scope上的属性和方法
    6.每一个Angular应用只有一个根$scope对象（一般位于ng-app上）
    7.$scope 可以传播时间，类似DOM事件，可以向上也可以向下
    8.$scope 不仅是MVC的基础，也是后面实现双向数据绑定的基础
    9.可以用angular.element($0).scope()进行测试
-------------------------------------------------------------------------------
## AngularJS 开始
# 1         
            <!DOCTYPE html>
            <html ng-app> // ng-app 告诉angular处理整个html
            <head>
                <meta charset="UTF-8">
                <title>Document</title>
            </head>
            <body>
                <p><input type="text" ng-model = "name"></p>
                <p>hello{{name}}</p> 
                //使用双大括号标记{{}} 通过大括号获取内容
                <script src = "angular.min.js"></script>
            </body>
            </html>
        注释：
           1. ng-app 指令告诉 AngularJS，<div> 元素是 AngularJS 应用程序 的"所有者"。
           2.ng-model 指令把输入域的值绑定到应用程序变量 name。
           3.ng-bind 指令把应用程序变量 name 绑定到某个段落的 innerHTML。
# 2
    HTML5 允许扩展的（自制的）属性，以 data- 开头。
    AngularJS 属性以 ng- 开头，但是您可以使用 data-ng- 来让网页对 HTML5 有效。
    <div data-ng-app="" data-ng-init="firstName='John'">
        <p>姓名为 <span data-ng-bind="firstName"></span></p>
    </div>
# AngularJS 表达式
    AngularJS 表达式写在双大括号内：{{ expression }}。
    AngularJS 表达式把数据绑定到 HTML，这与 ng-bind 指令有异曲同工之妙。
    AngularJS 将在表达式书写的位置"输出"数据。
    AngularJS 表达式 很像 JavaScript 表达式：它们可以包含文字、运算符和变量。
    <div ng-app="">
        <p>我的第一个表达式： {{ 5 + 5 }}</p>
    </div>
# AngularJS 应用
    AngularJS 模块（Module） 定义了 AngularJS 应用。
    AngularJS 控制器（Controller） 用于控制 AngularJS 应用。
    ng-app指令定义了应用, ng-controller 定义了控制器。
# AngularJS 指令
    ng-app 指令初始化一个 AngularJS 应用程序。
           指令定义了 AngularJS 应用程序的 根元素.
    ng-init 指令初始化应用程序数据。
            通常情况下，不使用 ng-init。您将使用一个控制器或模块来代替它
    ng-model 指令把元素值（比如输入域的值）绑定到应用程序。
             1.为应用程序数据提供类型验证（number、email、required）。
             2.为应用程序数据提供状态（invalid、dirty、touched、error）。
                Valid(如果输入的值是合法的则为 true)。
                    用法：{{myForm.myAddress.$valid}}
                Dirty(如果值改变则为 true)。
                Touched (如果通过触屏点击则为 true)
             3.为 HTML 元素提供 CSS 类。
             4.绑定 HTML 元素到 HTML 表单。
    ng-repeat 指令对于集合中（数组中）的每个项会 克隆一次 HTML 元素。
            例子：克隆数组
                  <div ng-app>
                        <div ng-init = "names=['li','zhang','wnag']"></div>
                        <div ng-repeat = "x in names">
                            <li> x </li>
                        </div>
                  </div>
## 创建自定义的指令 .directive
    要调用自定义指令，HTMl 元素上需要添加自定义指令名。
    使用驼峰命名法，runoobDirective, 但在使用它时需要以 - 分割, runoob-directive:
## 什么是脏检查
    脏检查：检查值是否发生了变化，而整个应用还没有同步该变化。
        $scope.$apply(
            function(){
                $scope.date = new Date();
            })
        },1000) 
## $watch
    在degest执行时，如果watch观察到value值与上一次不一样就会触发
    watch实现随着model的value值得改变而改变
    $watch("表达式或函数字符串"，"监听器函数",true)
            会在作用域中找到      检查当前值与之前的值是否相等，（除啦首次）
            true 作为可选参数 是确认angular 是否执行严格检查。

