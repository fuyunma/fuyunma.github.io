# part 20 - Creating Custom Service

## In this session we will learn

    Creating and using a custom service in AngularJS.

#####    Script.js
    /// <reference path = "angular.min.js"/>

    var myApp = angular
                    .module("myModule",[])
                    .controller("myController",function($scope){
                        $scope.transformString = function(input){
                            var output = "";
                            if(!input){
                                return input;
                            }
                            for(var i = 0; i < input.length; i++){
                                if(i > 0 && input[i] == input[i].toUpperCase()){
                                    output = output + " ";
                                }
                                output += input[i];
                            }
                            $scope.output = output;
                        }
                    });

#####    HtmlPage1.html
    <!DOCTYPE html>
    <html lang="en" ng-app = "myModule">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <link rel="stylesheet" href="../style/Styles.css">
        <script type="text/javascript" src="../script/angular.min.js"></script>
        <script type="text/javascript" src="../script/Script.js"></script>
    </head>
    <body>
        <div ng-controller="myController">
            <table>
                <tr>
                    <td>Your String</td>
                    <td><input type="text" ng-model="input"></td>
                </tr>
                <tr>
                    <td>Result</td>
                    <td><input type="text" ng-model="output"></td>
                </tr>
                <tr>
                    <td></td>
                    <td><input type="button" ng-click="transformString(input)" value="Process String"></td>
                </tr>
            </table>
        </div>
    </body>
    </html>

##### There are two problems : 
###### first, the controller code has become a bit complex and it has become a bit large;
###### second, if we want to reuse this logic within any other controller then we will have to duplicate this code within that controller, the moment we start duplicating code, the maintainability of the application has gone for a toss.

    We want to encapsulate all this logic and its own service and inject that service into any controller where you need that,the first thing to do here is adding another javascript file to a project.This is the javascript file which is going to contain our custome service.We have the model and on that we have the factory method which we use to create a custom service and register that with angular.Usually the service is an angular of state less.The last thing that is reference that strength serviced or js file on our HTML page.

#####    Script.js(此时controller中的代码变得很简洁)
    /// <reference path = "angular.min.js"/>

    var myApp = angular
                    .module("myModule",[])
                    .controller("myController",function($scope, stringService){
                        $scope.transformString = function(input){
                            
                            $scope.output = stringService.processString(input);
                        }
                    });

#####    stringService.js(此时logic的复用性变得更好)
    /// <reference path = "Script.js"/>

    app.factory('stringService',function(){
            //      |                  |
            //name of the service   this anonymous function is actually going to return a JavaScript object.
        return{
            processString: function(input){
                var output = "";
                if(!input){
                    return input;
                }
                for(var i = 0; i < input.length; i++){
                    if(i > 0 && input[i] == input[i].toUpperCase()){
                        output = output + " ";
                    }
                    output += input[i];
                }
                return output;
            }
        };
    });

#####    HtmlPage1.html
    <!DOCTYPE html>
    <html lang="en" ng-app = "myModule">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <link rel="stylesheet" href="../style/Styles.css">
        <script type="text/javascript" src="../script/angular.min.js"></script>
        <script type="text/javascript" src="../script/Script.js"></script>
        <script type="text/javascript" src="../script/stringService.js"></script>
    </head>
    <body>
        <div ng-controller="myController">
            <table>
                <tr>
                    <td>Your String</td>
                    <td><input type="text" ng-model="input"></td>
                </tr>
                <tr>
                    <td>Result</td>
                    <td><input type="text" ng-model="output"></td>
                </tr>
                <tr>
                    <td></td>
                    <td><input type="button" ng-click="transformString(input)" value="Process String"></td>
                </tr>
            </table>
        </div>
    </body>
    </html>