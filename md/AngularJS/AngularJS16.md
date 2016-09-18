# part 16 - ng-include Directive

## In this session we will learn

    ng-include directive in AngularJS

###### 1.ng-include directive is used to embed an HTML page into another HTML page.

###### 2.This technique is extremely useful when you want to reuse a specific view in multiple pages in your application.

###### 3.The value for ng-include directive : 
     (1)Can be the name of the HTML page that you want to reuse.
        <div ng-include="'EmployeeList.html'"></div>

     (2)Can be a property on the $scope object that points to the reusable HTML page.
        <div ng-include="employeeList"></div>

##### 写法一：

#####    Script.js
    /// <reference path = "angular.min.js"/>

    var myApp = angular
                    .module("myModule",[])
                    .controller("myController",function($scope){

                        var employees = [
                                { name : "Ben", gender : "Male", salary : 55000 },
                                { name : "Sara", gender : "Female", salary : 68000 },
                                { name : "Mark", gender : "Male", salary : 57000 },
                                { name : "Pam", gender : "Female", salary : 53000 },
                                { name : "Todd", gender : "Male", salary : 60000 }
                            ];
                        
                            $scope.employees = employees;
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
            <div ng-include="'EmployeeTable.html'"></div>
        </div>
    </body>
    </html>

#####    EmployeeTable.html
    <table>
        <thead>
            <tr>
                <th>Name</th>
                <th>Gender</th>
                <th>Salary</th>
            </tr>
        </thead>
        <tbody>
            <tr ng-repeat="employee in employees">
                <td>{{ employee.name }}</td>
                <td>{{ employee.gender }}</td>
                <td>{{ employee.salary }}</td>
            </tr>
        </tbody>
    </table>

##### 写法二：

#####    Script.js
    /// <reference path = "angular.min.js"/>

    var myApp = angular
                    .module("myModule",[])
                    .controller("myController",function($scope){

                        var employees = [
                                { name : "Ben", gender : "Male", salary : 55000 },
                                { name : "Sara", gender : "Female", salary : 68000 },
                                { name : "Mark", gender : "Male", salary : 57000 },
                                { name : "Pam", gender : "Female", salary : 53000 },
                                { name : "Todd", gender : "Male", salary : 60000 }
                            ];
                        
                            $scope.employees = employees;
                            $scope.employeeView = "EmployeeTable.html";
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
            <div ng-include="employeeView"></div>
        </div>
    </body>
    </html>

##### 扩展小例子：

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
            Select View : 
            <select ng-model="employeeView">
                <option value="EmployeeTable.html">Table</option>
                <option value="EmployeeList.html">List</option>
            </select>
            <br><br>
            <div ng-include="employeeView"></div>
        </div>
    </body>
    </html>

#####    EmployeeList.html
    <ul>
        <li ng-repeat="employee in employees">
            {{ employee.name }}
            <ul>
                <li>
                    {{ employee.gender }}
                </li>
                <li>
                    {{ employee.salary }}
                </li>
            </ul>
        </li>
    </ul>

#####   result: 
![](../img/ng-include.png)