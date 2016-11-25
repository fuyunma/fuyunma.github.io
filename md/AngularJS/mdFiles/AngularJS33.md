# part 33 - Angular nested scopes and CONTROLLER AS syntax

## In this session we will learn

How the CONTROLLER AS syntax can make our code more readable when working with nested scopes?

##### 方法一：使用 $scope object(如果有多级嵌套的controllers，写起来容易乱)

##### Script.js

    /// <reference path = "angular.min.js"/>

    var myApp = angular
                    .module("Demo",[])
                    .controller("countryController",function($scope){
                        $scope.name = "India";
                    })
                    .controller("stateController",function($scope){
                        $scope.name = "Maharashtra";
                    })
                    .controller("cityController",function($scope){
                        $scope.name = "Mumbai";
                    })

##### HtmlPage1.html

    <!DOCTYPE html>
    <html lang="en" ng-app="Demo">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <script type="text/javascript" src="script/angular.min.js"></script>
        <script type="text/javascript" src="script/Script.js"></script>
    </head>
    <body>
        <div ng-controller="countryController">
            {{name}}
            <div ng-controller="stateController">
                {{$parent.name}} - {{name}}
                <div ng-controller="cityController">
                    {{$parent.$parent.name}} - {{$parent.name}} - {{name}}
                </div>
            </div>
        </div>
    </body>
    </html>

##### result: 

    India
    India - Maharashtra
    India - Maharashtra - Mumbai

##### 方法二：使用CONTROLLER  AS syntax(如果有多级嵌套的controllers，写起来层次清晰,可读性更好)

##### Script.js

    /// <reference path = "angular.min.js"/>

    var myApp = angular
                    .module("Demo",[])
                    .controller("countryController",function(){
                        this.name = "India";
                    })
                    .controller("stateController",function(){
                        this.name = "Maharashtra";
                    })
                    .controller("cityController",function(){
                        this.name = "Mumbai";
                    })

##### HtmlPage1.html
    
    <!DOCTYPE html>
    <html lang="en" ng-app="Demo">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <script type="text/javascript" src="script/angular.min.js"></script>
        <script type="text/javascript" src="script/Script.js"></script>
    </head>
    <body>
        <div ng-controller="countryController as countryCtrl">
            {{countryCtrl.name}}
            <div ng-controller="stateController as stateCtrl">
                {{countryCtrl.name}} - {{stateCtrl.name}}
                <div ng-controller="cityController as cityCtrl">
                    {{countryCtrl.name}} - {{stateCtrl.name}} - {{cityCtrl.name}}
                </div>
            </div>
        </div>
    </body>
    </html>

##### result: 

    India
    India - Maharashtra
    India - Maharashtra - Mumbai