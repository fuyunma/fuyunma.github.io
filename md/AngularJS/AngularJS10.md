# part 10 - AngularJS Sort Rows by Table Header

## In this session we will learn

    How to implement bidirectional sort in AngularJS

#####    Script.js
    /// <reference path = "angular.min.js"/>

    var myApp = angular
                    .module("myModule",[])
                    .controller("myController",function($scope){
                        var employees = [
                            { name : "Ben" , dateOfBirth : new Date("November 23, 1980") , gender : "Male" , salary : 55000 },
                            { name : "Sara" , dateOfBirth : new Date("May 05, 1970") , gender : "Female" , salary : 68000 },
                            { name : "Mark" , dateOfBirth : new Date("August 15, 1974") , gender : "Male" , salary : 57000 },
                            { name : "Pam" , dateOfBirth : new Date("October 27, 1979") , gender : "Female" , salary : 53000 },
                            { name : "Todd" , dateOfBirth : new Date("December 30, 1983") , gender : "Male" , salary : 60000 }
                        ];
                    
                        $scope.employees = employees;
                        $scope.sortColumn = "name";
                        $scope.reverseSort = false;

                        $scope.sortData = function(column){
                            $scope.reverseSort = ($scope.sortColumn == column) ? !$scope.reverseSort : false;
                            $scope.sortColumn = column;
                        }

                        $scope.getSortClass = function(column){
                            if($scope.sortColumn == column){
                                return $scope.reverseSort ? "arrow-down" : "arrow-up";
                            }

                            return '';
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
        <table>
            <thead>
                <tr>
                    <th ng-click="sortData('name')">
                        Name
                        <div ng-class="getSortClass('name')"></div>
                    </th>
                    <th ng-click="sortData('dateOfBirth')">
                        Date of Birth
                        <div ng-class="getSortClass('dateOfBirth')"></div>
                    </th>
                    <th ng-click="sortData('gender')">
                        Gender
                        <div ng-class="getSortClass('gender')"></div>
                    </th>
                    <th ng-click="sortData('salary')">
                        Salary
                        <div ng-class="getSortClass('salary')"></div>
                    </th>
                </tr>
            </thead>
            <tbody>
                <tr ng-repeat="employee in employees | orderBy : sortColumn : reverseSort">
                    <td>{{ employee.name }}</td>
                    <td>{{ employee.dateOfBirth | date : "dd/MM/yyyy" }}</td>
                    <td>{{ employee.gender }}</td>
                    <td>{{ employee.salary }}</td>
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

    .arrow-up{
        width:0px;
        height:0px;
        border-left:5px solid transparent;
        border-right:5px solid transparent;
        border-bottom:10px solid black;
        display:inline-block;
    }

    .arrow-down{
        width:0px;
        height:0px;
        border-left:5px solid transparent;
        border-right:5px solid transparent;
        border-top:10px solid black;
        display:inline-block;
    }

#####   result: 
![](../img/thead_click_orderBy.png)