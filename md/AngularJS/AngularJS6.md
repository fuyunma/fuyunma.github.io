# part 6 - AngularJS ng-repeat directive

## In this session we will learn

    1.ng-repeat directive in Angular
    2.Nesting ng-repeat with an example

    ng-repeat is similar to foreach loop in C#

#####    Script.js
    /// <reference path = "angular.min.js"/>

    var myApp = angular
                    .module("myModule",[])
                    .controller("myController",function($scope){
                        var employees = [
                            {firstName : "Ben" , lastName : "Hastings" , gender : "Male" , salary : 55000},
                            {firstName : "Sara" , lastName : "Paul" , gender : "Female" , salary : 68000},
                            {firstName : "Mark" , lastName : "Holland" , gender : "Male" , salary : 57000},
                            {firstName : "Pam" , lastName : "Macintosh" , gender : "Female" , salary : 53000},
                            {firstName : "Todd" , lastName : "Barber" , gender : "Male" , salary : 60000}
                        ];
                    
                        $scope.employees = employees;
                    });

#####    HtmlPage1.html
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
            <thead>
                <tr>
                    <th>Firstname</th>
                    <th>Lastname</th>
                    <th>Gender</th>
                    <th>Salary</th>
                </tr>
            </thead>
            <tbody>
                <tr ng-repeat="employee in employees">
                    <td>{{ employee.firstName }}</td>
                    <td>{{ employee.lastName }}</td>
                    <td>{{ employee.gender }}</td>
                    <td>{{ employee.salary }}</td>
                </tr>
            </tbody>
        </table>
    </body>
    </html>

#####   result: 
    Firstname   Lastname    Gender  Salary
    Ben Hastings    Male    55000
    Sara    Paul    Female  68000
    Mark    Holland Male    57000
    Pam Macintosh   Female  53000
    Todd    Barber  Male    60000

#####    Script.js
    /// <reference path = "angular.min.js"/>

    var myApp = angular
                    .module("myModule",[])
                    .controller("myController",function($scope){
                        var countries = [
                            {
                                name:"UK",
                                cities:[
                                    { name:"London" },
                                    { name:"Manchester" },
                                    { name:"Birmingham" }
                                ]
                            },
                            {
                                name:"USA",
                                cities:[
                                    { name:"Los Angeles" },
                                    { name:"Chicago" },
                                    { name:"Houston" }
                                ]
                            },
                            {
                                name:"India",
                                cities:[
                                    { name:"Hyderabad" },
                                    { name:"Chennai" },
                                    { name:"Mumbai" }
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
        <script type="text/javascript" src="../script/angular.js"></script>
        <script type="text/javascript" src="../script/Script.js"></script>
    </head>
    <body ng-controller = "myController">
        <ul>
            <li ng-repeat="country in countries">
                {{ country.name }}
                <ul>
                    <li ng-repeat="city in country.cities">
                        {{ city.name }}
                    </li>
                </ul>
            </li>
        </ul>
    </body>
    </html>

#####   result: 
![](../img/ng-repeat.png)

### Finding the index of an item in the collection:

    1.To find the index of an item in the collection use $index property
    2.To get the index of the parent element
        (1)Use $parent.$index
        (2)Use ng-init="parentIndex=$index"

#####To get the index of the parent element(two methods):

###### result:
![](../img/parentIndex.png)

#####the first method:

#####    HtmlPage1.html
    <!DOCTYPE html>
    <html lang="en" ng-app = "myModule">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <script type="text/javascript" src="../script/angular.js"></script>
        <script type="text/javascript" src="../script/Script.js"></script>
    </head>
    <body ng-controller = "myController">
        <ul>
            <li ng-repeat="country in countries">
                {{ country.name }} - Index = {{ $index }}
                <ul>
                    <li ng-repeat="city in country.cities">
                        {{ city.name }} - Parent Index = {{ $parent.$index }}, Index = {{ $index }}
                    </li>
                </ul>
            </li>
        </ul>
    </body>
    </html>

#####the second method:

#####    HtmlPage1.html

    <!DOCTYPE html>
    <html lang="en" ng-app = "myModule">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <script type="text/javascript" src="../script/angular.js"></script>
        <script type="text/javascript" src="../script/Script.js"></script>
    </head>
    <body ng-controller = "myController">
        <ul>
            <li ng-repeat="country in countries" ng-init="parentIndex = $index">
                {{ country.name }} - Index = {{ $index }}
                <ul>
                    <li ng-repeat="city in country.cities">
                        {{ city.name }} - Parent Index = {{ parentIndex }}, Index = {{ $index }}
                    </li>
                </ul>
            </li>
        </ul>
    </body>
    </html>