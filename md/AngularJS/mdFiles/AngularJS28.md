# part 28 - AngularJS Default Route

## In this session we will learn

    How to set a default route in Angular?

###### At the moment the problem is that, if you try to navigate to a route that is not configured, you will see only the layout page without any partial template injected into it. 

###### For example if you navigate to http://localhost:51983/ABC, since ABC is not a configured route you will see the layout page (index.html) as shown below. 

![](../img/AngularJS_DefaultRoute.png)

##### You will also have this same problem if you navigate to the root of the site i.ehttp://localhost:51983. The reason angular is displaying the empty layout template in both these cases, is because it does not know what partial template to inject. We want angular to redirect to default route if the user is trying to navigate to a route that is not configured. 

###### How to configure the default route in Angular : Well that is straight forward. All you need is the following line in config() function in script.js file 

    .otherwise({
        redirectTo: "/home"
    }) 

##### With the above change the code in config() function should be as shown below. 

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
            .otherwise({
                redirectTo: "/home"
            })
        $locationProvider.html5Mode(true);
    })