# part 39 - AngularJS route change events

## In this session we will learn

###### 1.Different events that are triggered when a route change occurs in an angular application.
    
###### 2.Logging the events and event handler parameters to inspect their respective properties.(记录事件和事件处理参数来检查他们各自的属性)

##### When route navigation occurs in an Angular application, the following events are triggered.

    1.$locationChangeStart
    2.$routeChangeStart
    3.$locationChangeSuccess
    4.$routeChangeSuccess

<img src="../img/routeChangeEvents1.png" alt="">

<p style="text-indent:30px;">
    We are going to /courses from there and look at that as soon as a route navigation occurs,those are the four event start that triggered:(按事件触发的先后顺序排序如下)
</p>

    $routeChangeStart
    $locationChangeStart
    $locationChangeSuccess
    $routeChangeSuccess

<img src="../img/routeChangeEvents2.png" alt="">

<p style="text-indent:30px;">
    When we navigate to courses, look at that $routeChangeStart fired and the first parameter here is the event itself. So when we expend this have a lot of information about that event, and then we have the next parameter which contains information about the next route,so we were on /students and we navigated to /courses,so the /courses is the next route. And look at that the next parameter has got $$route and when we expand that, it has got originalPath and look at that originalPath is having a value /courses the URL that we are navigating to the next route. And the third parameter is the current parameter which contains information about the current, again this current parameter has got $$route and it also has got originalPath property which contains information about the current route. So you can inspect these parameters to see all the properties they have. And then we have a $locationChangeStart event.So the first parameter again here is the event itself notice $locationChangeStart, and then look at the next and current parameters. You know next and current parameters have the full next and current URLs.So logging these parameters will definitely give us some valuable information.
</p>