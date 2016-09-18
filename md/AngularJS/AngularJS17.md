# part 17 - Consuming ASP.NET Web Service in AngularJS using $http

## In this session we will learn

    How to consume an ASP.NET Web Service in an AngularJS application?

![](../img/part17.png)

### Here is what we want to do

###### 1. Create an ASP.NET Web service. This web service retrieves the data from SQL Server database table, returns it in JSON format.
###### 2. Call the web service using AngularJS and display employee data on the web page.

##### Step 1 : Create SQL Server table and insert employee data

    Create table tblEmployees
    (
        Id int primary key identity,
        Name nvarchar(50),
        Gender nvarchar(10),
        Salary int
    )
    Go
     
    Insert into tblEmployees values ('Ben', 'Male', 55000)
    Insert into tblEmployees values ('Sara', 'Female', 68000)
    Insert into tblEmployees values ('Mark', 'Male', 57000)
    Insert into tblEmployees values ('Pam', 'Female', 53000)
    Insert into tblEmployees values ('Todd', 'Male', 60000)
    Go

##### Step 2 : Create new empty asp.net web application project. Name it Demo.

##### Step 3 : Include the following settings in web.config file.

    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <connectionStrings>
        <add name="DBCS"
             connectionString="server=.;database=SampleDB; integrated security=SSPI"/>
      </connectionStrings>
      <system.web>
        <webServices>
          <protocols>
            <add name="HttpGet"/>
          </protocols>
        </webServices>
      </system.web>
    </configuration>

##### Step 4 : Add a class file to the project. Name it Employee.cs. Copy and paste the following code.

    namespace Demo
    {
        public class Employee
        {
            public int id { get; set; }
            public string name { get; set; }
            public string gender { get; set; }
            public int salary { get; set; }
        }
    }

##### Step 5 : Add a new WebService (ASMX). Name it EmployeeService.asmx. Copy and paste the following code.

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
        public class EmployeeService : System.Web.Services.WebService
        {
            [WebMethod]
            public void GetAllEmployees()
            {
                List<Employee> listEmployees = new List<Employee>();
     
                string cs = ConfigurationManager.ConnectionStrings["DBCS"].ConnectionString;
                using (SqlConnection con = new SqlConnection(cs))
                {
                    SqlCommand cmd = new SqlCommand("Select * from tblEmployees", con);
                    con.Open();
                    SqlDataReader rdr = cmd.ExecuteReader();
                    while (rdr.Read())
                    {
                        Employee employee = new Employee();
                        employee.id = Convert.ToInt32(rdr["Id"]);
                        employee.name = rdr["Name"].ToString();
                        employee.gender = rdr["Gender"].ToString();
                        employee.salary = Convert.ToInt32(rdr["Salary"]);
                        listEmployees.Add(employee);
                    }
                }
     
                JavaScriptSerializer js = new JavaScriptSerializer();
                Context.Response.Write(js.Serialize(listEmployees));
            }
        }
    }

##### Step 6 : Add a new folder to the project. Name it Scripts. Download angular.js script file from http://angularjs.org, and past it in Scripts folder. 

##### Step 7 : Add a new JavaScript file to the Scripts folder. Name it Script.js. Copy and paste the following code. 

    /// <reference path="angular.min.js" />
     
    var app = angular
            .module("myModule", [])
            .controller("myController", function ($scope, $http) {
     
                $http.get("EmployeeService.asmx/GetAllEmployees")
                     .then(function (response) {
                         $scope.employees = response.data;
                     });
            });

##### Step 8 : Add a new stylesheet to the project. Name it Styles.css. Copy and paste the following styles in it. 

    body {
        font-family: Arial;
    }
     
    table {
        border-collapse: collapse;
    }
     
    td {
        border: 1px solid black;
        padding: 5px;
    }
     
    th {
        border: 1px solid black;
        padding: 5px;
        text-align: left;
    }

##### Step 9 : Add an HTML page to the ASP.NET project. Copy and paste the following HTML and Angular code 

    <!DOCTYPE html>
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head>
        <title></title>
        <script src="Scripts/angular.js"></script>
        <script src="Scripts/Script.js"></script>
        <link href="Styles.css" rel="stylesheet" />
    </head>
    <body ng-app="myModule">
        <div ng-controller="myController">
            <table>
                <thead>
                    <tr>
                        <th>Id</th>
                        <th>Name</th>
                        <th>Gender</th>
                        <th>Salary</th>
                    </tr>
                </thead>
                <tbody>
                    <tr ng-repeat="employee in employees">
                        <td>{{employee.id}}</td>
                        <td>{{employee.name}}</td>
                        <td>{{employee.gender}}</td>
                        <td>{{employee.salary}}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </body>
    </html>