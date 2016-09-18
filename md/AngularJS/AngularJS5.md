# part 5 - Two way DataBinding

## In this session we will learn

### Two way databinding in AngularJS
    
    The Two Way Data-Binding,keeps the model and the view in sync at all times,that is a change in the model updates the view and a change in the view updates the model.

######  1.Binding expression updates the view when the model changes 
    {{ message }}.

#####    Script.js
        /// <reference path = "angular.min.js"/>

        var myApp = angular
                        .module("myModule",[])
                        .controller("myController",function($scope){
                            $scope.message = "Hello Angular!"
                        });

#####   HtmlPage1.html
        <!DOCTYPE html>
        <html lang="en" ng-app = "myModule">
        <head>
            <meta charset="UTF-8">
            <title>Document</title>
            <script type="text/javascript" src="../script/angular.js"></script>
            <script type="text/javascript" src="../script/Script.js"></script>
        </head>
        <body ng-controller = "myController">
            {{ message }}
        </body>
        </html>

######  2.ng-model directive updates the model when the view changes.
    <input type="text" ng-model="message"/>

#####   HtmlPage1.html(right)
        <!DOCTYPE html>
        <html lang="en" ng-app = "myModule">
        <head>
            <meta charset="UTF-8">
            <title>Document</title>
            <script type="text/javascript" src="../script/angular.js"></script>
            <script type="text/javascript" src="../script/Script.js"></script>
        </head>
        <body ng-controller = "myController">
            <input type="text" ng-model="message">
            <br><br>
            {{ message }}
        </body>
        </html>

#####   HtmlPage1.html(error)
        <!DOCTYPE html>
        <html lang="en" ng-app = "myModule">
        <head>
            <meta charset="UTF-8">
            <title>Document</title>
            <script type="text/javascript" src="../script/angular.js"></script>
            <script type="text/javascript" src="../script/Script.js"></script>
        </head>
        <body ng-controller = "myController">
            <input type="text" ng-model="greeting">
            <br><br>
            {{ message }}
        </body>
        </html>
### ng-model directive

#####   HtmlPage1.html
    <!DOCTYPE html>
    <html lang="en" ng-app = "myModule">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <script type="text/javascript" src="../script/angular.js"></script>
        <script type="text/javascript" src="../script/Script.js"></script>
    </head>
    <body ng-controller = "myController">
        <input type="text" ng-model="greeting">
        <br><br>
        {{ message }}
        <br><br>
        {{ greeting }}
    </body>
    </html>

##### ng-model directive can be used with : input、select、textarea.

#####   HtmlPage1.html
    <!DOCTYPE html>
    <html lang="en" ng-app = "myModule">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <script type="text/javascript" src="../script/angular.js"></script>
        <script type="text/javascript" src="../script/Script.js"></script>
    </head>
    <body ng-controller = "myController">
        <table>
            <tr>
                <td>First Name:</td>
                <td>
                    <input type="text" ng-model="employee.firstName">
                </td>
            </tr>
            <tr>
                <td>Last Name:</td>
                <td>
                    <input type="text" ng-model="employee.lastName">
                </td>
            </tr>
            <tr>
                <td>Gender:</td>
                <td>
                    <input type="text" ng-model="employee.gender">
                </td>
            </tr>
        </table>
        <br>
        <table>
            <tr>
                <td>First Name:</td>
                <td>
                    {{ employee.firstName }}
                </td>
            </tr>
            <tr>
                <td>Last Name:</td>
                <td>
                    {{ employee.lastName }}
                </td>
            </tr>
            <tr>
                <td>Gender:</td>
                <td>
                    {{ employee.gender }}
                </td>
            </tr>
        </table>
    </body>
    </html>
