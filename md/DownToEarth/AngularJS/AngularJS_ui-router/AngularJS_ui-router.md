## AngularJS——ui-router详解

### 1.配置使用ui-router

##### 1.1导入js文件

###### 需要注意的是：必须导入angular.min.js这个文件，且angular.min.js必须导入在angular-ui-router.min.js前面。

```JavaScript
<script type="text/javascript" src="JS/angular.min.js"></script>
<script type="text/javascript" src="JS/angular-ui-router.min.js"></script>
```

##### 1.2注入angular模块

```JavaScript
var app = angular.module('myApp', ['ui.router']);
```

注入的名字“ui.router”，可在angular-ui-router.min.js里找到，如下图： 

![](img/ui-router.png)

##### 1.3定义视图

ui-view替代的是ngroute路由的ng-view。

```JavaScript
<div ui-view></div>
```

##### 1.4配置路由状态

```JavaScript
app.config(["$stateProvider", function ($stateProvider){       
    $stateProvider     
    .state("home", { //导航用的名字，如<a ui-sref="login">login</a>里的login
        url: '/',    //访问路径 
        template:'<div>模板内容......</div>'
    })      
 }]);
```

### 2.Demo

```Html
<html>
  <head>   
    <title>ui-router</title>
    <meta http-equiv="pragma" content="no-cache">
    <meta http-equiv="cache-control" content="no-cache">
    <meta http-equiv="expires" content="0">    
    <meta http-equiv="keywords" content="keyword1,keyword2,keyword3">
    <meta http-equiv="description" content="This is my page">
    <!-- 导入JS -->
    <script type="text/javascript" src="JS/angular.min.js"></script>
    <script type="text/javascript" src="JS/angular-ui-router.min.js"></script>  
  </head>

  <body >   
    <div ng-app="myApp">        
        <div ui-view></div> <!-- 视图 -->     
    </div>  
  </body>

  <script type="text/javascript">
    //定义模板，并注入ui-router
    var app = angular.module('myApp', ['ui.router']);   
    //对服务进行参数初始化，这里配stateProvider服务的视图控制
    app.config(["$stateProvider",  function ($stateProvider) {      
        $stateProvider     
        .state("home", {
            url: '/',   
            template:'<div>模板内容......</div>'
        })     
    }]);  
  </script>
</html>
```

### 3.嵌套路由的实现

通过url参数的设置实现路由的嵌套（父路由与子路由通过"."连接就形成了子路由）。嵌套路由可实现多层次的ui-view。

```JavaScript
  <body>    
    <div ng-app="myApp" >
        <a ui-sref="parent">点我显示父view内容</a>
        <a ui-sref="parent.child">点我显示父view与子view内容</a>
        <div ui-view></div> <!-- 父View -->      
    </div>  
  </body>

  <script type="text/javascript">
    var app = angular.module('myApp', ['ui.router']);   
    app.config(["$stateProvider",  function ($stateProvider) {      
        $stateProvider     
        .state("parent", {//父路由
            url: '/parent',  
            template:'<div>parent'
                    +'<div ui-view><div>'// 子View
                    +'</div>'
        })      
        .state("parent.child", {//子路由
            url: '/child',    
            template:'<div>child</div>'
        })     
    }]);
  </script>
```

#####上面的是相对路径方式： 
‘parent’将匹配…./index.html#/parent；
#####‘parent.child’将匹配…./index.html#/parent/child。 

#####若改成绝对路径方式，则需要在子url里加上^:

```JavaScript
.state("parent.child", {
    url: '^/child',    
    template:'<div>child</div>'
}) 
```

此时，‘parent’将匹配…./index.html#/parent； 
#####‘parent.child’将匹配…./index.html#/child。

### 4. 通过views实现多视图

多个视图时，使用views属性。该属性里包含了哪些ui-view，则对应的template或templateUrl里的内容就会填充该ui-view。

同一个状态下有多个视图示例：

```JavaScript
  <body>    
    <div ng-app="myApp">
        <a ui-sref="index">点我显示index内容</a>
        <div ui-view="header"></div>  
        <div ui-view="nav"></div>  
        <div ui-view="body"></div>      
    </div>  
  </body>

  <script type="text/javascript">
    var app = angular.module('myApp', ['ui.router']);   
    app.config(["$stateProvider",  function($stateProvider) {      
        $stateProvider     
        .state("index", {
            url: '/index',  
            views:{
                'header':{template:"<div>头部内容</div>"},
                'nav':{template:"<div>菜单内容</div>"},
                'body':{template:"<div>展示内容</div>"}
            }
        })
    }]);
  </script>
```

### 5.ui-view的定位

@的作用是用来绝对定位view，即说明该ui-view属于哪个模板。如：'header@index'表示名为header的view属于index模板。绝对和相对路径的效果一样，请看如下代码：

```JavaScript
  <body>    
    <div ng-app="myApp">
        <a ui-sref="index">show index</a>
        <a ui-sref="index.content1">content111111</a>
        <a ui-sref="index.content2">content222222</a>
        <div ui-view="index"><div>             
    </div>  
  </body>

  <script type="text/javascript">
    var app = angular.module('myApp', ['ui.router']);   
    app.config(["$stateProvider",  function ($stateProvider) {      
        $stateProvider     
        .state("index", {
            url: '/index',  
            views:{
                'index':{template:"<div><div ui-view='header'></div><div ui-view='nav'></div><div ui-view='body'></div></div>"},
                //这里必须要绝对定位
                'header@index':{template:"<div>头部内容header</div>"},
                'nav@index':{template:"<div>菜单内容nav</div>"},
                'body@index':{template:"<div>展示内容contents</div>"}
            }
        })    
        //绝对定位
        .state("index.content1", {
            url: '/content1',  
            views:{
                'body@index':{template:"<div>content11111111111111111</div>"}
                //'body@index'表示名为body的view使用index模板
            }
        })  
        //相对定位：该状态里的名为body的ui-view为相对路径下的（即没有说明具体是哪个模板下的）
        .state("index.content2", {
            url: '/content2',  
            views:{
                'body':{template:"<div>content2222222222222222222</div>"}//
            }
        })      
    }]);
  </script>
```

由上面代码可知，相对定位不能找到的ui-view需要用@来绝对定位。

### 6.URL路由传参（通过$stateParams服务获取参数）

有url: '/index/:id',和url: '/index/{id}',两种形式传参。

```JavaScript
  <body >    
    <div ng-app="myApp" >
        <a ui-sref="index({id:30})">show index</a>    
        <a ui-sref="test({username:'peter'})">show test</a>
        <div ui-view></div>
    </div>  
  </body>

  <script type="text/javascript">
    var app = angular.module('myApp', ['ui.router']);   
    app.config(["$stateProvider",  function ($stateProvider) {      
        $stateProvider     
        .state("home", {
            url: '/',  
            template:"<div>homePage</div>"

        })
        .state("index", {
            url: '/index/:id',  
            template:"<div>indexcontent</div>",
            controller:function($stateParams){
                alert($stateParams.id)
            }
        })  
        .state("test", {
            url: '/test/:username',  
            template:"<div>testContent</div>",
            controller:function($stateParams){
                alert($stateParams.username)
            }
        })
    }]);
  </script>
```

### 7.Resolve（预载入）

参考资料：

使用预载入功能，开发者可以预先载入一系列依赖或者数据，然后注入到控制器中。在ngRoute中resolve选项可以允许开发者在路由到达前载入数据保证（promises）。在使用这个选项时比使用angular-route有更大的自由度。

预载入选项需要一个对象，这个对象的key即要注入到控制器的依赖，这个对象的value为需要被载入的factory服务。

如果传入的是字符串，angular-route会试图匹配已经注册的服务。如果传入的是函数，该函数将会被注入，并且该函数返回的值便是控制器的依赖之一。如果该函数返回一个数据保证（promise），这个数据保证将在控制器被实例化前被预先载入并且数据会被注入到控制器中。

```JavaScript
  <body>    
    <div ng-app="myApp">
        <a ui-sref="index">show index</a>
        <div ui-view></div>
    </div>  
  </body>

  <script type="text/javascript">
    var app = angular.module('myApp', ['ui.router']);   
    app.config(["$stateProvider",  function ($stateProvider) {      
        $stateProvider     
        .state("home", {
            url: '/',  
            template:"<div>homePage</div>"
        })
        .state("index", {
            url: '/index/{id}',  
            template:"<div>indexcontent</div>",
            resolve: {
                //这个函数的值会被直接返回，因为它不是数据保证
                user: function() {
                  return {
                    name: "peter",
                    email: "audiogroup@qq.com"
                  }
                },
                //这个函数为数据保证, 因此它将在控制器被实例化之前载入。
                detail: function($http) {
                  return $http({
                    method: 'JSONP',
                    url: '/current_details'
                  });
                },
                //前一个数据保证也可作为依赖注入到其他数据保证中！（这个非常实用）
                myId: function($http, detail) {
                  $http({
                    method: 'GET',
                    url: 'http://facebook.com/api/current_user',
                    params: {
                      email: currentDetails.data.emails[0]
                    }
                  })
                }
            },
            controller:function(user,detail,myId,$scope){
                alert(user.name)
                alert(user.email)
                console.log(detail)
            }
        })
    }]);
  </script>
```