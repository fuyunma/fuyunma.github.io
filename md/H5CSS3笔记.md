##1.H5新增标签 语义化
    头为header 中间为 main 
    1.<aside> 定义页面内容之外的内容。 
    2.<article> 标签定义外部的内容。比如来自一个外部的新闻提供者的一篇新的文章，或者来自 blog 的文本，或者是来自论坛的文本。亦或是来自其他外部源内容
    3.<audio> 标签定义声音，比如音乐或其他音频流
    4.<canvas> 标签定义图形，比如图表和其他图像。
    5.<command> 标签定义命令按钮，比如单选按钮、复选框或按钮。
    定义和用法
    6.<details> 标签定义元素的细节，用户可进行查看，或通过点击进行隐藏。
    7.<footer> 标签定义 section 或 document 的页脚。典型地，它会包含创作者的姓名、文档的创作日期以及/或者联系信息。
    8.<header> 标签定义文档或者文档的一部分区域的页眉。
        <header> 元素应该作为介绍内容或者导航链接栏的容器。
        在一个文档中，您可以定义多个 <header> 元素。
        注释：<header> 标签不能被放在 <footer>、<address> 或者另一个 <header> 元素内部。
    9.<hgroup> 标签用于对网页或区段（section）的标题进行组合。
    10.<section> 标签定义文档中的节（section、区段）。比如章节、页眉、页脚或文档中的其他部分。
    11.<nav> 标签定义导航链接的部分。
    12.<video> 标签定义视频，比如电影片段或其他视频流。
    13.<time> 标签定义日期或时间，或者两者
    14.<figure> 标签用于对元素进行组合。
    15.<figcaption> 元素应该被置于 <figure> 元素的第一个或最后一个子元素的位置。
    16.<datalist> 标签定义可选数据的列表。与 input 元素配合使用，就可以制作出输入值的下拉列表。
    17.<mark> 标签定义带有记号的文本。请在需要突出显示文本时使用 <m> 标签。
    18.<datalist> 标签规定了 <input> 元素可能的数据选项列表。
        <input list="browsers">//list="name"要与datalist中的ID名字一样
        <datalist id="browsers">
            <option value="Internet Explorer">
            <option value="Firefox">
            <option value="Chrome">
            <option value="Opera">
            <option value="Safari">
        </datalist>
##2.快速书写
    .wrap>(header>.top+nav)+aside +section.content+footer
##3.标签权重
    (1).h1>h2>h3....>h6 权重最高
    (2).em==i
    (3).strong==b
    (4).mark
    一个文档一般只能有一个h1 如果用的多了会削弱权重值
    h3不要超过6个
##4.通用文件
    reset.css 清除标签默认样式
    html5.js  为了兼容IE6和IE7,使用js创建h5标签
              使用h5注意事项文件中的文字，将新创建的标签元素变为块元素
    respond.min.js  用于为IE6/IE7/IE8及其它不支持CSS3 Media 
                    Query的浏览器提供媒体查询所需的min-width和max-width特性，实现HTML5标准响应式网页设计
                    （Respond.js越早引入越好）
                    <!--[if lte IE 9 ]>
                        <script src="Respond.min.js"></script>
                    <![endif]--> 
    modernizr.js    Modernizr 检测浏览器对 CSS3 或 HTML5 功能支持情况。  
                    Modernizr 并非试图添加老版本浏览器不支持的功能，
                    而是令你通过创建可选风格配置修改页面设计。 它也可以通过加载定制的脚本来模拟老版本浏览器不支持的功能
##5.CSS3 英文转换
    text-transform:uppercase; 把小写字母转换成为大写字母
    text-transform:none;   默认。定义带有小写字母和大写字母的标准的文本。
    text-transform:capitalize  文本中的每个单词以大写字母开头。
    text-transform:lowercase   定义无大写字母，仅有小写字母。
    text-transform:inherit 规定应该从父元素继承 text-transform 属性的值。
##6.box-shadow text-shadow
    box-shadow(水平，垂直，模糊程度，颜色，内外阴影)
                5px,  5px,  >=5px,   #f00  默认为外阴影 内阴影为inset
##7.HTML5 新的表单属性
    HTML5 的 <form> 和 <input>标签添加了几个新属性.
    ####<form>新属性：
    autocomplete 属性规定 form 或 input 域应该拥有自动完成功能
    novalidate  属性规定在提交表单时不应该验证 form 或 input 域
    ####<input>新属性：
    autocomplete 属性规定 form 或 input 域应该拥有自动完成功能
    autofocus   属性规定在页面加载时，域自动地获得焦点
    form   IE不支持form
    formaction 属性用于描述表单提交的URL地址，属性会覆盖<form> 元素中的action属
    formenctype 
    formmethod 
    formnovalidate 
    formtarget 
    height and width 属性规定用于 image 类型的 <input> 标签的图像高度和宽度。
    list  属性规定输入域的 datalist。datalist 是输入域的选项列表
    min and max 属性用于为包含数字或日期的 input 类型规定限定（约束）。
    multiple 属性规定<input> 元素中可选择多个值
    pattern (regexp) pattern 属性描述了一个正则表达式用于验证 <input> 元素的值
    placeholder  属性提供一种提示（hint），描述输入域所期待的值。
    required 属性规定必须在提交之前填写输入域（不能为空）。
    step 属性为输入域规定合法的数字间隔
##8.单位
    单位      描述
    %         百分比
    in        英寸
    cm        厘米
    mm        毫米
    em        1em 等于当前的字体尺寸。
              2em 等于当前字体尺寸的两倍。
              例如，如果某元素以 12pt 显示，那么 2em 是24pt。
              在 CSS 中，em 是非常有用的单位，因为它可以自动适应用户所使用的字体。
    ex  一个 ex 是一个字体的 x-height。 (x-height 通常是字体尺寸的一半。)
    pt  磅 (1 pt 等于 1/72 英寸)
    pc  12 点活字 (1 pc 等于 12 点)
    px  像素 (计算机屏幕上的一个点)
##9.CSS3 背景
    background-clip     规定背景的绘制区域。  
    background-origin   规定背景图片的定位区域。    
    background-size     规定背景图片的尺寸。 参数：cover contain
##10.清浮动
    1.overflow: hidden 子元素使用float 父级元素的高不会自适应此时加overflow:fidden
    2.万能清浮动：
        .clearfix:before,.clearfix:after{
            display:block;
            content:"";
        }
        .clearfix:after{
            clear:both;
         }
        IE 6需要加上以下代码
        .clearfix{zoon:1;}
    3.clear:both;
##11.各浏览器识别
    -moz-            Firefox            火狐
    -webkit-         Safari 和 Chrome   苹果浏览器 谷歌浏览器
    -o-              Opera              欧朋浏览器
    -ms-             IE                 IE浏览器
##12.样式表过滤
    <!--[if lt IE 7]>      <html class="no-js lt-ie9 lt-ie8 lt-ie7"> <![endif]-->
    <!--[if IE 7]>         <html class="no-js lt-ie9 lt-ie8"> <![endif]-->
    <!--[if IE 8]>         <html class="no-js lt-ie9"> <![endif]-->
    <!--[if ie]>
##13/*针对Firefox*/
    @-moz-document url-prefix() {
        #nav{ width:200px; }
    }
##14/*针对Safari & Chrome*/
    @media screen and (-webkit-min-device-pixel-ratio:0) {
        #nav{ width:300px; }
    }
