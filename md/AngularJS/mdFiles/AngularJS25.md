# part 25 - AngularJS Partial Templates

## In this session we will learn

    Creating the partial templates

###### Add Templates folder, include home.html & courses.html & students.html.

##### home.html
    <h1>{{message}}</h1>
     
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

##### courses.html
    <h1>Courses we offer</h1>
    <ul>
        <li ng-repeat="course in courses">
            {{course}}
        </li>
    </ul>

##### students.html : 

###### The students data is going to come from a database table. So here are the steps

##### Step 1 : Create the database table (tblStudents) and populate it with test data. 

    Create table tblStudents
    (
        Id int primary key identity,
        Name nvarchar(50),
        Gender nvarchar(10),
        City nvarchar(20)
    )
    Go
     
    Insert into tblStudents values ('Mark', 'Male', 'London')
    Insert into tblStudents values ('John', 'Male', 'Chennai')
    Insert into tblStudents values ('Sara', 'Female', 'Sydney')
    Insert into tblStudents values ('Tom', 'Male', 'New York')
    Insert into tblStudents values ('Pam', 'Male', 'Los Angeles')
    Insert into tblStudents values ('Catherine', 'Female', 'Chicago')
    Insert into tblStudents values ('Mary', 'Female', 'Houston')
    Insert into tblStudents values ('Mike', 'Male', 'Phoenix')
    Insert into tblStudents values ('Rosie', 'Female', 'Manchester')
    Insert into tblStudents values ('Sasha', 'Female', 'Hyderabad')
    Go

##### Step 2 : Include the following configuration in web.config file. Notice we have a connection string to the database. We also have enabled HttpGet protocol for ASP.NET web services.

    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <connectionStrings>
        <add name="DBCS"
             connectionString="server=(local);database=SampleDB; integrated security=true"
             providerName="System.Data.SqlClient" />
      </connectionStrings>
      <system.web>
        <webServices>
          <protocols>
            <add name="HttpGet" />
          </protocols>
        </webServices>
      </system.web>
    </configuration>

##### Step 3 : Add a class file to the project. Name it Student.cs. Copy and paste the following code.

    namespace Demo
    {
        public class Student
        {
            public int id { get; set; }
            public string name { get; set; }
            public string gender { get; set; }
            public string city { get; set; }
        }
    }

##### Step 4 : Add an ASMX web service to the project. Name it StudentService.asmx. Copy and paste the following code.

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
        }
    }

##### Step 5 : Right click on the Templates folder and add a new HTML file. Name it students.html. Copy and paste the following. The studentsController will set the students property on the $scope object.

    <h1>List of Students</h1>
    <ul>
        <li ng-repeat="student in students">
            {{student.name}}
        </li>
    </ul>