##全局变量设置之value vs constant vs rootscope vs 服务

    AngualrJS中设置全局变量，即每个Controller中都可以访问的变量，主要有以下几种方法：
    1、通过var 直接定义global variable，相当于直接用js
    2.、用angularjs rootscope来设置全局变量 。
    3、用angularjs value来设置全局变量 。
    4、用angularjs constant来设置全局变量 。
    5、定义服务传值

    方法2-5如下：

###一、angularjs rootscope来设置全局变量

    像使用rootscope，笔者的建议是放在run中，这里其这controller中都不用引入rootscope，直接使用需要的全局变量就可以了。

    appCommon.run(function($rootScope) {  
        $rootScope.paginationConf = {  
            currentPage : 1, // 分页开始  
            itemsPerPage : 15, // 分页每页显示条数   
        };  
    })

    然后，其它Controller要用，直接

    app.controller('merchantController', function($scope) {  
        var   limit = $scope.paginationConf.itemsPerPage;  
        var   pageIndex  = $scope.paginationConf.currentPage; 
        .......................................  
    }）

    这里需要注意的是，每个Controller层都会先在当前的scope找需要的变量，找不到，再到rootscope上去寻找。如果还是找不到，就会报错。

###二、用angularjs value来设置全局变量

    使用实例如下：

    <!DOCTYPE html>  
    <html lang="zh" ng-app="myApp">  
      
    <head>  
        <meta charset="UTF-8">  
        <title>AngularJS学习</title>  
        <script type="text/javascript" src="./1.5.3/angular.min.js"></script>  
    </head>  
      
    <body>  
        <div ng-controller="myCtrl1">  
            <button ng-click="onclick1()">请点击我1</button>  
            {{value1}}  
        </div>  
        <div ng-controller="myCtrl2">  
            <button ng-click="onclick2()">请点击我2</button>  
              {{value2}}  
        </div>  
    </body>  
    <script type="text/javascript">  
    var app = angular.module('myApp', []);  
    app.value('myValue',{"value1":"林炳文","value2":"hello world",value3:1});    
    app.controller('myCtrl1', function($scope,myValue) {  
        $scope.onclick1 = function() {  
           $scope.value1 = myValue.value1 + (++myValue.value3);  
       };  
    });  
    app.controller('myCtrl2', function($scope,myValue) {  
        $scope.onclick2 = function() {  
           $scope.value2 = myValue.value2 +  (++myValue.value3);  
       };  
    });  
    </script>  
    </html>

###三、用angularjs constant来设置全局变量

    使用实例

    <!DOCTYPE html>  
    <html lang="zh" ng-app="myApp">  
      
    <head>  
        <meta charset="UTF-8">  
        <title>AngularJS学习</title>  
        <script type="text/javascript" src="./1.5.3/angular.min.js"></script>  
    </head>  
      
    <body>  
        <div ng-controller="myCtrl1">  
            <button ng-click="onclick1()">请点击我1</button>  
            {{value1}}  
        </div>  
        <div ng-controller="myCtrl2">  
            <button ng-click="onclick2()">请点击我2</button>  
              {{value2}}  
        </div>  
    </body>  
    <script type="text/javascript">  
    var app = angular.module('myApp', []);  
    app.constant('myConstant',{"value1":"林炳文","value2":"hello world",value3:1});    
    app.controller('myCtrl1', function($scope,myConstant) {  
        $scope.onclick1 = function() {  
           $scope.value1 = myConstant.value1 + (++myConstant.value3);  
           myConstant.value1 = $scope.value1;  
           myConstant.value2 = $scope.value1;  
       };  
    });  
    app.controller('myCtrl2', function($scope,myConstant) {  
        $scope.onclick2 = function() {  
           $scope.value2 = myConstant.value2 +  (++myConstant.value3);  
            myConstant.value1 = $scope.value2;  
            myConstant.value2 = $scope.value2;  
       };  
    });  
    </script>  
    </html>

####value与constant区别

    value不可在config里注入，constant可以。下面是笔者做的一个测试：

    app.constant('myConstant',{"value1":"林炳文","value2":"hello world",value3:1});    
    app.value('myValue',{"value1":"林炳文","value2":"hello world",value3:1});

    然后在config来引入：

    app.config(function(myValue){  
    ..  
    });

    会报错

    如果使用

    app.config(function(myConstant){  
    //可以得到constant定义的'myConstant'  
    }); 

    一切正常

###四、定义服务传值

    这是java中最常用的方法了，其实就相当于定义一个对象的服务中，并设置get/set方法。通过这两个方法来实时更新与获取数据

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
      var name = '我是林炳文';  
      var service = {};  
      service.getName = function() {  
        return name;  
      };  
      service.setName = function(newName) {  
         name = newName;  
      };  
      return service;  
    });  
    app.controller('childCtrl1', function($scope,dataService) {  
        $scope.name = dataService.getName();  
        $scope.setName = function() {  
              dataService.setName( "set name to jack jack jack");  
               $scope.name = dataService.getName();  
        };  
    });  
    app.controller('childCtrl2', function($scope,dataService) {  
           $scope.name = dataService.getName();  
           $scope.setName = function() {  
            dataService.setName( "set name to tom tom tom");  
              $scope.name = dataService.getName();  
        };  
    });  
    </script>  
    </html>