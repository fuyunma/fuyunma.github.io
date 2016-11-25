# part 26 - AngularJS Route Configuration

## In this session we will learn

    Configuring routes and creating controllers

##### Right click on the Scripts folder and add a new JavaScript file. Name it script.js. Copy and paste the following code. 

    /// <reference path="angular.min.js" />
     
    var app = angular
                .module("Demo", ["ngRoute"])
                .config(function ($routeProvider) {
                    $routeProvider
                        .when("/home", {
                            templateUrl: "Templates/home.html",
                            controller: "homeController"
                        })
                        .when("/courses", {
                            templateUrl: "Templates/courses.html",
                            controller: "coursesController"
                        })
                        .when("/students", {
                            templateUrl: "Templates/students.html",
                            controller: "studentsController"
                        })
                })
                .controller("homeController", function ($scope) {
                    $scope.message = "Home Page";
                })
                .controller("coursesController", function ($scope) {
                    $scope.courses = ["C#", "VB.NET", "ASP.NET", "SQL Server"];
                })
                 .controller("studentsController", function ($scope, $http) {
                     $http.get("StudentService.asmx/GetAllStudents")
                                            .then(function (response) {
                                                $scope.students = response.data;
                                            })
                 })

##### Changes to index.html 

###### 1. Add a reference to the script.js file in the layout template i.e index.html.

    <script src="Scripts/script.js"></script>

###### 2. Set ng-app="Demo" on the root html element

    <html lang="en" ng-app="Demo">

##### At this point, depending on the URL, the respective partial template will be injected into the layout template in the location where we have ng-view directive. For example if you have index.html#/home, then home.html is injected into index.html. Similarly if you are on index.html#/courses, then course.html is injected into index.html. 