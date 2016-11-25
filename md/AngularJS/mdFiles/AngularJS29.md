# part 29 - AngularJS intellisense in Visual Studio

## In this session we will learn

    How to get better intellisense for Angular in Visual Studio?

###### In the previous videos if you have noticed as we were typing the angular code in Script.js file we were getting some intellisense but it definitely is not good though. For example when we type $routeProvider and then a . (DOT) we were not getting intellisense. 

##### 3 Simple Steps to get better intellisense for angular in visual studio.

##### Step 1 :  Download AngularJS extension for Visual Studio from the following link. The link displays the script in a web page. 

https://raw.githubusercontent.com/jmbledsoe/angularjs-visualstudio-intellisense/master/src/Scripts/angular.intellisense.js

##### Step 2 : Copy and paste the script in a new notepad. Name it angular.intellisense.js and save it to the following folder on your computer

C:\Program Files (x86)\Microsoft Visual Studio 12.0\JavaScript\References 

##### Step 3 : Now drag and drop the following 2 files from Scripts folder onto script.js file
angular.min.js
angular-route.min.js

    Visual Studio will automatically add references to the above 2 files in script.js
    /// <reference path="angular.min.js" />
    /// <reference path="angular-route.min.js" />

###### At this point when we type $routeProvider and then a . (DOT) in the script.js file, we get great intellisense. 