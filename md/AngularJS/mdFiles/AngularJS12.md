# part 12 - Filter by muliple properties

## In this session we will learn

#### How to filter by multiple properties?

#####    Script.js
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
        <input type="text" placeholder="Search name" ng-model="searchText.name">
        <input type="text" placeholder="Search city" ng-model="searchText.city">
        <input type="checkbox" ng-model="exactMatch">Exact Match
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
                <tr ng-repeat="employee in employees | filter : searchText : exactMatch">
                    <td>{{ employee.name }}</td>
                    <td>{{ employee.gender }}</td>
                    <td>{{ employee.salary }}</td>
                    <td>{{ employee.city }}</td>
                </tr>
            </tbody>
        </table>
    </body>
    </html>

#### Single search textbox searching multiple properties

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

                        //该函数的作用是：1.判断输入框中是否输入了内容，如果没有则显示全部数据；
                        //2.如果有内容，则将其与对应的每一项数据中的name或city进行比较,如果该数据被包含在name或city中，则显示对应的数据；
                        //3.如果不满足上述条件则不显示任何数据。
                        $scope.search = function(item){
                            if($scope.searchText == undefined){
                                return true;
                            }
                            else{
                                if(item.name.toLowerCase().indexOf($scope.searchText.toLowerCase()) != -1 || 
                                    item.city.toLowerCase().indexOf($scope.searchText.toLowerCase()) != -1){
                                    return true;
                                }
                            }
                            return false;
                        }
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
        <input type="text" placeholder="Search city &amp; name" ng-model="searchText">
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
                <tr ng-repeat="employee in employees | filter : search">
                    <td>{{ employee.name }}</td>
                    <td>{{ employee.gender }}</td>
                    <td>{{ employee.salary }}</td>
                    <td>{{ employee.city }}</td>
                </tr>
            </tbody>
        </table>
    </body>
    </html>