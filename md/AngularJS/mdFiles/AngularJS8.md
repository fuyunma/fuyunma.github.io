# part 8 - AngularJS filters

## In this session we will learn

    Filters in AngularJS

##### Filters can do 3 different things
    Format,Sort and Filter data

##### Filters can be used with a binding expression or a directive
    
##### To apply a filter use pipe(|) character
    {{ expression | filterName:parameter }}

##### Filters for formatting data
![](../img/filters.png)

##### AngularJS Filters

######    1.Angular Date formats
![](../img/AngularDateFormats.png)

######    2.Angular date format documentation
    https://docs.angularjs.org/api/ng/filter/date

######    3.limitTo filter : Can be used to limit the number of rows or characters in a string
    {{ expression | limitTo : limit : begin }}

##### no use limitTo filter:
![](../img/no_limitToFilter.png)

#####    Script.js
    /// <reference path = "angular.min.js"/>

    var myApp = angular
                    .module("myModule",[])
                    .controller("myController",function($scope){
                        var employees = [
                            { name : "Ben" , dateOfBirth : new Date("November 23, 1980") , gender : "Male" , salary : 55000.788 },
                            { name : "Sara" , dateOfBirth : new Date("May 05, 1970") , gender : "Female" , salary : 68000 },
                            { name : "Mark" , dateOfBirth : new Date("August 15, 1974") , gender : "Male" , salary : 57000 },
                            { name : "Pam" , dateOfBirth : new Date("October 27, 1979") , gender : "Female" , salary : 53000 },
                            { name : "Todd" , dateOfBirth : new Date("December 30, 1983") , gender : "Male" , salary : 60000 }
                        ];
                    
                        $scope.employees = employees;
                        $scope.rowLimit = 3;
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
        Rows to display : <input type="number" step="1" min="0" max="5" ng-model="rowLimit">
        <br><br>
        <table>
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Date of Birth</th>
                    <th>Gender</th>
                    <th>Salary (number)</th>
                    <th>Salary (currency)</th>
                </tr>
            </thead>
            <tbody>
                <tr ng-repeat="employee in employees | limitTo : 2 : 1" >
                                                       <!-- rowsNum index -->
                                                       <!-- 行数    从下标(最小为0)为几的行开始显示 -->
                    <td>{{ employee.name | uppercase }}</td>
                    <td>{{ employee.dateOfBirth | date : "dd/MM/yyyy" }}</td>
                    <td>{{ employee.gender | lowercase }}</td>
                    <td>{{ employee.salary | number : 2 }}</td>
                    <td>{{ employee.salary | currency : "￡" : 1 }}</td>
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

#####   result: 
![](../img/limitToFilter.png)

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
        Rows to display : <input type="number" step="1" min="0" max="5" ng-model="rowLimit">
        <br><br>
        <table>
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Date of Birth</th>
                    <th>Gender</th>
                    <th>Salary (number)</th>
                    <th>Salary (currency)</th>
                </tr>
            </thead>
            <tbody>
                <tr ng-repeat="employee in employees | limitTo : rowLimit">
                    <td>{{ employee.name | uppercase }}</td>
                    <td>{{ employee.dateOfBirth | date : "dd/MM/yyyy" }}</td>
                    <td>{{ employee.gender | lowercase }}</td>
                    <td>{{ employee.salary | number : 2 }}</td>
                    <td>{{ employee.salary | currency : "￡" : 1 }}</td>
                </tr>
            </tbody>
        </table>
    </body>
    </html>

#####   result: 
![](../img/limitToFilter2.png)