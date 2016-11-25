# part 30 - AngularJS Routeparams Example

## In this session we will learn

    How to pass and retrieve parameters from URL in AngularJS?

Here is what we want to do : When we navigate to /students, the list of student names must be displayed as hyperlinks. 

![](../img/AngularJS_RouteparamsExample.png)

When we click on any student name, the respective student details should be displayed as shown below. When we click on "Back to Students list" it should take us back to students list page. 

![](../img/passParametersInUrl.png)

#### Here are the steps to achieve this :

##### Step 1 : The first step is to add a Web Method to our ASP.NET web service, which will retrieve student by their id. Add the following Web Method in StudentService.asmx.cs

    [WebMethod]
    public void GetStudent(int id)
    {
        Student student = new Student();
     
        string cs = ConfigurationManager.ConnectionStrings["DBCS"].ConnectionString;
        using (SqlConnection con = new SqlConnection(cs))
        {
            SqlCommand cmd = new
                SqlCommand("Select * from tblStudents where id = @id", con);
     
            SqlParameter param = new SqlParameter()
            {
                ParameterName = "@id",
                Value = id
            };
     
            cmd.Parameters.Add(param);
     
            con.Open();
            SqlDataReader rdr = cmd.ExecuteReader();
            while (rdr.Read())
            {
                student.id = Convert.ToInt32(rdr["Id"]);
                student.name = rdr["Name"].ToString();
                student.gender = rdr["Gender"].ToString();
                student.city = rdr["City"].ToString();
            }
        }
     
        JavaScriptSerializer js = new JavaScriptSerializer();
        Context.Response.Write(js.Serialize(student));
    }

##### After adding the above method, the complete code in StudentService.asmx.cs should be as shown below.

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Web.Script.Serialization;
    using System.Web.Services;
     
    namespace Demo
    {
        [WebService(Namespace = "http://tempuri.org/")]
        [WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1)]
        [System.ComponentModel.ToolboxItem(false)]
        [System.Web.Script.Services.ScriptService]
        public class StudentService : System.Web.Services.WebService
        {
            [WebMethod]
            public void GetAllStudents()
            {
                List<Student> listStudents = new List<Student>();
     
                string cs = ConfigurationManager.ConnectionStrings["DBCS"].ConnectionString;
                using (SqlConnection con = new SqlConnection(cs))
                {
                    SqlCommand cmd = new SqlCommand("Select * from tblStudents", con);
                    con.Open();
                    SqlDataReader rdr = cmd.ExecuteReader();
                    while (rdr.Read())
                    {
                        Student student = new Student();
                        student.id = Convert.ToInt32(rdr["Id"]);
                        student.name = rdr["Name"].ToString();
                        student.gender = rdr["Gender"].ToString();
                        student.city = rdr["City"].ToString();
                        listStudents.Add(student);
                    }
                }
     
                JavaScriptSerializer js = new JavaScriptSerializer();
                Context.Response.Write(js.Serialize(listStudents));
            }
     
            [WebMethod]
            public void GetStudent(int id)
            {
                Student student = new Student();
     
                string cs = ConfigurationManager.ConnectionStrings["DBCS"].ConnectionString;
                using (SqlConnection con = new SqlConnection(cs))
                {
                    SqlCommand cmd = new
                        SqlCommand("Select * from tblStudents where id = @id", con);
     
                    SqlParameter param = new SqlParameter()
                    {
                        ParameterName = "@id",
                        Value = id
                    };
     
                    cmd.Parameters.Add(param);
     
                    con.Open();
                    SqlDataReader rdr = cmd.ExecuteReader();
                    while (rdr.Read())
                    {
                        student.id = Convert.ToInt32(rdr["Id"]);
                        student.name = rdr["Name"].ToString();
                        student.gender = rdr["Gender"].ToString();
                        student.city = rdr["City"].ToString();
                    }
                }
     
                JavaScriptSerializer js = new JavaScriptSerializer();
                Context.Response.Write(js.Serialize(student));
            }
        }
    }

##### Step 2 : Change the HTML in students.html partial template as shown below. Notice student name is now wrapped in an anchor tag. This will display student name as a hyperlink. If you click on a student name with id = 1, then we will be redirected to /students/1

    <h1>List of Students</h1>
    <ul>
        <li ng-repeat="student in students">
            <a href="students/{{student.id}}">
                {{student.name}}
            </a>
        </li>
    </ul>

##### Step 3 : Now let's create an angularjs route with parameters. Add the following route in script.js file. Our next step is to create studentDetails.html partial template and studentDetailsController.

    .when("/students/:id", {
        templateUrl: "Templates/studentDetails.html",
        controller: "studentDetailsController"
    })

##### With the above change, the code in script.js should now look as shown below. Please pay attention to the code highlighted in yellow.

    /// <reference path="angular.min.js" />
    /// <reference path="angular-route.min.js" />
     
    var app = angular
                .module("Demo", ["ngRoute"])
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
                        .when("/students/:id", {
                            templateUrl: "Templates/studentDetails.html",
                            controller: "studentDetailsController"
                        })
                        .otherwise({
                            redirectTo: "/home"
                        })
                    $locationProvider.html5Mode(true);
                })
                .controller("homeController", function ($scope) {
                    $scope.message = "Home Page";
                })
                .controller("coursesController", function ($scope) {
                    $scope.courses = ["C#", "VB.NET", "ASP.NET", "SQL Server","AngularJS","JavaScript"];
                })
                 .controller("studentsController", function ($scope, $http) {
                     $http.get("StudentService.asmx/GetAllStudents")
                                            .then(function (response) {
                                                $scope.students = response.data;
                                            })
                 })

##### Step 4 : Right click on Templates folder in solution explorer and add a new HTMLpage. Name it studentDetails.html. Copy and paste the following HTML.

    <h1>Student Details</h1>
     
    <table style="border:1px solid black">
        <tr>
            <td>Id</td>
            <td>{{student.id}}</td>
        </tr>
        <tr>
            <td>Name</td>
            <td>{{student.name}}</td>
        </tr>
        <tr>
            <td>Gender</td>
            <td>{{student.gender}}</td>
        </tr>
        <tr>
            <td>City</td>
            <td>{{student.city}}</td>
        </tr>
    </table>
    <h4><a href="students">Back to Students list</a></h4>

##### Step 5 : Add studentDetailsController in script.js which calls GetStudent web method and returns the requested student data.

    .controller("studentDetailsController", function ($scope, $http, $routeParams) {
        $http({
            url: "StudentService.asmx/GetStudent",
            method: "get",
            params: { id: $routeParams.id }
        }).then(function (response) {
            $scope.student = response.data;
        })
    })

##### With the above change, the code in script.js should now look as shown below. Please pay attention to the code highlighted in yellow.

    /// <reference path="angular.min.js" />
    /// <reference path="angular-route.min.js" />
     
    var app = angular
                .module("Demo", ["ngRoute"])
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
                        .when("/students/:id", {
                            templateUrl: "Templates/studentDetails.html",
                            controller: "studentDetailsController"
                        })
                        .otherwise({
                            redirectTo: "/home"
                        })
                    $locationProvider.html5Mode(true);
                })
                .controller("homeController", function ($scope) {
                    $scope.message = "Home Page";
                })
                .controller("coursesController", function ($scope) {
                    $scope.courses = ["C#", "VB.NET", "ASP.NET", "SQL Server"];
                })
                 .controller("studentsController", function ($scope, $http) {
                     $http.get("StudentService.asmx/GetAllStudents")
                                            .then(function (response) {
                                                $scope.students = response.data;
                                            })
                 })
                .controller("studentDetailsController", function ($scope, $http, $routeParams) {
                    $http({
                        url: "StudentService.asmx/GetStudent",
                        method: "get",
                        params: { id: $routeParams.id }
                    }).then(function (response) {
                        $scope.student = response.data;
                    })
                })