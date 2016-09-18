# part 14 - ng-hide & ng-show

## In this session we will learn
    
    ng-hide and ng-show in AngularJS

### ng-hide and ng-show directives are used to control the visibility of the HTML elements.

##### 使用ng-hide实现显示隐藏salary column

#####    Script.js
    /// <reference path = "angular.min.js"/>

    var myApp = angular
                    .module("myModule",[])
                    .controller("myController",function($scope){
                        var employees = [
                            { name : "Ben", gender : 1, city : "London", salary : 55000 },
                            { name : "Sara", gender : 2, city : "Chennai", salary : 68000 },
                            { name : "Mark", gender : 1, city : "Chicago", salary : 57000 },
                            { name : "Pam", gender : 2, city : "London", salary : 53000 },
                            { name : "Todd", gender : 3, city : "Chennai", salary : 60000 }
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
        <script type="text/javascript" src="../script/angular.js"></script>
        <script type="text/javascript" src="../script/Script.js"></script>
    </head>
    <body ng-controller = "myController">
        <input type="checkbox" ng-model="hideSalary">Hide Salary
        <br><br>
        <table>
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Gender</th>
                    <th>City</th>
                    <th ng-hide="hideSalary">Salary</th>
                </tr>
            </thead>
            <tbody>
                <tr ng-repeat="employee in employees">
                    <td>{{ employee.name }}</td>
                    <td>{{ employee.gender }}</td>
                    <td>{{ employee.city }}</td>
                    <td ng-hide="hideSalary">{{ employee.salary }}</td>
                </tr>
            </tbody>
        </table>
    </body>
    </html>

#####    Styles.css
    body{
        font-family: Arial;
    }

    table{
        border-collapse: collapse;
    }

    td{
        border:1px solid black;
        padding:5px;
    }

    th{
        border:1px solid black;
        padding:5px;
        text-align:left;
    }

##### 使用ng-show实现显示隐藏salary column

#####    HtmlPage1.html
    <!DOCTYPE html>
    <html lang="en" ng-app = "myModule">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <link rel="stylesheet" href="../style/Styles.css">
        <script type="text/javascript" src="../script/angular.js"></script>
        <script type="text/javascript" src="../script/Script.js"></script>
    </head>
    <body ng-controller = "myController">
        <input type="checkbox" ng-model="hideSalary">Hide Salary
        <br><br>
        <table>
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Gender</th>
                    <th>City</th>
                    <th ng-show="!hideSalary">Salary</th>
                </tr>
            </thead>
            <tbody>
                <tr ng-repeat="employee in employees">
                    <td>{{ employee.name }}</td>
                    <td>{{ employee.gender }}</td>
                    <td>{{ employee.city }}</td>
                    <td ng-show="!hideSalary">{{ employee.salary }}</td>
                </tr>
            </tbody>
        </table>
    </body>
    </html>

### Mask and unmask Salary column values.

#####    HtmlPage1.html
    <!DOCTYPE html>
    <html lang="en" ng-app = "myModule">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <link rel="stylesheet" href="../style/Styles.css">
        <script type="text/javascript" src="../script/angular.js"></script>
        <script type="text/javascript" src="../script/Script.js"></script>
        <script type="text/javascript" src="../script/Filters.js"></script>
    </head>
    <body ng-controller = "myController">
        <input type="checkbox" ng-model="hideSalary">Hide Salary
        <br><br>
        <table>
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Gender</th>
                    <th>City</th>
                    <th ng-hide="hideSalary">Salary</th>
                    <th ng-show="hideSalary">Salary</th>
                </tr>
            </thead>
            <tbody>
                <tr ng-repeat="employee in employees">
                    <td>{{ employee.name }}</td>
                    <td>{{ employee.gender }}</td>
                    <td>{{ employee.city }}</td>
                    <td ng-hide="hideSalary">{{ employee.salary }}</td>
                    <td ng-show="hideSalary">####</td>
                </tr>
            </tbody>
        </table>
    </body>
    </html>