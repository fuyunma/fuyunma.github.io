## 继承与原型链

 JavaScript 是一门动态语言，而且它没有类的概念（ ES6 新增了class 关键字，但只是语法糖，JavaScript 仍旧是基于原型）。

### 原型链：
　　涉及到继承这一块，Javascript 只有一种结构，那就是：对象。在 javaScript 中，每个对象都有一个指向它的原型（prototype）对象的内部链接。这个原型对象又有自己的原型，直到某个对象的原型为 null 为止（也就是不再有原型指向），组成这条链的最后一环。这种一级一级的链结构就称为原型链（prototype chain）。

虽然，原型继承经常被视作 JavaScript 的一个弱点，但事实上，原型继承模型比经典的继承模型更强大。举例来说，在原型继承模型的基础之上建立一个经典的继承模型是相当容易的。

### 基于原型链的继承

#### 继承属性

JavaScript 对象是动态的属性“包”（指其自己的属性）。JavaScript 对象有一个指向一个原型对象的链。当试图访问一个对象的属性时，它不仅仅在该对象上搜寻，还会搜寻该对象的原型，以及该对象的原型的原型，依此层层向上搜索，直到找到一个名字匹配的属性或到达原型链的末尾。

`根据 ECMAScript 标准，someObject.[[Prototype]] 符号是用于指派 someObject 的原型。这个等同于 JavaScript 的 __proto__  属性（现已弃用）。从 ECMAScript 6 开始, [[Prototype]] 可以用Object.getPrototypeOf()和Object.setPrototypeOf()访问器来访问。`

##### 下面的代码将演示，当访问一个对象的属性时会发生的行为：

```JavaScript
// 假定有一个对象 o, 其自身的属性（own properties）有 a 和 b：
// {a: 1, b: 2}
// o 的原型 o.[[Prototype]]有属性 b 和 c：
// {b: 3, c: 4}
// 最后, o.[[Prototype]].[[Prototype]] 是 null.
// 这就是原型链的末尾，即 null，
// 根据定义，null 没有[[Prototype]].
// 综上，整个原型链如下: 
// {a:1, b:2} ---> {b:3, c:4} ---> null

console.log(o.a); // 1
// a是o的自身属性吗？是的，该属性的值为1

console.log(o.b); // 2
// b是o的自身属性吗？是的，该属性的值为2
// o.[[Prototype]]上还有一个'b'属性,但是它不会被访问到.这种情况称为"属性遮蔽 (property shadowing)".

console.log(o.c); // 4
// c是o的自身属性吗？不是，那看看o.[[Prototype]]上有没有.
// c是o.[[Prototype]]的自身属性吗？是的,该属性的值为4

console.log(o.d); // undefined
// d是o的自身属性吗？不是,那看看o.[[Prototype]]上有没有.
// d是o.[[Prototype]]的自身属性吗？不是，那看看o.[[Prototype]].[[Prototype]]上有没有.
// o.[[Prototype]].[[Prototype]]为null，停止搜索，
// 没有d属性，返回undefined
```

创建一个对象它自己的属性的方法就是设置这个对象的属性。唯一例外的获取和设置的行为规则就是当有一个 getter或者一个setter 被设置成继承的属性的时候。

#### 继承方法

JavaScript 并没有其他基于类的语言所定义的“方法”。在 JavaScript 里，任何函数都可以添加到对象上作为对象的属性。函数的继承与其他的属性继承没有差别，包括上面的“属性遮蔽”（这种情况相当于其他语言的方法重写）。

##### 当继承的函数被调用时，this指向的是当前继承的对象，而不是继承的函数所在的原型对象。

```JavaScript
var o = {
  a: 2,
  m: function(){
    return this.a + 1;
  }
};

console.log(o.m()); // 3
// 当调用 o.m 时,'this'指向了o.

var p = Object.create(o);
// p是一个对象, p.[[Prototype]]是o.

p.a = 12; // 创建 p 的自身属性a.
console.log(p.m()); // 13
// 调用 p.m 时, 'this'指向 p. 
// 又因为 p 继承 o 的 m 函数
// 此时的'this.a' 即 p.a，即 p 的自身属性 'a'
```

### 使用不同的方法来创建对象和生成原型链

#### 使用普通语法创建对象

```JavaScript
var o = {a: 1};

// o这个对象继承了Object.prototype上面的所有属性
// 所以可以这样使用 o.hasOwnProperty('a').
// hasOwnProperty 是Object.prototype的自身属性。
// Object.prototype的原型为null。
// 原型链如下:
// o ---> Object.prototype ---> null

var a = ["yo", "whadup", "?"];

// 数组都继承于Array.prototype 
// (indexOf, forEach等方法都是从它继承而来).
// 原型链如下:
// a ---> Array.prototype ---> Object.prototype ---> null

function f(){
  return 2;
}

// 函数都继承于Function.prototype
// (call, bind等方法都是从它继承而来):
// f ---> Function.prototype ---> Object.prototype ---> null
```

#### 使用构造器创建对象

在 JavaScript 中，构造器其实就是一个普通的函数。当使用 new 操作符 来作用这个函数时，它就可以被称为构造方法（构造函数）。

```JavaScript
function Graph() {
  this.vertexes = [];
  this.edges = [];
}

Graph.prototype = {
  addVertex: function(v){
    this.vertexes.push(v);
  }
};

var g = new Graph();
// g是生成的对象,他的自身属性有'vertices'和'edges'.
// 在g被实例化时,g.[[Prototype]]指向了Graph.prototype.
```

#### 使用 Object.create 创建对象

ECMAScript 5 中引入了一个新方法：Object.create()。可以调用这个方法来创建一个新对象。新对象的原型就是调用 create 方法时传入的第一个参数：

```JavaScript
var a = {a: 1}; 
// a ---> Object.prototype ---> null

var b = Object.create(a);
// b ---> a ---> Object.prototype ---> null
console.log(b.a); // 1 (继承而来)

var c = Object.create(b);
// c ---> b ---> a ---> Object.prototype ---> null

var d = Object.create(null);
// d ---> null
console.log(d.hasOwnProperty); // undefined, 因为d没有继承Object.prototype
```

#### 使用 class 关键字

ECMAScript6 引入了一套新的关键字用来实现class。使用基于类语言的开发人员会对这些结构感到熟悉，但它们是不一样的。JavaScript仍然是基于原型的。这些新的关键字包括 class, constructor, static, extends, 和 super.

```JavaScript
"use strict";

class Polygon {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}

class Square extends Polygon {
  constructor(sideLength) {
    super(sideLength, sideLength);
  }
  get area() {
    return this.height * this.width;
  }
  set sideLength(newLength) {
    this.height = newLength;
    this.width = newLength;
  }
}

var square = new Square(2);
```

#### 性能

在原型链上查找属性比较耗时，对性能有副作用，这在性能要求苛刻的情况下很重要。另外，试图访问不存在的属性时会遍历整个原型链。

遍历对象的属性时，原型链上的每个可枚举属性都会被枚举出来。

检测对象的属性是定义在自身上还是在原型链上，有必要使用 hasOwnProperty 方法，所有继承自 Object.proptotype 的对象都包含这个方法。

##### hasOwnProperty是JavaScript中唯一一个只涉及对象自身属性而不会遍历原型链的方法。

###### 注意：仅仅通过判断值是否为undefined还不足以检测一个属性是否存在，一个属性可能存在而其值恰好为undefined。

#### 不好的实践：扩展原生对象的原型

一个经常被用到的错误实践是去扩展 Object.prototype 或者其他内置对象的原型。

该技术被称为 monkey patching，它破坏了原型链的密封性。尽管，一些流行的框架（如 Prototype.js）在使用该技术，但是并没有足够好的理由要用其他非标准的方法将内置的类型系统搞乱。

我们去扩展内置对象原型的唯一理由是引入新的 JavaScript 引擎的某些新特性，比如 Array.forEach。

#### 示例:

B 将继承自 A：

```JavaScript
function A(a){
  this.varA = a;
}

// 以上函数 A 的定义中，既然 A.prototype.varA 总是会被 this.varA 遮蔽，
// 那么将 varA 加入到原型（prototype）中的目的是什么？
A.prototype = {
  varA : null,  // 既然它没有任何作用，干嘛不将 varA 从原型（prototype）去掉？
      // 也许作为一种在隐藏类中优化分配空间的考虑？
      // https://developers.google.com/speed/articles/optimizing-javascript#Initializing instance variables
      // 将会验证如果 varA 在每个实例不被特别初始化会是什么情况。
  doSomething : function(){
    // ...
  }
}

function B(a, b){
  A.call(this, a);
  this.varB = b;
}
B.prototype = Object.create(A.prototype, {
  varB : {
    value: null, 
    enumerable: true, 
    configurable: true, 
    writable: true 
  },
  doSomething : { 
    value: function(){ // override
      A.prototype.doSomething.apply(this, arguments); // call super
      // ...
    },
    enumerable: true,
    configurable: true, 
    writable: true
  }
});
B.prototype.constructor = B;

var b = new B();
b.doSomething();
```

###### 最重要的部分是：

* 类型被定义在 .prototype 中
* 而你用 Object.create() 来继承

### prototype 和 Object.getPrototypeOf

对于从 Java 或 C++ 转过来的开发人员来说 JavaScript 会有点让人困惑，因为它全部都是动态的，都是运行时，而且不存在类（classes）。所有的都是实例（对象）。即使我们模拟出的 “类（classes）”，也只是一个函数对象。

你可能已经注意到，我们的函数 A 有一个特殊的属性叫做原型。这个特殊的属性与 JavaScript 的 new 运算符一起工作。对原型对象的引用会复制到新实例内部的 \[\[Prototype]] 属性。例如，当你这样： var a1 = new A()， JavaScript 就会设置：a1.\[\[Prototype]] = A.prototype（在内存中创建对象后，并在运行 this 绑定的函数 A()之前）。然后在你访问实例的属性时，JavaScript 首先检查它们是否直接存在于该对象中（即是否是该对象的自身属性），如果不是，它会在 \[\[Prototype]] 中查找。也就是说，你在原型中定义的元素将被所有实例共享，甚至可以在稍后对原型进行修改，这种变更将影响到所有现存实例。

像上面的例子中，如果你执行 var a1 = new A(); var a2 = new A(); 那么 a1.doSomething 事实上会指向Object.getPrototypeOf(a1).doSomething，它就是你在 A.prototype.doSomething 中定义的内容。比如：Object.getPrototypeOf(a1).doSomething == Object.getPrototypeOf(a2).doSomething == A.prototype.doSomething。

##### 简而言之， prototype 是用于类型的，而 Object.getPrototypeOf() 是用于实例的（instances），两者功能一致。

\[\[Prototype]] 看起来就像递归引用， 如a1.doSomething，Object.getPrototypeOf(a1).doSomething，Object.getPrototypeOf(Object.getPrototypeOf(a1)).doSomething 等等等， 直到它找到 doSomething 这个属性或者 Object.getPrototypeOf 返回 null。

###### 因此，当你执行：

```JavaScript
var o = new Foo();
```

###### JavaScript 实际上执行的是：

```JavaScript
var o = new Object();
o.[[Prototype]] = Foo.prototype;
Foo.call(o);
```

###### （或者类似上面这样的），然后当你执行：

```JavaScript
o.someProp;
```

它会检查是否存在 someProp 属性。如果没有，它会查找 Object.getPrototypeOf(o).someProp ,如果仍旧没有，它会继续查找 Object.getPrototypeOf(Object.getPrototypeOf(o)).someProp ，一直查找下去，直到它找到这个属性 或者 Object.getPrototypeOf() 返回 null 。

### 结论

在用原型继承编写复杂代码前理解原型继承模型十分重要。同时，还要清楚代码中原型链的长度，并在必要时结束原型链，以避免可能存在的性能问题。此外，除非为了兼容新 JavaScript 特性，否则，永远不要扩展原生的对象原型。