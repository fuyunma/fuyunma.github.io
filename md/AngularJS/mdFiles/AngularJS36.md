# part 36 - AngularJS route reload

## In this session we will learn

    Angular route service reload() method

##### Angular route service reload() method is useful when you want to reload just the current route instead of the entire app.

    // Controller Code
    .controller("studentsController", function ($http,$route) {
            var vm = this;

            vm.reloadData = function(){
                $route.reload();
            }

            $http.get("StudentService.asmx/GetAllStudents")
                                .then(function (response) {
                                    vm.students = response.data;
                                })
        })

    <!-- View HTML -->
    <button ng-click="studentsCtrl.reloadData()">Reload</button>

######利用 Angular route service 重载方法可以在不重载整个app的情况下，仅载入当前的route.