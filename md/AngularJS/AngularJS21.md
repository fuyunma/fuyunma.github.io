# part 21 - AngularJS anchorscroll example

## In this session we will learn

    $anchorscroll service

##### $anchorscroll service is used to jump to a specified element on the page.

###### $location service hash method appends hash fragments to the URL.

##### $anchorscroll() method reads the hash fragment in the URL and jumps to that element on the page.

###### yOffset property specifies the vertical scroll-offset.

#####    Script.js
    /// <reference path = "angular.min.js"/>

    var myApp = angular
                    .module("demoApp",[])
                    .controller("demoController",function($scope, $location, $anchorScroll){
                        $scope.scrollTo = function(scrollLocation)
                        {
                            $location.hash(scrollLocation);//This location service has got this method called hash,it's going to append whatever you provide to that to the URL using a hash symbol.

                            $anchorScroll.yOffset = 20;//Much space between the element and the browser.

                            $anchorScroll();//This method is going to read what we have in the URL.For example,if we have hash top appended,this anchorScroll method is going to read that hash to fragment and automatically scroll to that element on the page.
                        }
                    });

#####    HtmlPage1.html
    <!DOCTYPE html>
    <html lang="en" ng-app = "demoApp">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <link rel="stylesheet" href="../style/Styles.css">
        <script type="text/javascript" src="../script/angular.min.js"></script>
        <script type="text/javascript" src="../script/Script.js"></script>
    </head>
    <body ng-controller="demoController">
        <button id="top" ng-click="scrollTo('bottom')">Go to bottom of the page</button>
        <br><br>
        <div>
            <b>What is Angular</b>
            <br>
            AngularJS is a JavaScript framework that helps build applications that run in a web
            <br><br>
            <b>Who developed AngularJS</b>
            <br>
            Goole is the company that developed AngularJS. AngularJS is an open source project,
            <br><br>
            AngularJs is an excellent framework for building both Single Page Application(SPA)
            <br><br>
            There is a website, https://www.madewithangular.com, that has the list of web sites
            <br><br>
            <b>What is Angular</b>
            <br>
            AngularJS is a JavaScript framework that helps build applications that run in a web
            <br><br>
            <b>Who developed AngularJS</b>
            <br>
            Goole is the company that developed AngularJS. AngularJS is an open source project,
            <br><br>
            AngularJs is an excellent framework for building both Single Page Application(SPA)
            <br><br>
            There is a website, https://www.madewithangular.com, that has the list of web sites
            <br><br>
            <b>What is Angular</b>
            <br>
            AngularJS is a JavaScript framework that helps build applications that run in a web
            <br><br>
            <b>Who developed AngularJS</b>
            <br>
            Goole is the company that developed AngularJS. AngularJS is an open source project,
            <br><br>
            AngularJs is an excellent framework for building both Single Page Application(SPA)
            <br><br>
            There is a website, https://www.madewithangular.com, that has the list of web sites
            <br><br>
            <b>What is Angular</b>
            <br>
            AngularJS is a JavaScript framework that helps build applications that run in a web
            <br><br>
            <b>Who developed AngularJS</b>
            <br>
            Goole is the company that developed AngularJS. AngularJS is an open source project,
            <br><br>
            AngularJs is an excellent framework for building both Single Page Application(SPA)
            <br><br>
            There is a website, https://www.madewithangular.com, that has the list of web sites
        </div>
        <br>
        <button id="bottom" ng-click="scrollTo('top')">Go to top of the page</button>
    </body>
    </html>

#####    Styles.css
    div{
        width:400px;
        border:1px solid black;
        font-family:Arial;
        font-size:large;
        padding:5px;
    }
