# part 22 - Angular anchorscroll with database data

## In this session we will learn

    Angular anchorscroll service with database data.

![](../img/anchorscroll.png)

##### Step 1 : Create SQL Server tables and insert data(create data)
    
    Create Table tblCountry
    (
        Id int primary key identity,
        Name nvarchar(50)
    )
    Go
     
    Insert into tblCountry values ('India')
    Insert into tblCountry values ('USA')
    Insert into tblCountry values ('UK')
    Go
     
    Create Table tblCity
    (
        Id int primary key identity,
        Name nvarchar(50),
        CountryId int foreign key references tblCountry(Id)
    )
    Go
     
    Insert into tblCity values ('Mumbai', 1)
    Insert into tblCity values ('Delhi', 1)
    Insert into tblCity values ('Bangalore', 1)
    Insert into tblCity values ('Chennai', 1)
    Insert into tblCity values ('Hyderabad', 1)
    Insert into tblCity values ('New York', 2)
    Insert into tblCity values ('Los Angeles', 2)
    Insert into tblCity values ('Chicago', 2)
    Insert into tblCity values ('Houston', 2)
    Insert into tblCity values ('Philadelphia', 2)
    Insert into tblCity values ('London', 3)
    Insert into tblCity values ('Birmingham', 3)
    Insert into tblCity values ('Coventry', 3)
    Insert into tblCity values ('Liverpool', 3)
    Insert into tblCity values ('Manchester', 3)

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

##### Step 4 : Add a class file to the project. Name it City.cs. Copy and paste the following code.

    namespace Demo
    {
        public class City
        {
            public int Id { get; set; }
            public string Name { get; set; }
            public int CountryId { get; set; }
        }
    }

##### Step 5 : Add a class file to the project. Name it Country.cs. Copy and paste the following code.

    using System.Collections.Generic;
    namespace Demo
    {
        public class Country
        {
            public int Id { get; set; }
            public string Name { get; set; }
            public List<City> Cities { get; set; }
        }
    }

##### Step 6 : Add a new WebService (ASMX). Name it CountryService.asmx. Copy and paste the following code.(WebService code)

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Data;
    using System.Data.SqlClient;
    using System.Web.Script.Serialization;
    using System.Web.Services;
     
    namespace Demo
    {
        [WebService(Namespace = "http://tempuri.org/")]
        [WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1)]
        [System.ComponentModel.ToolboxItem(false)]
        [System.Web.Script.Services.ScriptService]
        public class CountryService : System.Web.Services.WebService
        {
     
            [WebMethod]
            public void GetData()
            {
                List<Country> listCountries = new List<Country>();
     
                string cs = ConfigurationManager.ConnectionStrings["DBCS"].ConnectionString;
                using (SqlConnection con = new SqlConnection(cs))
                {
                    SqlCommand cmd = new SqlCommand("Select * from tblCountry;Select * from tblCity", con);
                    SqlDataAdapter da = new SqlDataAdapter(cmd);
                    DataSet ds = new DataSet();
                    da.Fill(ds);
     
                    DataView dataView = new DataView(ds.Tables[1]);
     
                    foreach (DataRow countryDataRow in ds.Tables[0].Rows)
                    {
                        Country country = new Country();
                        country.Id = Convert.ToInt32(countryDataRow["Id"]);
                        country.Name = countryDataRow["Name"].ToString();
     
                        dataView.RowFilter = "CountryId = '" + country.Id + "'";
     
                        List<City> listCities = new List<City>();
     
                        foreach (DataRowView cityDataRowView in dataView)
                        {
                            DataRow cityDataRow = cityDataRowView.Row;
     
                            City city = new City();
                            city.Id = Convert.ToInt32(cityDataRow["Id"]);
                            city.Name = cityDataRow["Name"].ToString();
                            city.CountryId = Convert.ToInt32(cityDataRow["CountryId"]);
                            listCities.Add(city);
                        }
     
                        country.Cities = listCities;
                        listCountries.Add(country);
                    }
                }
     
                JavaScriptSerializer js = new JavaScriptSerializer();
                Context.Response.Write(js.Serialize(listCountries));
            }
        }
    }

##### Step 7 : Add a new folder to the project. Name it Scripts. Add a new JavaScript file to the Scripts folder. Name it Script.js. Copy and paste the following code.

    /// <reference path="angular.js" /> 
    var demoApp = angular.module("demoApp", [])
                         .controller("countryController",
                            function ($scope, $location, $anchorScroll, $http) {
                             $http.get("CountryService.asmx/GetData")
                                  .then(function (response) {
                                      $scope.countries = response.data;
                                  });
     
                             $scope.scrollTo = function (countryName) {
                                 $location.hash(countryName);
                                 $anchorScroll();
                             }
                         });

##### Step 8 : Add a new stylesheet to the project. Name it Styles.css. Copy and paste the following styles in it. 

    body {
        font-family: Arial;
    }
     
    div {
        display: block;
        font-size: xx-large;
        height: 350px;
        width: 400px;
        border: 1px solid black;
        padding: 10px;
        overflow-y: scroll;
    }

##### Step 9 : Add an HTML page to the ASP.NET project. Copy and paste the following HTML and Angular code.

    <!DOCTYPE html>
    <html xmlns="http://www.w3.org/1999/xhtml" ng-app="demoApp">
    <head>
        <title></title>
        <script src="Scripts/angular.js"></script>
        <script src="Scripts/Script.js"></script>
        <link href="Styles.css" rel="stylesheet" />
    </head>
    <body ng-controller="countryController">
        <span ng-repeat="country in countries">
            <button ng-click="scrollTo(country.Name)">{{country.Name}}</button>
        </span>
        <br /><br />
        <div class="containerDiv">
            <fieldset ng-repeat="country in countries" id="{{country.Name}}">
                <legend>{{country.Name}}</legend>
                <ul>
                    <li ng-repeat="city in country.Cities">
                        {{city.Name}}
                    </li>
                </ul>
            </fieldset>
        </div>
    </body>
    </html>