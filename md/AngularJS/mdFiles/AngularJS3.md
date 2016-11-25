# part 3 - Controllers in AngularJS

## In this session we will learn

### Continue our discussion on controllers in angular
    
The job of the controller is to build a model for the view,the controller does this by attaching the model to the scope,the scope object itself is not the model,it's the data that you attach to the scope is the model.

#####    Script.js
    /// <reference path = "angular.min.js"/>

    var myApp = angular.module("myModule",[]);

    myApp.controller("myController",function($scope){
        var employee = {
            firstName : "Daivd",
            lastName : "Hastings",
            gender : "Male"
        };

        $scope.employee = employee;
    });

#####   HtmlPage1.html
    <!DOCTYPE html>
    <html lang="en" ng-app = "myModule">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <script type="text/javascript" src="../script/angular.min.js"></script>
        <script type="text/javascript" src="../script/Script.js"></script>
    </head>
    <body ng-controller = "myController">
        <div>
            First Name : {{ employee.firstName }}
        </div>
        <div>
            Last Name : {{ employee.lastName }}
        </div>
        <div>
            Gender : {{ employee.gender }}
        </div>
    </body>
    </html>

#####   result: 
######        First Name : Daivd
######        Last Name : Hastings
######        Gender : Male

### What happens if the controller name is misspelled?
(When the error message is not really very readable,we've got a lot of including symbols within that msg and this is a URL.When you click ono this URL,it takes you to another page and then on that page we can actually see in a mite readable error message.Now the first question that comes to our mind is why is this error message not readable,that is because we're using the minified version of the angular script,so if you are in the development environment and if you want you no more meat readable error messages,one option you have is to use the uncompressed version of the Angular script.)

When the controller name is misspelled,2 things happen:
(1)An error is raised.To see the error,use brower developer tools.
(2)The binding expression in the view that are in the scope of the controller will not be evaluated.

#####   HtmlPage1.html
    <!DOCTYPE html>
    <html lang="en" ng-app = "myModule">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <!-- <script type="text/javascript" src="../script/angular.min.js"></script> --><!-- 控制台不能显示可读的错误原因，是由于使用了压缩版的angular.js文件。 -->

![](../img/compressedVersion.png)
![](../img/LinkError.png)

        <script type="text/javascript" src="../script/angular.js"></script><!-- 开发的时候使用非压缩的angular.js文件，在控制台上可以显示可读的错误原因。 -->

![](../img/UncompressedVersion.png)

        <script type="text/javascript" src="../script/Script.js"></script>
    </head>
    <body ng-controller = "myController1">//the controller name is misspelled
        <div>
            First Name : {{ employee.firstName }}
        </div>
        <div>
            Last Name : {{ employee.lastName }}
        </div>
        <div>
            Gender : {{ employee.gender }}
        </div>
    </body>
    </html>

#####   result: 
######        First Name : {{ employee.firstName }}
######        Last Name : {{ employee.lastName }}
######        Gender : {{ employee.gender }}

### What happens if a property name in the binding expression is misspelled?

Expression evaluation in angular is forgiving,meaning if you misspell a property name in the binding expression,angular will not report any error.It will simply return null or undefined.

#####   HtmlPage1.html
    <!DOCTYPE html>
    <html lang="en" ng-app = "myModule">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <!-- <script type="text/javascript" src="../script/angular.min.js"></script> --><!-- 控制台不能显示可读的错误原因，是由于使用了压缩版的angular.js文件。 -->
        <script type="text/javascript" src="../script/angular.js"></script><!-- 开发的时候使用非压缩的angular.js文件，在控制台上可以显示可读的错误原因。 -->
        <script type="text/javascript" src="../script/Script.js"></script>
    </head>
    <body ng-controller = "myController">
        <div>
            First Name : {{ employee.firstName }}
        </div>
        <div>
            Last Name : {{ employee.lastName }}
        </div>
        <div>
            Gender : {{ employee.gende }}//the property name in the binding expression is misspelled
        </div>
    </body>
    </html>

#####   result: 
######        First Name : Daivd
######        Last Name : Hastings
######        Gender : 

### How to create module,controller and register the controller with the module,all in one line?

Use the method chaining mechanism as shown below

#####    Script.js
    /// <reference path = "angular.min.js"/>

    var myApp = angular
                    .module("myModule",[])
                    .controller("myController",function($scope){
                        var employee = {
                            firstName : "Daivd",
                            lastName : "Hastings",
                            gender : "Male"
                        };

                        $scope.employee = employee;
                    });