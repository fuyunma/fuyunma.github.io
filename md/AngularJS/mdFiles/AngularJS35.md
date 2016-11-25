# part 35 - caseInsensitiveMatch and Inline Templates

## In this session we will learn

    caseInsensitiveMatch

    Inline Templates

##### Routes are case sensitive by default.To make the route case-insensitive set caseInsensitiveMatch property to true.

###### 解决了路径导航时的大小写敏感问题。

<img src="../img/caseInsensitiveMatch.png" alt="">

##### To make all routes case-insensitive set caseInsensitiveMatch property on $routeProvider.

    $routeProvider.caseInsensitiveMatch = true;

###### 如果想要解决所有路径的大小写敏感问题，则应该设置$routeProvider对象的caseInsensiveMatch属性值为true.