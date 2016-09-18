# part 11 - Search filter in AngularJS

## In this session we will learn

    How to implement search in Angular using search filter

    As we type in the search textbox,all the columns in the table must be searched and only the matching rows should be displayed.

##### 搜索所有column中包含搜索框中指定字符的rows

#####    Script.js
    /// <reference path = "angular.min.js"/>

    var myApp = angular
                    .module("myModule",[])
                    .controller("myController",function($scope){
                        var employees = [
                            { name : "Ben", gender : "Male", salary : 55000, city:"London" },
                            { name : "Sara", gender : "Female", salary : 68000, city:"Chennai" },
                            { name : "Mark", gender : "Male", salary : 57000, city:"London" },
                            { name : "Pam", gender : "Female", salary : 53000, city:"Chennai" },
                            { name : "Todd", gender : "Male", salary : 60000, city:"London" }
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
        Search : <input type="text" placeholder="Search employees" ng-model="searchText">
        <br><br>
        <table>
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Gender</th>
                    <th>Salary</th>
                    <th>City</th>
                </tr>
            </thead>
            <tbody>
                <tr ng-repeat="employee in employees | filter : searchText">
                    <td>{{ employee.name }}</td>
                    <td>{{ employee.gender }}</td>
                    <td>{{ employee.salary }}</td>
                    <td>{{ employee.city }}</td>
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

##### 搜索指定column中包含搜索框中指定字符的rows

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
        Search : <input type="text" placeholder="Search employees" ng-model="searchText.city">
        <br><br>
        <table>
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Gender</th>
                    <th>Salary</th>
                    <th>City</th>
                </tr>
            </thead>
            <tbody>
                <tr ng-repeat="employee in employees | filter : searchText">
                    <td>{{ employee.name }}</td>
                    <td>{{ employee.gender }}</td>
                    <td>{{ employee.salary }}</td>
                    <td>{{ employee.city }}</td>
                </tr>
            </tbody>
        </table>
    </body>
    </html>