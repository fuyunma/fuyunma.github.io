# part 27 - Remove # from URL AngularJS

## In this session we will learn

    How to remove # from URLs

##### Step 1 : Enable html5mode routing. To do this inject $locationProvider into config() function in script.js and call html5Mode() method passing true as the argument value. With this change the config function will now look as shown below. 

    .config(function ($routeProvider, $locationProvider) {
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
        $locationProvider.html5Mode(true);
    })

##### Step 2 : In index.html, remove # symbols from all the links. The links in index.html should look as shown below. 

    <a href="home">Home</a>
    <a href="courses">Courses</a>
    <a href="students">Students</a>

##### Step 3 : Include the following URL rewrite rule in web.config. This rewrite rule, rewrites all urls to index.html, except if the request is for a file, or a directory or a Web API request. 

    <system.webServer>
      <rewrite>
        <rules>
          <rule name="RewriteRules" stopProcessing="true">
            <match url=".*" />
            <conditions logicalGrouping="MatchAll">
              <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="true" />
              <add input="{REQUEST_FILENAME}" matchType="IsDirectory" negate="true" />
              <add input="{REQUEST_URI}" pattern="^/(api)" negate="true" />
            </conditions>
            <action type="Rewrite" url="/index.html" />
          </rule>
        </rules>
      </rewrite>
    </system.webServer>

##### Step 4 : Set the base href to the location of your single page application. In the head section of index.html include the following line.

    <base href="/" />