# part 1 - What is AngularJS

## In this session we will learn

### 1.What is AngularJS

    AngularJS is a JavaScript framework that helps build web applications.
####    (https://www.madewithangular.com)

### 2.Benefits of AngularJS

    (1)Dependency Injection 依赖注入
    (2)Two Way Data-Binding 双向数据绑定

![](../img/Model_View.png)

    (3)Testing 测试（单元测试 & 端到端测试）
    (4)Model View Controller 模型 视图 控制器
    (5)Directives,Filters,etc… Directive指令，过滤器，等等
####    (https://angularjs.org-----Download AngularJS)

### 3.A Simple angular example

##### HtmlPage1.html

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <script type="text/javascript" src="../script/angular.min.js"></script>
    </head>
    <body>
        <div ng-app>
            10 + 20 = {{ 10 + 20 }}
        </div>
        <div>
            40 + 50 = {{ 40 + 50 }}
        </div>
    </body>
    </html>

####    result: 
            10 + 20 = 30
            40 + 50 = {{ 40 + 50 }}

##### HtmlPage1.html
    <!DOCTYPE html>
    <html lang="en" ng-app>
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <script type="text/javascript" src="../script/angular.min.js"></script>
    </head>
    <body>
        <div>
            10 + 20 = {{ 10 + 20 }}
        </div>
        <div>
            40 + 50 = {{ 40 + 50 }}
        </div>
    </body>
    </html>

####    result: 
            10 + 20 = 30
            40 + 50 = 90

##### HtmlPage1.html
    <!DOCTYPE html>
    <html lang="en" ng-app>
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <script type="text/javascript" src="../script/angular.min.js"></script>
    </head>
    <body>
        <div>
            {{ 1 == 2 }}
        </div>
        <div>
            {{ 1 == 1 }}
        </div>
    </body>
    </html>

####    result: 
            false
            true

##### HtmlPage1.html
    <!DOCTYPE html>
    <html lang="en" ng-app>
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <script type="text/javascript" src="../script/angular.min.js"></script>
    </head>
    <body>
        <div>
            {{ { name:"fuyun", age:24 }.name }}
        </div>
    </body>
    </html>

####    result: 
            fuyun

##### HtmlPage1.html
    <!DOCTYPE html>
    <html lang="en" ng-app>
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <script type="text/javascript" src="../script/angular.min.js"></script>
    </head>
    <body>
        <div>
            {{ ['fuyun', 'fuxing', 'fujian'][2] }}
        </div>
    </body>
    </html>

####    result: 
            fujian