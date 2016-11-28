.md文件的编辑
=============

##关于标题

规范的README文件开头都写上一个标题，这被称为大标题。

###1.大标题 

==== 

在文本下面加上等于号=，那么上方的文本就变成了大标题（等于号的个数无限制，但一定要大于0个哦(∩_∩)）。

###2.中标题 

--

在文本下面加上减号-，那么上方的文本就变成了中标题，同样，减号个数无限制。

###小结：

使用=、-显示的大、中标题下面都有一条横线。

如果输入的=上方无文字，则只显示一条直线。如果不希望将上方的文字转义为大标题，但又需要在文字下面显示直线，则在文字和=之间插入一个空行即可（补空行：可以避免上下两种不同的布局方式交错在一起。）。

与=不同的是，使用-显示出来的直线是虚线而不是实线。并且只有输入三个或三个以上的-才能显示出直线（同-，*和下划线_也只有输入三个或三个以上才能显示直线）。

###3.标题的等级表示法

分为六个等级，显示的文本从大依次减小。不同等级之间是以井号 # 的个数来标识的。一级标题有一个 #，二级标题有两个# ，以此类推。

#####大标题 <====> 一级标题
#####中标题 <====> 二级标题

<img src="../images/titleGradeShow.png" alt="">

注意：#和标题名称要并排写作一行，显示效果：

#一级标题 

##二级标题 

###三级标题 

####四级标题 

#####五级标题 

######六级标题 

##显示文本

###1.普通文本

直接输入的文字就是普通文本。需要注意的是不能直接通过回车来换行，需要使用&lt;br&gt;(或者&lt;br/&gt;)标签。事实上，markdown支持一些html标签。当然如果完全使用html来写，就失去意义了，毕竟markdown并非专门做前端的，然而仅实现一般效果的话，它会比html写起来要简洁得多。

直接输入URL，就会自动转换为超链接。

###2.显示空格

文本首行缩进空格默认是会被忽略的，如果将输入法从半角转换为全角，就会解决这个问题。

###3.单行文本

使用Tab符实现单行文本（只在一行显示，不会自动换行，显示宽度不够会自动出现水平滚动条）。

![](../images/singleLineText.png)

注意前面有1个Tab。单行文本显示效果如图：

    Hello,大家好，我是fuyun。Hello,大家好，我是fuyun。Hello,大家好，我是fuyun。Hello,大家好，我是fuyun。


###4.多行文本

多行文本和单行文本异曲同工，只要在每行行首加一个Tab。

    欢迎到访
    很高兴见到您 
    祝您，早上好，中午好，下午好，晚安 

###5.部分文字高亮

使一段话中部分文字高亮显示，起到突出强调的作用，那么可以把它用 \` \` 包围起来。注意这不是单引号，而是Tab上方，数字1左边的按键（注意使用英文输入法）。

Thank `You`. Please `Call` Me `Coder`

###6.文字超链接

给一段文字加入超链接的格式: \[ 要显示的文字 \]( 链接的地址 )。比如：

\[我的博客\](https://fuyunma.github.io) 

显示效果：[我的博客](https://fuyunma.github.io) 

还可以加鼠标悬停显示的文本(即在URL之后添加一个用英文双引号括起来的字符串)：

\[我的博客\](https://fuyunma.github.io "fuyunma.github.io") 

显示效果：[我的博客](https://fuyunma.github.io "fuyunma.github.io") 

##插入符号

###1.圆点符

在GitHub的markdown语法里也支持使用圆点符，编辑的时候使用星号*。

![](../images/bullets.png)

要注意的是星号* 后面要有一个空格。否则显示为普通星号。上文的显示效果如图：

* 昵称：果冻虾仁 

* 别名：隔壁老王 

* 英文名：Jelly 

此外还有二级圆点和三级圆点。

![](../images/bulletsGrade.png)

第二行最前面加一个Tab，第三行最前面加两个Tab。这样用来表示层级结构会更加清晰：

* 编程语言 

    * 脚本语言 

        * Python 

###2.缩进

![](../images/indent.png)

显示效果：

>数据结构 

>>树 

>>>二叉树 

>>>>平衡二叉树 

>>>>>满二叉树

##插入图片

###1.来源于网络的图片

!\[](http://www.baidu.com/img/bdlogo.gif) 

即叹号! + 方括号[ ] + 括号( )，其中( )里是图片的URL。

在方括号里可以加入一些标识性的信息，如：

!\[baidu](http://www.baidu.com/img/bdlogo.gif) 

这个方括号里的baidu并不会对图像显示造成任何影响，如果你想达到鼠标悬停显示提示信息，那么可以仿照前面介绍的文本中的方法，如下：

!\[baidu](http://www.baidu.com/img/bdlogo.gif "百度logo") 

在URL后面，加一个双引号包围的字符串，显示效果如图：

![baidu](http://www.baidu.com/img/bdlogo.gif "百度logo") 

###2.GitHub仓库里的图片

考虑到其他来源的网络图片很可能会失效，所以在大多数情况下我们需要显示GitHub仓库(或者项目)里的图片，显示方法如下:

其实与上面的格式基本一致的，所不同的就是括号里的URL该怎么写。

https://github.com/ 你的用户名 / 你的项目名 / raw / 分支名 / 存放图片的文件夹 / 该文件夹下的图片

例如：

!\[](https://github.com/guodongxiaren/ImageCache/raw/master/Logo/foryou.gif) 

用户在GitHub上的用户名guodongxiaren；有一个项目ImageCache；raw表示原数据，无需修改；主分支master；项目里有一个文件夹Logo；Logo文件夹下有一张图片foryou.gif。显示如下：

![](https://github.com/guodongxiaren/ImageCache/raw/master/Logo/foryou.gif)

###3.给图片加上超链接

如果希望图片带有超链接的功能，即点击一个图片进入一个指定的网页，写法如下：

\[!\[](http://www.baidu.com/img/bdlogo.gif "百度Logo")](http://baidu.com)

显示效果:

[![](http://www.baidu.com/img/bdlogo.gif "百度Logo")](http://baidu.com)

##插入代码片段

我们需要在代码的上一行和下一行用\`\`\` 标记。\`\`\`不是单引号，而是数字1左边，Tab键上面的键。要实现语法高亮那么只要在 ``` 之后加上你的编程语言即可（忽略大小写）。c++语言可以写成c++也可以是cpp。看代码：

\`\`\`JavaScript
var box = document.getElementById("box");
\`\`\`

实际显示效果:

```JavaScript
var box = document.getElementById("box");
```


