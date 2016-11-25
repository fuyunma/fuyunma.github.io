# part 23 - AngularJS Routing Tutorial

## In this session we will learn

    AngularJS routing

###### In general, as the application becomes complex you will have more than one view in the application. Let's say you are building a single page application for a training institute and you have the following views
###### + Home
###### + Courses
###### + Students

We can take advantage of the Angular routing feature, to have a single layout page, and then inject and swap out different views depending on the URL the end user has requested. 

##### So in our application we will have the following views
![](../img/AngularRouting.png) 

##### Please note : The AngularJS Route module is present in a separate JavaScript file.

index.html is the main layout view which controls the layout for our single page application that is the website header, the side panel here, the website footer and the main content area. And then depending on the URL that the end user has requested. For example, if the end user requests /home then this home.html view is automatically injected into this layout here which is index.html. Similarly, if someone request /courses, then courses.html will be injected into index.html. Similarly, someone requests /students, then students.html will be injected into this layout view.

##### What is the CDN link for angular route?

The CDN link is if you go back to the homepage and when we click this download button and look at this, this is the CDN link.
(不需要下载angular.min.js或angular.js文件，通过CDN link可以直接引入外部的angular.min.js或angular.js文件。如果需要引入外部的angular-route.min.js，只需要复制外部的angular.min.js的CDN link并把名称改为angular-route.min.js即可。)

![](../img/CDN_link.png).

#####    index.html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <script type="text/javascript" src="Scripts/angular.min.js"></script>
        <script type="text/javascript" src="Scripts/angular-route.min.js"></script>
        <!-- <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/angularjs/1.5.8/angular-route.min.js"></script> -->
        
        <!-- Preparing the angular application application to use routing : The AngularJS Route module is present in a separate JavaScript file. You can either download it from AngularJs.org and use it in the application or you can use the CDN link. -->
    </head>
    <body>
        
    </body>
    </html>