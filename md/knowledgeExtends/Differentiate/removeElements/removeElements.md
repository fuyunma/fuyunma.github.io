## 一、JQuery .remove()

#### .remove( [selector ] )

selector
Type: String
A selector expression that filters the set of matched elements to be removed.
用于过滤要删除的匹配元素集合的选择器表达式。

##### Similar to .empty(), the .remove() method takes elements out of the DOM. Use .remove() when you want to remove the element itself, as well as everything inside it. In addition to the elements themselves, all bound events and jQuery data associated with the elements are removed. To remove the elements without removing data and events, use .detach() instead.

###### Consider the following HTML:

```JavaScript
<div class="container">
  <div class="hello">Hello</div>
  <div class="goodbye">Goodbye</div>
</div>
```

###### We can target any element for removal:

```JavaScript
$( ".hello" ).remove();
```

###### This will result in a DOM structure with the <div> element deleted:

```JavaScript
<div class="container">
  <div class="goodbye">Goodbye</div>
</div>
```

##### If we had any number of nested elements inside &lt;div class="hello"&gt;, they would be removed, too. Other jQuery constructs such as data or event handlers are erased as well.

##### We can also include a selector as an optional parameter. For example, we could rewrite the previous DOM removal code as follows:

```JavaScript
$( "div" ).remove( ".hello" );
```

###### This would result in the same DOM structure:

```JavaScript
<div class="container">
  <div class="goodbye">Goodbye</div>
</div>
```

##### Examples:
###### Removes all paragraphs from the DOM

```JavaScript
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>remove demo</title>
  <style>
  p {
    background: yellow;
    margin: 6px 0;
  }
  </style>
  <script src="https://code.jquery.com/jquery-1.10.2.js"></script>
</head>
<body>
 
<p>Hello</p>
how are
<p>you?</p>
<button>Call remove() on paragraphs</button>
 
<script>
$( "button" ).click(function() {
  $( "p" ).remove();
});
</script>
 
</body>
</html>
```

##### Removes all paragraphs that contain "Hello" from the DOM. Analogous to doing $("p").filter(":contains('Hello')").remove().

```JavaScript
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>remove demo</title>
  <style>
  p {
    background: yellow;
    margin: 6px 0;
  }
  </style>
  <script src="https://code.jquery.com/jquery-1.10.2.js"></script>
</head>
<body>
 
<p class="hello">Hello</p>
how are
<p>you?</p>
<button>Call remove( ":contains('Hello')" ) on paragraphs</button>
 
<script>
$( "button" ).click(function() {
  $( "p" ).remove( ":contains('Hello')" );
});
</script>
 
</body>
</html>
```

## 二、JavaScript移除元素节点

##### 在javascript操作dom树的时候可能会经常遇到增加，删除节点的事情。在一些js框架，如Prototype中，可以用element.remove()来删除一个节点，核心JS中并没有这样的方法，IE中有这样一个方法:removeNode()。

###### 尝试运行下面的代码：
```JavaScript
<div><input onclick="removeNode(this)" type="text" value="点击移除该输入框" /></div>
```

##### 可以发现，这个方法在IE下是好使的，但是在Firefox等标准浏览器中就会报错了 “removeNode is not defined”。

##### 在核心JS中有一个操作DOM节点的方法叫:removeChild()，看名字应该就知道是移除子节点的，那么我们就可以变通一下来实现移除指定的节点了。可以先去找到要删除节点的父节点，然后在父节点中运用removeChild来移除指定的节点。

###### 可以定义一个方法removeElement：

```JavaScript
function removeElement(_element){
    var _parentElement = _element.parentNode;
    if(_parentElement){
        _parentElement.removeChild(_element);  
    }
}
```

###### 运行下面的代码，可以在各种浏览器中正确执行了。

```JavaScript
<script type="text/javascript">
    function removeElement(_element){
        var _parentElement = _element.parentNode;
        if(_parentElement){
            _parentElement.removeChild(_element);
        }
    }
</script>
<div><input onclick="removeElement(this)" type="text" value="点击移除该输入框" /></div> 
```