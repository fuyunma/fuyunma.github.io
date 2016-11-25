# part 34 - AngularJS controller as vs scope

## In this session we will learn

    Difference between $scope and CONTROLLER AS syntax

###### CONTROLLER AS syntax is new and is officially released in 1.2.0.$scope is the old technique and is available since the initial version of angular is released.

##### 1.You can use either one of thes techniques.Both have their own uses.For example,CONTROLLER AS syntax makes your code more readable when working with nested scopes.

##### 2.If you want to use $scope it has to be injected into controller function,where as with CONTROLLER AS syntax there is no need for such injection,unless you need it for something else.

###### Which one to use depends purely on your person preference.When you're using CONTROLLER AS syntax,don't be under the impression that angular is not using $scope,angular is still using $scope behind the scenes.It's just hiding that.