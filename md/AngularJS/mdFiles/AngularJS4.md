# part 4 - AngularJS ng-src Directive

## In this session we will learn

Use of ng-src directive

###### Using a binding expression with the image src attribute,results in a 404 error.
That's because as soon as the DOM is in our part at that point a request issued to load that image from the server at that point the angularJS binding expression is not evaluated,so it's using this double curly brace country.flag and closing double curly brace as the part to load the image from and we don't have an image at that part in fact that's not a valid part so that's why we get this 404 error.

###### The image can be found at that part then how is it displaying the image that we see right here?
The reason we're seeing this image because a second request is made in order to load that image after the binding expression that we have specified as the value for the source attribute is evaluated,so in fact,there are two request made to the server to load that image,one is loaded as soon as the dorm is part at that point the binding is expression is not evaluated,so obviously,you know whick is an invalid part here it can't find the image,so we get that 404 error that we see in the developer tools.

![](../img/TwoRequest.png)    

#####    Script.js
    /// <reference path = "angular.min.js"/>

    var myApp = angular
                    .module("myModule",[])
                    .controller("myController",function($scope){
                        var country = {
                            name : "China",
                            capital : "Beijing",
                            flag : "../img/China_flag.jpg"
                        };

                        $scope.country = country;
                    });

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
        <!-- <img src="../img/China_flag.jpg" alt="" style="height:100px; width:150px;"> -->
        <div>
            Name : {{ country.name }}
        </div>
        <div>
            Capital : {{ country.capital }}
        </div>
        <div>
            <img src="{{ country.flag }}" 
                 alt="{{ country.name + ' Flag' }}" 
                 style="height:100px; width:150px;">
        </div>
    </body>
    </html>

#####   result: 
![](../img/ImgSrcError.png)

######Reason for the 404 error:
As soon as the DOM is parsed,an attempt is made is to fetch the image from the server.At this point,AngularJS binding expression that is specified with the src attribute is not evaluated.Hence 404(not found) error.

######To fix the 404 error use the ng-src directive : ng-src attribute ensures that a request is issued only after AngularJS has evaluated the binding expression.

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
            Name : {{ country.name }}
        </div>
        <div>
            Capital : {{ country.capital }}
        </div>
        <div>
            <img ng-src="{{ country.flag }}" 
                 alt="{{ country.name + ' Flag' }}" 
                 style="height:100px; width:150px;">
        </div>
    </body>
    </html>

#####    Script.js
    /// <reference path = "angular.min.js"/>

    var myApp = angular
                    .module("myModule",[])
                    .controller("myController",function($scope){
                        var country = {
                            name : "China",
                            capital : "Beijing",
                            flag : "../img/China_flag1.jpg"
                        };

                        $scope.country = country;
                    });

#####   result: 
![](../img/ImgAlt.png)