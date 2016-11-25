# part 37 - Angular scope vs rootScope

## In this session we will learn

    Difference between $scope and $rootScope.

##### $rootScope is available globally(for all controllers),whereas $scope is only available to the controller that has created it and it's children.

##### 案例一：

##### Script.js
    /// <reference path = "angular.min.js"/>

    var myApp = angular
                    .module("Demo",[])
                    .controller("redColorController",function($scope,$rootScope){
                        $scope.redColor = "I am Red Color";
                        $rootScope.rootScopeColor = "I am Root Scope Color";
                    })
                    .controller("greenColorController",function($scope){
                        $scope.greenColor = "I am Green Color";
                    })

##### HtmlPage1.html
    <!DOCTYPE html>
    <html lang="en" ng-app = "Demo">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <script type="text/javascript" src="../script/angular.min.js"></script>
        <script type="text/javascript" src="../script/Script.js"></script>
    </head>
    <body>
        <div ng-controller="redColorController">
            Root Scope Color : {{ rootScopeColor }} <br>
            Red Color Controller : {{ redColor }} <br>
            Green Color Controller : {{ greenColor }}
        </div>
        <div ng-controller="greenColorController">
            Root Scope Color : {{ rootScopeColor }} <br>
            Green Color Controller : {{ greenColor }} <br>
            Red Color Controller : {{ redColor }}
        </div>  
    </body>
    </html>

##### result:
    Root Scope Color : I am Root Scope Color 
    Red Color Controller : I am Red Color 
    Green Color Controller :
    Root Scope Color : I am Root Scope Color 
    Green Color Controller : I am Green Color 
    Red Color Controller :

##### 案例二：

##### HtmlPage1.html
    <!DOCTYPE html>
    <html lang="en" ng-app = "Demo">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <script type="text/javascript" src="../script/angular.min.js"></script>
        <script type="text/javascript" src="../script/Script.js"></script>
    </head>
    <body>
        <div ng-controller="redColorController">
            Root Scope Color : {{ rootScopeColor }} <br>
            Red Color Controller : {{ redColor }} <br>
            Green Color Controller : 
            <span style="color:red;" ng-show="greenColor == undefined">
                greenColor is undefined
            </span>
        </div>
        <div ng-controller="greenColorController">
            Root Scope Color : {{ rootScopeColor }} <br>
            Green Color Controller : {{ greenColor }} <br>
            Red Color Controller : 
            <span style="color:red;" ng-show="redColor == undefined">
                redColor is undefined
            </span>
        </div>  
    </body>
    </html>

##### result:
<img src="../img/rootScopeVSscope.png" alt="">