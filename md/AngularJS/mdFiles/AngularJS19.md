# part 19 - AngularJS Serivces

## In this session we will learn

### 1. What is a service in AngularJS

A service in Angular is simply an object that provide some sort of service that can be reused with in an angular application.

The ambulance service object has properties and methods just like any other JavaScript object.AngularJS has a lot of built-in services.

### 2. Why do we need services in an angular application

The primary responsibility of the controller is to build a model for the view,the controller should not be doing too many things.For example,if the controller also has the logic to compute age from date of birth in addition to building the model,then it while it's one of the solid principles that is the single responsibility principle states that an object should only have a single responsibility,so this kind of logic belongs in its own service which can then be injected into the object that needs that service.

Services encapsulate reusable logic that does not belong anywhere else(i.e Directives,Filters,Views,Models & Controllers).

### 3. What are the benefits of using services

    (1) Reusability 可重用性
    (2) Dependency Injection 依赖注入
    (3) Testability 可测试性