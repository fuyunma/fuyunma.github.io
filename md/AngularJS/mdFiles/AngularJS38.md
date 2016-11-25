# part 38 - AngularJS cancel route change

## In this session we will learn

    AngularJS cancel route change

<img src="../img/cancelRouteChange1.png" alt="">

<p style="text-indent:30px;">This technique is extremely useful when you have a long form that you're feeling that's for example your field ninety percent of that form and at that point you have accidentally click on one of the navigation links and at that point if that website allows you to navigate to that new route without any sort of confirmation like this,you will lose your unsaved data. On the other hand, at the website displays the confirmation message like this you can click the cancel button and get to stay on the same page and retain your unsaved data.(防止误点击其他的导航栏图标而导致数据的丢失)</p>

<img src="../img/cancelRouteChange2.png" alt="">

<p style="text-indent:30px;">Into this controller function,we're going to inject $scope object and on this $scope object,I'm going to call $on function.now when route navigation occurs in an angular application,there is even that is triggered and that event is $routeChangeStart event.So we want to handle that event using this on function.So the event is $routeChangeStart that's the event we want to handle.So when that event is triggered,this is the function that is called,and this event handle function is going to have three parameters.The first parameter is the event object itself,the second parameter is the next parameter which has information about the next row that we are navigating to and the third parameter is current which has information about the current route that we are on.Now when this event is triggered what we want to do the first thing that we want to do is display a confirmation message like this.To display a confirmation message we are going to use JavaScript confirm function.So what's the message that we want to display to the user? the message is "Are you sure you want to navigate away from this page".So that's the message that we want to display to the user.Now this confirm function is going to display a confirmation message box like this with OK and Cancel button.When we click OK the function will return true,when we click Cancel the function returns false and that's when we want to cancel out change.To cancel out change,we are going to use this event object.So this event object contains information about the event itself which is that all changed event and that's what we want to cancel.To cancel the event,we're going to call preventDefault function on the event object.So that is all the code that is required to cancel it out change in an angular application.</p>

<img src="../img/cancelRouteChange3.png" alt="">

<p style="text-indent:30px;">Now we can also actually exactly the same thing by using another event and that is locationChangeStart event. Whenever route change occurs in an angular application there are two event started to triggered. routeChangeStart which we are handling at the moment and another event is locationChangeStart you can handle a bit of these events to achieve exactly the same thing. The only difference is that the next and current parameters of this event handle function has got the complete next and current URL that we are navigating to.</p>

<img src="../img/cancelRouteChange4.png" alt="">