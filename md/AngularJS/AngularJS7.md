# part 7 - Handling events in AngularJS

## In this session we will learn
    
    How to handle events in AngularJS

    1.Display the list of technologies in a table
    2.Provide the ability to like and dislike a technology
    3.Increment the likes and dislikes when the respective buttons are clicked

#####    Script.js
    /// <reference path = "angular.min.js"/>

    var myApp = angular
                    .module("myModule",[])
                    .controller("myController",function($scope){
                        var technologies = [
                            { name:"C#", likes:0, dislikes:0 },
                            { name:"ASP.NET", likes:0, dislikes:0 },
                            { name:"SQL Server", likes:0, dislikes:0 },
                            { name:"AngularJS", likes:0, dislikes:0 }
                        ];
                    
                        $scope.technologies = technologies;

                        $scope.incrementLikes = function(technology){
                            technology.likes++;
                        }

                        $scope.incrementDislikes = function(technology){
                            technology.dislikes++;
                        }
                    });

    In the controller function we have 2 methods to increment likes and dislikes.Both the functions have the technology object that we want to like or dislike as a parameter.

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
                    <th>Likes</th>
                    <th>Dislikes</th>
                    <th>Like/Dislike</th>
                </tr>
            </thead>
            <tbody>
                <tr ng-repeat="technology in technologies">
                    <td>{{ technology.name }}</td>
                    <td>{{ technology.likes }}</td>
                    <td>{{ technology.dislikes }}</td>
                    <td>
                        <input type="button" value="Like" ng-click="incrementLikes(technology)">
                        <input type="button" value="Dislike" ng-click="incrementDislikes(technology)">
                    </td>
                </tr>
            </tbody>
        </table>
    </body>
    </html>

    IncrementLikes() and IncrementDislikes() function are associated with the respective buttons.When any of these buttons are clicked,the corresponding technology object is automatically passed to the function,and the likes or dislikes property is incremented depending on which button is clicked.

#####    Styles.css
    table{
        border-collapse: collapse;
        font-family: Arial;
    }

    td{
        border:1px solid black;
        padding:5px;
    }

    th{
        border:1px solid black;
        padding:5px;
        text-align:left;
    }

#####   result: 
![](../img/HandlingEvent.png)