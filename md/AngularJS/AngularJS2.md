# part 2 - Modules and Controllers

## In this session we will learn

    1.What is a module and how to create a module
    2.What is a controller and how to create a controller
    3.How to register a controller with the module
    4.How to use the module that we create to bootstrap the angular application

### What is a module in AngularJS

    A module is a container for different parts of your application i.e controllers,services,directives,filters,etc.

    You can think of a module as a Main() method in other types of applications.

### How to create a module
    
    Use the angular object's module() method to create a module.
#####   var myApp = angular.module("myModule",[]);
                                    |         |
                  所创建的module的名称     module的依赖关系(一个module可以依赖于其他的modules)

### What is a controller in angular

    In angular a controller is a JavaScript function.The job of the controller is to build a model for the view to display.

### How to create a controller in angular

#####     var myController = function($scope){
            $scope.message = "AngularJS Tutorial";
#####    }

    $scope is an angular object that is passed to this controller function by the angular framework automatically.The $scope object is provided by the framework within the view.

#####    Script.js
        /// <reference path = "angular.min.js"/>

        var myApp = angular.module("myModule",[]);//the first step => create a module

        var myController = function($scope){//the second step => create a controller
            $scope.message = "AngularJS Tutorial";
        };

        myApp.controller("myController",myController);//the next step is to register this controller with other module
            //name for the controller   this controller function itself

#####    另一种写法：

        /// <reference path = "angular.min.js"/>

        var myApp = angular.module("myModule",[]);

        myApp.controller("myController",function($scope){controller
            $scope.message = "AngularJS Tutorial";
        });

#####   HtmlPage1.html
        <!DOCTYPE html>
        <html lang="en" ng-app = "myModule">
        <head>
            <meta charset="UTF-8">
            <title>Document</title>
            <script type="text/javascript" src="../script/angular.min.js"></script>
            <script type="text/javascript" src="../script/Script.js"></script>
        </head>
        <body>
            <div ng-controller = "myController">
                {{ message }}
            </div>
            <div>
                {{ message }}
            </div>
        </body>
        </html>

#####   result: 
######        AngularJS Tutorial

        <!DOCTYPE html>
        <html lang="en" ng-app = "myModule">
        <head>
            <meta charset="UTF-8">
            <title>Document</title>
            <script type="text/javascript" src="../script/angular.min.js"></script>
            <script type="text/javascript" src="../script/Script.js"></script>
        </head>
        <body ng-controller = "myController">
            <div>
                {{ message }}
            </div>
            <div>
                {{ message }}
            </div>
        </body>
        </html>

#####   result: 
######        AngularJS Tutorial
######        AngularJS Tutorial

![](../img/Module_Controller.png)