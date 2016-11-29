## AngularJs $interval 和 $timeout

###$interval

window.setInterval的Angular包装形式。Fn是每次延迟时间后被执行的函数。

间隔函数的返回值是一个承诺。这个承诺将在每个间隔刻度被通知，并且到达规定迭代次数后被取消，如果迭代次数未定义，则无限制的执行。通知的值将是运行的迭代次数。取消一个间隔，调用$intreval.cancel(promise)。

备注：当你执行完这项服务后应该把它销毁。特别是当controller或者directive元素被销毁时而$interval未被销毁。你应该考虑到在适当的时候取消interval事件。

####使用：$interval(fn,delay,[count],[invokeApply],[Pass]);

fn:一个将被反复执行的函数。

delay：每次调用的间隔毫秒数值。

count：循环次数的数值，如果没设置，则无限制循环。

invokeApply：如果设置为false，则避开脏值检查，否则将调用$apply。

Pass：函数的附加参数。

####方法：cancel(promise);

取消与承诺相关联的任务。

promise：$interval函数的返回值。

####使用代码：

(function () {
    angular.module("Demo", [])
    .controller("testCtrl",["$interval",testCtrl]);
    function testCtrl($interval){
      var toDo = function () {
          console.log("Hello World");
      };
      $interval(toDo, 3000, 10);
    };
  }());

###$timeout

window.setTimeout的Angular包装形式。Fn函数包装成一个try/catch块，代表$exceptionHandler服务里的任何异常。

timeout函数的返回值是一个promise，当到达设置的超时时间时，这个承诺将被解决，并执行timeout函数。

需要取消timeout，需要调用$timeout.cancel(promise);

####使用： $timeout(fn,[delay],[invokeApply]);

fn：一个将被延迟执行的函数。

delay：延迟的时间（毫秒）。

invokeApply：如果设置为false，则跳过脏值检测，否则将调用$apply。

####方法：cancel(promise);

取消与承诺相关联的任务。这个的结果是，承诺将被以摒弃方式来解决。

promise：$timeout函数返回的承诺。

####使用代码：

(function () {
    angular.module("Demo", [])
    .controller("testCtrl",["$timeout",testCtrl]);
    function testCtrl($timeout){
      var toDo = function () {
          console.log("Hello World");
      };
      $timeout(toDo,5000)
    };
  }());