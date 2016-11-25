# part 31 - AngularJS page refresh problem

## In this session we will learn

    Page refresh issue

##### What is the issue : When you navigate to http://localhost/students, you will see list of students as shown below 

![](../img/AngularJS_RouteparamsExample.png)

##### Click on any student name. For example when you click on Mark, you will see mark details and the URL in the address bar is http://localhost/students/2

![](../img/passParametersInUrl.png)

##### At this point if you refresh the page by pressing CTRL + F5 or CTRL + R, the student details disappear and the page will be renedered as shown below. 

![](../img/angularjsRoutingRefresh.png)

###### To see the errors, launch the Browser Developer Tools by pressing F12. 

![](../img/refreshPage404.png)

##### To fix this issue all you have to do is place the &lt;base href="/"&gt; element just below the &lt;title&gt; element in the head section of index.html page. 