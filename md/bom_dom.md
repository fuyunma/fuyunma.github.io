##window对象
    BOM 的核心对象是window，它表示浏览器的一个实例。在浏览器中，window 对象有双重角色，
    它既是通过JavaScript 访问浏览器窗口的一个接口，又是ECMAScript 规定的Global 对象。这意味着
    在网页中定义的任何一个对象、变量和函数，都以window 作为其Global 对象

    全局作用域
    由于 window 对象同时扮演着ECMAScript 中Global 对象的角色，因此所有在全局作用域中声明
    的变量、函数都会变成window 对象的属性和方法

    var age = 29;
    function sayAge(){
    alert(this.age);
    }
    alert(window.age); //29
    sayAge(); //29
    window.sayAge(); //29
    全局变量不能通过delete 操作符删除，而直接在window 对象上的定义的属性可以

    var age = 29;
    window.color = "red";
    //在IE < 9 时抛出错误，在其他所有浏览器中都返回false
    delete window.age;
    //在IE < 9 时抛出错误，在其他所有浏览器中都返回true
    delete window.color; //returns true
    alert(window.age); //29
    alert(window.color); //undefined
    尝试访问未声明的变量会抛出错误，但是通过查询window 对象，可以知道某个可能未声明的变量是否存在


    //这里会抛出错误，因为oldValue 未定义
    var newValue = oldValue;
    //这里不会抛出错误，因为这是一次属性查询
    //newValue 的值是undefined
    var newValue = window.oldValue;
    窗口关系及框架
    如果页面中包含框架，则每个框架都拥有自己的window 对象，并且保存在frames 集合中。在frames
    集合中，可以通过数值索引（从0 开始，从左至右，从上到下）或者框架名称来访问相应的window 对
    象。每个window 对象都有一个name 属性，其中包含框架的名称

    <html>
        <head>
            <title>Frameset Example</title>
            <meta charset="UTF-8">
        </head>
    <frameset rows="160,*">
        <frame src="frames/frame1.html" name="topFrame">
        <frameset cols="50%,50%">
            <frame src="frames/frame2.html" name="leftFrame">
            <frame src="frames/frame3.html" name="rightFrame">
        </frameset>
    </frameset>
    </html>
    以上代码创建了一个框架集，其中一个框架居上，两个框架居下。对这个例子而言，可以通过
    window.frames[0]或者window.frames["topFrame"]来引用上方的框架。不过，恐怕你最好使用
    top 而非window 来引用这些框架（例如，通过top.frames[0]）,top 对象始终指向最高（最外）层的框架，也就是浏览器窗口,与top相对的是parent,parent指向的是父框架

    窗口位置
    使用下列代码可以跨浏览器取得窗口左边和上边的位置。

    var leftPos = (typeof window.screenLeft == "number") ?
    window.screenLeft : window.screenX;
    var topPos = (typeof window.screenTop == "number") ?
    window.screenTop : window.screenY;
    系统对话框
    系统对话框有三个,分别为:alert,confirm,prompt.
    alert为系统提示框

    alert('nice to meet you');
    confirm为确认框

    var sure = confirm('are you have a good time ?');
    if(sure){
    alert('yes, you have a good time !');
    }
    prompt为系统输入框

    var getname = prompt('what's you name ?','name');//参数1为提示语, 参数2为默认字符.
    alert(getname);
    间歇调用和超时调用
    间歇调用使用setTimeout方法,超时调用使用setInterval方法
    这两个方法都有两个参数,第一个参数为执行的代码或函数,第二个参数为执行时间.
    当然这两种调用也有对应的方法来清除调用.

     setTimeout(function(){ alert('good morning!'); },1000); //一秒后弹出弹框.
     
     var count = 0;
     var interval =  setInterval(function(){      
        count++;
        if(count > 10){
             clearInterval(interval);  //清除间歇调用
            }
     },1000); 
    setInterval有个不足之处是后一个间歇调用可能会在前一个间歇调用结束之前启动,因此使用setTimeout来模拟setInterval是不错的选择.

    var count = 0; 
    function doSoming(){
        count ++;
        if(count<=10){
     setTimeout(doSoming,1000);    
    }
    }
    setTimeout(doSoming,1000);
    获取窗口大小
    通过以下代码可以跨浏览器获取页面视口大小

    var pageWidth = window.innerWidth,
        pageHeight = window.innerHeight;
    if(typeof pageWidth !="number"){
        if (document.compatMode == "CSS1Compat"){
            pageWidth = document.documentElement.clientWidth;
            pageHeight = document.documentElement.clientHeight;
            }
        else {
            pageWidth = document.body.clientWidth;
            pageHeight = document.body.clientHeight;
         }
    }


##location对象
    location 是最有用的BOM对象之一，它提供了与当前窗口中加载的文档有关的信息，还提供了一些导航功能
    以下是location对象的属性列表.

    hash 返回URL中的hash（#号后跟零或多个字符），如果URL中不包含散列，则返回空字符串,例"#contents"
    host 返回服务器名称和端口号(如果有).例"www.zhaosywz.com:80"
    hostname 返回不带端口号的服务器名称.例"www.zhaosywz.com"
    href 返回当前页面的完整url.例"www.zhaosywz.com/index.html"
    pathname 返回url中的目录或文件名,例"/category/shoes"
    port 返回url的端口号,如果没有则返回空字符串.例"8080"
    protocol 返回页面使用的协议。通常是http:或https:
    search 返回URL的查询字符串。这个字符串以问号开头,'?id=100'
## navigator对象
    最早由 Netscape Navigator 2.0 引入的navigator 对象，现在已经成为识别客户端浏览器的事实标准,navigator有以下跨浏览器属性和方法.

    appCodeName 浏览器的名称。通常都是Mozilla，即使在非Mozilla浏览器中也是如此
    appName 完整的浏览器名称
    appVersion 浏览器版本，一般不与实际的浏览器版本对应.
    cookieEnabled 表示cookie是否启用
    javaEnabled() 表示单签浏览器是否启用Java
    onLine 表示浏览器是否连接到了因特网
    mimeTypes 在浏览器中注册的MIME类型数组
    platform 浏览器的系统平台
    plugins 浏览器中安装的插件信息的数组
    userAgent 浏览器用户代理字符串
    userAgent是最常用的属性.