## js中instanceof和typeof的区别

##### instanceof和typeof都能用来判断一个变量是否为空或是什么类型的变量。

### 1.typeof

typeof用以获取一个变量的类型。typeof一般只能返回如下几个结果：number,boolean,string,function,object,undefined。

我们可以使用typeof来获取一个变量是否存在，如if(typeof a != "undefined"){}，而不要去使用if(a)因为如果a不存在（未声明）则会出错。对于Array,Null等特殊对象使用typeof 一律返回object，这正是typeof的局限性。

### 2.instanceof

如果我们希望获取一个对象是否是数组，或判断某个变量是否是某个对象的实例则要选择使用instanceof。

instanceof用于判断一个变量是否某个对象的实例，如var a = new Array();alert(a instanceof Array);会返回true。同时alert(a instanceof Object)也会返回true;这是因为Array是object的子类。再如：function test(){};var a=new test();alert(a instanceof test)会返回true。