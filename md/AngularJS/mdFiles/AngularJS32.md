# part 32 - AngularJS controller as syntax

## In this session we will learn

    CONTROLLER AS syntax

##### So far we have been using $scope to expose the members from the controller to the view.
    
    app.controller("mainController", function ($scope) {
        $scope.message = "Hello Angular";
    });

##### In the example above we are attaching message property to $scope, which is automatically available in the view.

    <h1 ng-controller="mainController">{{message}}</h1>

##### Another way that is available to expose the members from the controller to the view, is by using CONTROLLER AS syntax. With this syntax, there is no need to inject $scope object in to the controller function, instead you simply use this keyword as shown below.

    app.controller("mainController", function () {
        this.message = "Hello Angular";
    });

##### In the view, you use, CONTROLLER AS syntax as shown below.

    <h1 ng-controller="mainController as main">{{main.message}}</h1>

##### Now, let us see how we can use this CONTROLLER AS syntax in the example that we worked with in Part 31.

###### Code changes in script.js. Notice the changes highlighted in yellow.

1. In the when() function, notice that we are using CONTROLLER AS syntax
2. With in each controller() function we are using this keyword to set the properties that we want to make available in the view
3. Notice in studentsController and studentDetailsController we are assigning this keyword to variable vm. vm stands for ViewModel. You can give it any meaningful name you want.
4. If you use this keyword in then() function as shown below, you would not get the result you expect. That's because 'this' keyword points to the window object when the control comes to then() function. 

    .controller("studentsController", function ($http) {
        $http.get("StudentService.asmx/GetAllStudents")
                            .then(function (response) {
                                this.students = response.data;
                            })
    })

###### At this point we also need to modify all our partial templates

##### Changes in home.html : Use homeCtrl object to retrieve the message property that the homeController has set.

    <h1>{{homeCtrl.message}}</h1>
     
    <div>
        PRAGIM Established in 2000 by 3 S/W engineers offers very cost effective training. PRAGIM Speciality in training arena unlike other training institutions
    </div>
    <ul>
        <li>Training delivered by real time software experts having more than 10 years of experience.</li>
        <li>Realtime projects discussion relating to the possible interview questions.</li>
        <li>Trainees can attend training and use lab untill you get a job.</li>
        <li>Resume preperation and mock up interviews.</li>
        <li>100% placement assistance.</li>
        <li>Lab facility.</li>
    </ul>

##### Changes in courses.html : Use coursesCtrl object to retrieve the courses property that the coursesController has set.

    <h1>Courses we offer</h1>
    <ul>
        <li ng-repeat="course in coursesCtrl.courses">
            {{course}}
        </li>
    </ul>

##### Changes in students.html : Use studentsCtrl object to retrieve the students property that the studentsController has set.

    <h1>List of Students</h1>
    <ul>
        <li ng-repeat="student in studentsCtrl.students">
            <a href="students/{{student.id}}">
                {{student.name}}
            </a>
        </li>
    </ul>

##### Changes in studentDetails.html : Use studentDetailsCtrl object to retrieve the student property that the studentDetailsController has set.

    <h1>Student Details</h1>
    <table style="border:1px solid black">
        <tr>
            <td>Id</td>
            <td>{{studentDetailsCtrl.student.id}}</td>
        </tr>
        <tr>
            <td>Name</td>
            <td>{{studentDetailsCtrl.student.name}}</td>
        </tr>
        <tr>
            <td>Gender</td>
            <td>{{studentDetailsCtrl.student.gender}}</td>
        </tr>
        <tr>
            <td>City</td>
            <td>{{studentDetailsCtrl.student.city}}</td>
        </tr>
    </table>
    <h4><a href="students">Back to Students list</a></h4>

##### You can also use CONTROLLER AS syntax when defining routes as shown below

    var app = angular
                .module("Demo", ["ngRoute"])
                .config(function ($routeProvider, $locationProvider) {
                    $routeProvider
                        .when("/home", {
                            templateUrl: "Templates/home.html",
                            controller: "homeController",
                            controllerAs: "homeCtrl"
                        })
                        .when("/courses", {
                            templateUrl: "Templates/courses.html",
                            controller: "coursesController as coursesCtrl",
                            controllerAs: "coursesCtrl"
                        })
                        .when("/students", {
                            templateUrl: "Templates/students.html",
                            controller: "studentsController as studentsCtrl",
                            controllerAs: "studentsCtrl"
                        })
                        .when("/students/:id", {
                            templateUrl: "Templates/studentDetails.html",
                            controller: "studentDetailsController as studentDetailsCtrl",
                            controllerAs: "studentDetailsCtrl"
                        })
                        .otherwise({
                            redirectTo: "/home"
                        })
                    $locationProvider.html5Mode(true);
                })