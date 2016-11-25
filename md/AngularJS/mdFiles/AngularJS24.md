# part 24 - Angular layout template

## In this session we will learn
    
    Creating the layout template

##### The layout page for our example should be as shown below. 

![](../img/angular_layout_template.png)

##### index.html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <script type="text/javascript" src="script/angular.min.js"></script>
        <script type="text/javascript" src="script/angular-route.min.js"></script>
        <link rel="stylesheet" type="text/css" href="style/Styles.css">
        <!-- <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/angularjs/1.5.8/angular.min.js"></script> -->
    </head>
    <body>
        <table style="font-family: Arial">
            <tr>
                <td colspan="2" class="header">
                    <h1>
                        WebSite Header
                    </h1>
                </td>
            </tr>
            <tr>
                <td class="leftMenu">
                    <a href="#/home">Home</a>
                    <a href="#/courses">Courses</a>
                    <a href="#/students">Students</a>
                </td>
                <td class="mainContent">
                    <ng-view></ng-view>
                </td>
            </tr>
            <tr>
                <td colspan="2" class="footer">
                    <b>Website Footer</b>
                </td>
            </tr>
        </table>
    </body>
    </html>

##### Styles.css
    .header {
        width: 800px;
        height: 80px;
        text-align: center;
        background-color:#BDBDBD;
    }
     
    .footer {
        background-color:#BDBDBD;
        text-align: center;
    }
     
    .leftMenu {
        height: 500px;
        background-color:#D8D8D8;
        width: 150px;
    }
     
    .mainContent {
        height: 500px;
        background-color:#E6E6E6;
        width: 650px;
    }
     
    a{
        display:block;
        padding:5px
    }

##### Please note : 

###### 1. The partial templates (home.html, courses.html & students.html) will be injected into the location where we have ng-view directive. 

###### 2. For linking to partial templates we are using # symbol in the href attribute. This tells the browser not to navigate away from index.html.

