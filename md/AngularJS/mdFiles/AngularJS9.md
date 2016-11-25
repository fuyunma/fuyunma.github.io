# part 9 - Sorting data in AngularJS

## In this session we will learn

    Sorting data in AngularJS

##### To sort the data in Angular

######    Use orderBy filter
######    {{ orderBy_expression | orderBy : expression : reverse }}

     Example : ng-repeat="employee in employees | orderBy : 'salary' : false"
    
#####    To sort in ascending order,set reverse to false(升序)
#####    To sort in descending order,set reverse to true(降序)
######   You can also use + and - to sort in ascending and descending order respectively
    ng-repeat="employee in employees | orderBy : '+salary'"

##### 写法一：

#####    Script.js(Asc)
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
                    <th>Name</th>
                    <th>Date of Birth</th>
                    <th>Gender</th>
                    <th>Salary</th>
                </tr>
            </thead>
            <tbody>
                <tr ng-repeat="employee in employees | orderBy : 'name' : false"><!-- 去掉false后默认也为升序排序，等价于<tr ng-repeat="employee in employees | orderBy : 'name'"> -->
                    <td>{{ employee.name }}</td>
                    <td>{{ employee.dateOfBirth | date : "dd/MM/yyyy" }}</td>
                    <td>{{ employee.gender }}</td>
                    <td>{{ employee.salary }}</td>
                </tr>
            </tbody>
        </table>
    </body>
    </html>

#####   result: 
![](../img/Asc.png)

#####    HtmlPage1.html(Desc)
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
                    <th>Name</th>
                    <th>Date of Birth</th>
                    <th>Gender</th>
                    <th>Salary</th>
                </tr>
            </thead>
            <tbody>
                <tr ng-repeat="employee in employees | orderBy : 'name' : true">
                    <td>{{ employee.name }}</td>
                    <td>{{ employee.dateOfBirth | date : "dd/MM/yyyy" }}</td>
                    <td>{{ employee.gender }}</td>
                    <td>{{ employee.salary }}</td>
                </tr>
            </tbody>
        </table>
    </body>
    </html>

#####   result: 
![](../img/Desc.png)

##### 写法二：

#####    HtmlPage1.html(Asc)
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
                    <th>Name</th>
                    <th>Date of Birth</th>
                    <th>Gender</th>
                    <th>Salary</th>
                </tr>
            </thead>
            <tbody>
                <tr ng-repeat="employee in employees | orderBy : '+name'">
                    <td>{{ employee.name }}</td>
                    <td>{{ employee.dateOfBirth | date : "dd/MM/yyyy" }}</td>
                    <td>{{ employee.gender }}</td>
                    <td>{{ employee.salary }}</td>
                </tr>
            </tbody>
        </table>
    </body>
    </html>

#####    HtmlPage1.html(Desc)
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
                    <th>Name</th>
                    <th>Date of Birth</th>
                    <th>Gender</th>
                    <th>Salary</th>
                </tr>
            </thead>
            <tbody>
                <tr ng-repeat="employee in employees | orderBy : '-name'">
                    <td>{{ employee.name }}</td>
                    <td>{{ employee.dateOfBirth | date : "dd/MM/yyyy" }}</td>
                    <td>{{ employee.gender }}</td>
                    <td>{{ employee.salary }}</td>
                </tr>
            </tbody>
        </table>
    </body>
    </html>

#####    Script.js(通过下拉列表选择排序的数据)
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
        Order By : <select ng-model="sortColumn">
            <option value="name">Name Asc</option>
            <option value="dateOfBirth">Date of Birth Asc</option>
            <option value="gender">Gender Asc</option>
            <option value="-salary">Salary Desc</option>
        </select>
        <br><br>
        <table>
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Date of Birth</th>
                    <th>Gender</th>
                    <th>Salary</th>
                </tr>
            </thead>
            <tbody>
                <tr ng-repeat="employee in employees | orderBy : sortColumn">
                    <td>{{ employee.name }}</td>
                    <td>{{ employee.dateOfBirth | date : "dd/MM/yyyy" }}</td>
                    <td>{{ employee.gender }}</td>
                    <td>{{ employee.salary }}</td>
                </tr>
            </tbody>
        </table>
    </body>
    </html>

#####   result: 
![](../img/selectData_orderBy.png)