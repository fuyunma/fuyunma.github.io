## word-wrap、word-break和white-space之间的区别：

### 1.word-break 属性规定自动换行的处理方法。

####语法:
    word-break: normal|break-all|keep-all;

    值          描述
    normal      使用浏览器默认的换行规则。
    break-all   允许在单词内换行。
    keep-all    只能在半角空格或连字符处换行。

### 2.word-wrap 属性允许长单词或 URL 地址换行到下一行。

####语法:
    word-wrap: normal|break-word;

    值          描述
    normal      只在允许的断字点换行（浏览器保持默认处理）。
    break-word  在长单词或 URL 地址内部进行换行。

### 3.white-space 属性设置如何处理元素内的空白。

####可能的值：
    
    值          描述
    normal      默认。空白会被浏览器忽略。
    pre         空白会被浏览器保留。其行为方式类似 HTML 中的 <pre> 标签。
    nowrap      文本不会换行，文本会在在同一行上继续，直到遇到 <br> 标签为止。
    pre-wrap    保留空白符序列，但是正常地进行换行。
    pre-line    合并空白符序列，但是保留换行符。
    inherit     规定应该从父元素继承 white-space 属性的值。

### 区别：
    
####（1）word-wrap:break-word;
内容将在边界内换行，仅用于块对象，内联对象要用的话，必须要设定height、width或display:block或position:absolute。
######不会使单词折断，如果剩余空间长度小于单词长度，则单词会在下一行显示。

####（2）word-break:break-all;
用于处理单词折断。(注意与第一个属性的对比)
######会使单词折断，如果剩余空间长度小于单词长度，则单词一部分在剩余空间显示，另一部分在下一行显示。

####（3）white-space:nowrap;
用于处理元素内的空白，只在一行内显示。
######单词不会折断，并且不管剩余部分是否能够容纳单词，单词都会在一行显示。

####（4）overflow:hidden;
超出边界的部分隐藏。

####（5）text-overflow:ellipsis;
超出部分显示省略号。
######超出边界，则会显示省略号。省略号和内容正好占满规定宽度。