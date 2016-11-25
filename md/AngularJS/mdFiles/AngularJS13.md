# part 13 - Create a Custom Filter

## In this session we will learn

    How to create a custom filter in AngularJS (自定义过滤器)

### Custom filter in AngularJs

###### 1.Is a function that returns a function
###### 2.Use the filter function to create a custom filter

### Example:Create a custom filter to convert integer values 1,2,3 to Male,Female and Not disclosed respectively.

#### 写法一：

#####    Script.js
    /// <reference path = "angular.min.js"/>

    var myApp = angular
                    .module("myModule",[])
                    .filter("gender",function(){
                        //      |
                        //filter's name
                        return function(gender){
                                    //    |
                                    //this will be the input for our filter
                                    //in our example,the input is going to be the gender integer values.
                            switch(gender){
                                case 1:
                                    return "Male";
                                case 2:
                                    return "Female";
                                case 3:
                                    return "Not disclosed";
                            }
                        }
                    })
                    .controller("myController",function($scope){
                        var employees = [
                            { name : "Ben", gender : 1, salary : 55000 },
                            { name : "Sara", gender : 2, salary : 68000 },
                            { name : "Mark", gender : 1, salary : 57000 },
                            { name : "Pam", gender : 2, salary : 53000 },
                            { name : "Todd", gender : 3, salary : 60000 }
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
                    <th>Gender</th>
                    <th>Salary</th>
                </tr>
            </thead>
            <tbody>
                <tr ng-repeat="employee in employees">
                    <td>{{ employee.name }}</td>
                    <td>{{ employee.gender | gender }}</td>
                    <td>{{ employee.salary }}</td>
                </tr>
            </tbody>
        </table>
    </body>
    </html>

##### 使用Custom Filter前：
![](../img/noUseCustomFilter.png)
##### 使用Custom Filter后：
![](../img/useCustomFilter.png)

#### 写法二：

#####    Script.js
    /// <reference path = "angular.min.js"/>

    var myApp = angular
                    .module("myModule",[])
                    .controller("myController",function($scope){
                        var employees = [
                            { name : "Ben", gender : 1, salary : 55000 },
                            { name : "Sara", gender : 2, salary : 68000 },
                            { name : "Mark", gender : 1, salary : 57000 },
                            { name : "Pam", gender : 2, salary : 53000 },
                            { name : "Todd", gender : 3, salary : 60000 }
                        ];
                    
                        $scope.employees = employees;
                    });

#####    Filter.js
    /// <reference path = "angular.min.js"/>

    myApp.filter("gender",function(){
            //      |
            //filter's name
        return function(gender){
                    //    |
                    //this will be the input for our filter
                    //in our example,the input is going to be the gender integer values.
            switch(gender){
                case 1:
                    return "Male";
                case 2:
                    return "Female";
                case 3:
                    return "Not disclosed";
            }
        }
    })

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
                    <td>{{ employee.gender | gender }}</td>
                    <td>{{ employee.salary }}</td>
                </tr>
            </tbody>
        </table>
    </body>
    </html>

![](../img/CustomFilter.png)