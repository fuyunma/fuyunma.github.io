##AngularJs:Controller数据共享、继承、通信使用详解

###一、controller基础与用法

    AngularJS中的controller中文名就是控制器，它是一个Javascript函数（类型/类），用来向视图的作用域（$scope）添加额外的功能。而且每个controller都有自己的scope， 同时也可以共享他们父controller的scope内的数据。

	其能实现的功能如下：

####（1）给作用域对象设置初始状态

	你可以通过创建一个模型属性来设置初始作用域的初始状态。 比如:

	var app = angular.module('myApp', []);  
	app.controller('myController', function($scope) {  
    	$scope.inputValue = "林炳文Evankaka";  
	});  
	
	上面我们设置了一个inputValue，如果要在html页面中使用，就可以直接用{{inputValue}},如下：

	<h1>您输入的内容为：{{inputValue}}</h1>
	
	当然，你也可以将此数据双向绑定到一个input、select等，如下：

	<input  type="text" ng-model = "inputValue"> 

####（2）给作用域对象增加行为
	
	AngularJS作用域对象的行为是由作用域的方法来表示的。这些方法是可以在模板或者说视图中调用的。这些方法和应用模型交互，并且能改变模型。

	如我们在模型那一章所说的，任何对象（或者原生的类型）被赋给作用域后就会变成模型。任何赋给作用域的方法，都能在模板或者说视图中被调用，并且能通过表达式或者ng事件指令调用。如下：

	var app = angular.module('myApp', []);  
	app.controller('myController', function($scope) {  
	    $scope.myClick = function(){  
	        alert("click");  
	    }  
	});

	然后页面上使用：

	<button ng-click= "myClick()" ></button>

	这样就给button添加了一个点击事件。

###二、controller继承

    这里说的继承一般说的是scope数据，这是因为子控制器的作用域将会原型继承父控制器的作用域。因此当你需要重用来自父控制器中的功能时，你所要做的就是在父作用域中添加相应的方法。这样一来，自控制器将会通过它的作用域的原型来获取父作用域中的所有方法。

    如下实例：

    <!DOCTYPE html>  
    <html lang="zh" ng-app="myApp">  
    <head>  
        <meta charset="UTF-8">  
        <title>AngularJS入门学习</title>  
        <script type="text/javascript"  src="./1.5.3/angular.min.js"></script>  
    </head>  
    <body>  
        <div ng-controller = "parentCtrl">  
            <p><input  type="text" ng-model = "value1">请输入内容</p>  
            <h1>您输入的内容为：{{value1}}</h1>  
              <div ng-controller = "childCtrl">  
                <button ng-click = "gerParentValue()"></button>  
              </div>  
        </div>  
      
    </body>  
    <script type="text/javascript">  
    var app = angular.module('myApp', []);//获得整个angularJS影响的html元素  
    app.controller('parentCtrl',function($scope){  
        $scope.value2 = "我是林炳文";  
    });    
      
    app.controller('childCtrl',function($scope){  
        $scope.gerParentValue = function() {  
            alert($scope.value1 + $scope.value2);  
        }  
    });   
    </script>  
    </html>  

    这里需要注意的是childCtrl所在的DIV一定要放在parentCtrl所在的DIV里才会生效！而且如果你需要从父控制器中调用子控制器的方法，那么使用上面的代码会发生错误。

###三、controller之间共享数据

####(1)在父级controller中定义scope,子级共用

    <!DOCTYPE html>  
    <html lang="zh" ng-app="myApp">  
    <head>  
        <meta charset="UTF-8">  
        <title>AngularJS入门学习</title>  
        <script type="text/javascript" src="./1.5.3/angular.min.js"></script>  
    </head>  
    <body>  
       <div  ng-controller="paretnCtrl">  
         <input type="text" ng-model="name" />  
         <div ng-controller="childCtrl1">  
            {{name}}  
            <button ng-click="setName()">set name to jack jack jack</button>  
         </div>  
         <div ng-controller="childCtrl2">  
            {{name}}  
            <button ng-click="setName()">set name to tom tom tom</button>  
         </div>  
       </div>  
    </body>  
    <script type="text/javascript">  
    var app = angular.module('myApp', []);  
    app.controller('paretnCtrl', function($scope,$timeout) {  
        $scope.name = "林炳文Evankaka";  
    });  
    app.controller('childCtrl1', function($scope,$timeout) {  
        $scope.setName = function() {  
             $scope.name = "set name to jack jack jack";  
        };  
    });  
    app.controller('childCtrl2', function($scope,$timeout) {  
        $scope.setName = function() {  
            $scope.name = "set name to tom tom tom";  
        };  
    });  
    </script>  
    </html>

####（2）将数据全局共享

    angularjs自身有二种，设置全局变量的方法，在加上js的设置全局变量的方法，总共有三种。要实现的功能是，在ng-app中定义的全局变量，在不同的ng-controller里都可以使用。

    通过var 直接定义global variable，这根纯js是一样的。
    用angularjs value来设置全局变量 。
    用angularjs constant来设置全局变量 。

    下面是使用value的方式

    <!DOCTYPE html>  
    <html lang="zh" ng-app="myApp">  
    <head>  
        <meta charset="UTF-8">  
        <title>AngularJS入门学习</title>  
        <script type="text/javascript" src="./1.5.3/angular.min.js"></script>  
    </head>  
    <body>  
         <div ng-controller="childCtrl1">  
            {{name}}  
            <button ng-click="setName()">set name to jack jack jack</button>  
         </div>  
         <div ng-controller="childCtrl2">  
            {{name}}  
            <button ng-click="setName()">set name to tom tom tom</button>  
         </div>  
    </body>  
    <script type="text/javascript">  
    var app = angular.module('myApp', []);  
    app.value('data',{'name':'我是林炳文'});  
    app.controller('childCtrl1', function($scope,data) {  
        $scope.name = data.name;  
        $scope.setName = function() {  
             $scope.name = "set name to jack jack jack";  
        };  
    });  
    app.controller('childCtrl2', function($scope,data) {  
           $scope.name = data.name;  
           $scope.setName = function() {  
            $scope.name = "set name to tom tom tom";  
        };  
    });  
    </script>  
    </html>

####（3）service依赖注入
    angularjs最突出的特殊之一就是DI，也就是注入，利用service把需要共享的数据注入给需要的controller。这是最好的方法

    <!DOCTYPE html>  
    <html lang="zh" ng-app="myApp">  
    <head>  
        <meta charset="UTF-8">  
        <title>AngularJS入门学习</title>  
        <script type="text/javascript" src="./1.5.3/angular.min.js"></script>  
    </head>  
    <body>  
         <div ng-controller="childCtrl1">  
            {{name}}  
            <button ng-click="setName()">set name to jack jack jack</button>  
         </div>  
         <div ng-controller="childCtrl2">  
            {{name}}  
            <button ng-click="setName()">set name to tom tom tom</button>  
         </div>  
    </body>  
    <script type="text/javascript">  
    var app = angular.module('myApp', []);  
    app.factory('dataService', function() {  
      var service = {  
         name:'我是林炳文'  
       };  
       return service;  
    });  
    app.controller('childCtrl1', function($scope,dataService) {  
        $scope.name = dataService.name;  
        $scope.setName = function() {  
             $scope.name = "set name to jack jack jack";  
        };  
    });  
    app.controller('childCtrl2', function($scope,dataService) {  
           $scope.name = dataService.name;  
           $scope.setName = function() {  
            $scope.name = "set name to tom tom tom";  
        };  
    });  
    </script>  
    </html>

###四、controller之间通信

    在一般情况下基于继承的方式已经足够满足大部分情况了，但是这种方式没有实现兄弟控制器之间的通信方式，所以引出了事件的方式。

    基于事件的方式中我们可以里面作用的$on,$emit,$boardcast这几个方式来实现，其中$on表示事件监听，$emit表示向父级以上的作用域触发事件，$boardcast表示向子级以下的作用域广播事件。

    $emit只能向parent controller传递event与data
    $broadcast只能向child controller传递event与data
    $on用于接收event与data

####实例一：

    <!DOCTYPE html>  
    <html lang="zh" ng-app="myApp">  
    <head>  
        <meta charset="UTF-8">  
        <title>AngularJS入门学习</title>  
        <script type="text/javascript" src="./1.5.3/angular.min.js"></script>  
    </head>  
    <body>  
    <div ng-app="app" ng-controller="parentCtr">  
         <div ng-controller="childCtr1">childCtr1 name :  
             <input ng-model="name" type="text" ng-change="change(name)" />  
        </div>  
         <div ng-controller="childCtr2">from childCtr1 name:  
             <input ng-model="ctr1Name" />  
         </div>  
    </div>  
    </body>  
    <script type="text/javascript">  
    var app = angular.module('myApp', []);  
    app.controller("parentCtr",function ($scope) {  
        $scope.$on("Ctr1NameChange",function (event, msg) {//接收到来自子childCtr1的信息后再广播给所有子controller  
            console.log("parent", msg);  
            $scope.$broadcast("Ctr1NameChangeFromParrent", msg);//给所有子controller广播  
        });  
    });  
    app.controller("childCtr1", function ($scope) {  
        $scope.change = function (name) {  
            console.log("childCtr1", name);  
            $scope.$emit("Ctr1NameChange", name);//将信息传递给父controller  
        };  
    }).controller("childCtr2", function ($scope) {  
        $scope.$on("Ctr1NameChangeFromParrent",function (event, msg) { //监听来自父controller的信息  
            console.log("childCtr2", msg);  
            $scope.ctr1Name = msg;  
        });  
    });  
    </script>  
    </html>

####实例二：

    <!DOCTYPE html>  
    <html lang="zh" ng-app="myApp">  
    <head>  
        <meta charset="UTF-8">  
        <title>AngularJS入门学习</title>  
        <script type="text/javascript" src="./1.5.3/angular.min.js"></script>  
    </head>  
    <body>  
    <div ng-controller="ParentCtrl">                <!--父级-->  
        <div ng-controller="SelfCtrl">              <!--自己-->  
             <button ng-click="click()">click me</button>  
            <div ng-controller="ChildCtrl">  
                  
            </div>   <!--子级-->  
        </div>  
        <div ng-controller="BroCtrl">  
              
        </div>         <!--平级-->  
    </div>  
    </body>  
    <script type="text/javascript">  
    var app = angular.module('myApp', []);  
    app.controller('SelfCtrl', function($scope) {  
      $scope.click = function () {  
        $scope.$broadcast('to-child', 'child');  
        $scope.$emit('to-parent', 'parent');  
      }  
    });  
      
    app.controller('ParentCtrl', function($scope) {  
      $scope.$on('to-parent', function(event,data) {  
        console.log('ParentCtrl', data);       //父级能得到值  
      });  
      $scope.$on('to-child', function(event,data) {  
        console.log('ParentCtrl', data);       //子级得不到值  
      });  
    });  
      
    app.controller('ChildCtrl', function($scope){  
      $scope.$on('to-child', function(event,data) {  
        console.log('ChildCtrl', data);      //子级能得到值  
      });  
      $scope.$on('to-parent', function(event,data) {  
        console.log('ChildCtrl', data);      //父级得不到值  
      });  
    });  
      
    app.controller('BroCtrl', function($scope){    
      $scope.$on('to-parent', function(event,data) {    
        console.log('BroCtrl', data);         //平级得不到值    
      });    
      $scope.$on('to-child', function(event,data) {    
        console.log('BroCtrl', data);         //平级得不到值    
      });    
    });  
    </script>  
    </html>

    $emit和$broadcast可以传多个参数，$on也可以接收多个参数。

    ***在$on的方法中的event事件参数，其对象的属性和方法如下

    事件属性                            目的
    event.targetScope                   发出或者传播原始事件的作用域
    event.currentScope                  目前正在处理的事件的作用域
    event.name                          事件名称
    event.stopPropagation()             一个防止事件进一步传播(冒泡/捕获)
                                        的函数(这只适用于使用`$emit`发出的事件)
    event.preventDefault()              这个方法实际上不会做什么事，但是会设置
                                        `defaultPrevented`为true。直到事件监听器的实现者采取行动之前它才会检查`defaultPrevented`的值。
    event.defaultPrevented              如果调用

###五、 对于controller层的一些建议

    1、controller层不要涉及到太多的业务逻辑，可以将公用的部分抽取到Service层
    2、service层：主要负责数据交互和数据处理、处理一些业务领域上的逻辑；
    3、controller层：主要负责初始化$scope的变量用于传递给view层，并且处理一些页面交互产生的逻辑;
    4、当一个功能是设计远程API调用、数据集、业务领悟复杂逻辑、将会大量重复的运算方法时就可以考虑将代码以service形式注入controller层。
    5、controller 里的 $scope 是唯一页面数据来源。不要直接修改 DOM。
    6、controller 不要在全局范围

###参考文章：
    http://www.jianshu.com/p/1e1aaf0fd30a
    http://cnodejs.org/topic/54dd47fa7939ece1281aa54f
    http://www.html-js.com/article/1847
    http://blog.51yip.com/jsjquery/1601.html
    http://www.cnblogs.com/CraryPrimitiveMan/p/3679552.html?utm_source=tuicool&utm_medium=referral
    http://www.cnblogs.com/whitewolf/archive/2013/04/16/3024843.html