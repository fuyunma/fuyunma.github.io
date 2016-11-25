# part 15 - AngularJS ng-init directive

## In this session we will learn

    ng-init directive

###### The ng-init directive allows you to evaluate an expression in the current scope.

#####    HtmlPage1.html
    <!DOCTYPE html>
    <html lang="en" ng-app = "myModule">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <link rel="stylesheet" href="../style/Styles.css">
        <script type="text/javascript" src="../script/angular.js"></script>
    </head>
    <body>
        <div ng-init="employees = [
                    { name : 'Ben', gender : 'Male', city : 'London' },
                    { name : 'Sara', gender : 'Female', city : 'Chennai' },
                    { name : 'Mark', gender : 'Male', city : 'Chicago' },
                    { name : 'Pam', gender : 'Female', city : 'London' },
                    { name : 'Todd', gender : 'Male', city : 'Chennai' }
                ]">
            <table>
                <thead>
                    <tr>
                        <th>Name</th>
                        <th>Gender</th>
                        <th>City</th>
                    </tr>
                </thead>
                <tbody>
                    <tr ng-repeat="employee in employees">
                        <td>{{ employee.name }}</td>
                        <td>{{ employee.gender }}</td>
                        <td>{{ employee.city }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </body>
    </html>

###### In a real world application you should use a controller instead of ng-init to initialize values on a scope.

#####    Script.js
    /// <reference path = "angular.min.js"/>

    var myApp = angular
                    .module("myModule",[])
                    .controller("myController",function($scope){
                        var employees = [
                            { name : 'Ben', gender : 'Male', city : 'London' },
                            { name : 'Sara', gender : 'Female', city : 'Chennai' },
                            { name : 'Mark', gender : 'Male', city : 'Chicago' },
                            { name : 'Pam', gender : 'Female', city : 'London' },
                            { name : 'Todd', gender : 'Male', city : 'Chennai' }
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
    <body>
        <div ng-controller="myController">
            <table>
                <thead>
                    <tr>
                        <th>Name</th>
                        <th>Gender</th>
                        <th>City</th>
                    </tr>
                </thead>
                <tbody>
                    <tr ng-repeat="employee in employees">
                        <td>{{ employee.name }}</td>
                        <td>{{ employee.gender }}</td>
                        <td>{{ employee.city }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </body>
    </html>

###### ng-init should only be used for aliasing special properties of ng-repeat directive.

#####    Script.js
    /// <reference path = "angular.min.js"/>

    var myApp = angular
                    .module("myModule",[])
                    .controller("myController",function($scope){
                        var countries = [
                            {
                                name:"India",
                                cities:[
                                    { name:"Hyderabad" },
                                    { name:"Chennai" }
                                ]
                            },
                            {
                                name:"USA",
                                cities:[
                                    { name:"Los Angeles" },
                                    { name:"Chicago" }
                                ]
                            }
                        ];
                    
                        $scope.countries = countries;
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
    <body>
        <div ng-controller="myController">
            <ul>
                <li ng-repeat="country in countries" ng-init="parentIndex = $index">
                    {{ country.name }} - Index = {{ parentIndex }}
                    <ul>
                        <li ng-repeat="city in country.cities">
                            {{ city.name }} - Parent Index = {{ parentIndex }}, Index = {{ $index }}
                                                                    |
                                                        也可以使用$parent.$index
                        </li>
                    </ul>
                </li>
            </ul>
        </div>
    </body>
    </html>

