# part 18 - $http service in AngularJS

## In this session we will learn

    $http service in Angular

##### $http service is used to make HTTP requests to remote server.

##### $http service is a function that has a single input parameter i.e a configuration object.

    Example : The following example issues a GET request to the specified URL.

    $http({
        method : "GET",
        url : 'EmployeeService.asmx/GetAllEmployees'
    });

##### Complete list of properties supported by the configuration object.
https://docs.angularjs.org/api/ng/service/$http#usage

##### Shortcut methods like get,post,put,delete etc are also available to be used with $http service.
    
    Example :  Using the shortcut method get()

    $http.get('EmployeeService.asmx/GetAllEmployees')

##### $http service returns a promise object

    $scope.employees = $http.get('EmployeeService.asmx/GetAllEmployees');

##### Instead use the then() method

    $scope.employees = $http.get('EmployeeService.asmx/GetAllEmployees')
                            .then(function(response){
                                $scope.employees = response.data;
                            });

##### Use the $log service to log the response object to the console

    $scope.employees = $http.get('EmployeeService.asmx/GetAllEmployees')
                            .then(function(response){
                                $scope.employees = response.data;
                                $log.info(response);
                            });

##### If there is an error processing the request, the errorCallback function is called.

    $scope.employees = $http.get('EmployeeService.asmx/GetAllEmployee')
                            .then(function(response){
                                $scope.employees = response.data;
                            },function(reason){
                                $scope.error = reason.data;
                            });

##### You can also create separate functions and associate them as successCallback and errorCallback functions.

    var successCallBack = function(response){
        $scope.employees = response.data;
    };

    var errorCallBack = function(reason){
        $scope.error = reason.data;
    }

    $scope.employees = $http.get('EmployeeService.asmx/GetAllEmployees')
                            .then(successCallBack,errorCallBack);

##### Default Transformations provided by Angular's http service

###### 1. If the data property of the request configuration object contains a JavaScript object,it is automatically converted into JSON object.

###### 2. If JSON response is detected,it is automatically converted into a JavaScript object.