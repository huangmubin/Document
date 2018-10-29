# 概述

## 优先级

> CSS 样式优先级

一般而言，所有的样式会根据下面的规则层叠于一个新的虚拟样式表中，其中数字 4 拥有最高的优先权。

1. 浏览器缺省设置
2. 外部样式表 `<link rel="stylesheet" type="text/css" href="mystyle.css">`
3. 内部样式表（位于 <head> 标签内部）`<head> <style> body {background-image:url("images/back40.gif");} </style> </head>`
4. 内联样式（在 HTML 元素内部）`<p style="color:sienna;margin-left:20px">这是一个段落。</p>`

> 多重样式优先等级

1. 通用选择器（*）
2. 元素(类型)选择器
3. 类选择器
4. 属性选择器
5. 伪类
6. ID 选择器
7. 内联样式
8. !important 

## 格式

```
Selector { Property : Value; }
```

## 注释

```
/*  这是个注释  */
```

## 选择器

```
<!--  id 选择器  -->
#id { }

<!--  class 选择器  -->
.class { }
```

```
<!--  p 标签中 class="center" 的内容  -->
p.center { }
```

## 盒子模型

```
div {
    /* 元素控件 = 宽度 + 内边距 + 边框 + 外边距 */
    width: 100px;
    padding: 10px;
    border: 5px solid gray;
    margin: 2px;
}
```

### 边框

```
/* 透明边框 */
border-color: transparent;
```

# 属性

## 背景 Background

```
body {
    <!--  red  #fff  rgb(0,0,0)  rgba(0,0,0,0)  -->
    background-color:#b0c4de;
    
    <!--  url  -->
    background-image:url('paper.gif');
    
    <!--  
        repeat : @ x+y
        repeat-x
        repeat-y
        no-repeat
        inherit 继承自父元素
    -->
    background-repeat:repeat-y;
    
    <!--
        scroll	@ 背景图片随页面的其余部分滚动
        fixed	背景图像是固定的
        inherit	指定background-attachment的设置应该从父元素继承
        local	背景图片随滚动元素滚动
    -->
    background-attachment:fixed;
    
    <!--
        只指定一个另一个默认是 center
        水平方向：left  |  center  |  right  |  x%  |  xpos  |  inherit
        垂直方向：top  |  center  |  bottom  |  y%  |  ypos  |  inherit
    -->
    background-position: horizontal vertical;
}
```

```
<!--  快捷  -->
body {
    background: #00ff00 url('smiley.gif') no-repeat fixed center; 
}
```

## 文本 Text

```
p {
    /* 字体颜色 */
    color: blue;
               
    /* 文本对齐方式
    left: 左对齐
    right: 右对齐
    center: 中间对齐
    justify: 两端对齐
    inherit: 继承
    */
    text-align: center;
    
    /* 文本修饰类型
    none: 无修饰 @
    underline: 文本底部线
    overline: 文本顶部线
    line-through: 文本中间线
    blink: 闪烁文本
    inherit: 继承
    */
    text-decoration: none;
    
    /* 文本大小写转换
    none: 默认。定义带有小写字母和大写字母的标准的文本。
    capitalize: 文本中的每个单词以大写字母开头。
    uppercase: 定义仅有大写字母。
    lowercase: 定义无大写字母，仅有小写字母。
    inherit: 规定应该从父元素继承 text-transform 属性的值。
    */
    text-transform: none;
    
    /* 文本缩进
    px: 像素
    %: 百分比
    inheirt: 继承
    */
    text-indent: 50px;
    
    /* 文本间距 */
    word-spacing: 10px;
    
    /* 字符间距 */
    letter-spacing: 10px;
    
    /* 行高 */
    line-height: 40px;
}
```

## 字体 Font

```
p {
    /* 在线生成字体CSS样式工具
     https://www.w3cschool.cn/tools/index?name=csscreate
    */
    
    /* 字体设置，后面的是备用字体，在不支持时往后找 */
    font-family: "Times New Roman", Times, serif;
    
    /* 字体样式
     normal: 正常 @
     italic: 斜体
     */
    font-style: italic;
    
    /* 字体大小
     一般用 px, 也可以用 em
     em 是一个比例大小，比如默认字体或父元素字体是 16px，则 1em = 16px
     body {font-size:100%;}
     h1 {font-size:2.5em;}
     h2 {font-size:1.875em;}
     p {font-size:0.875em;}
     */
    font-size: 20px;
    
    /* 字体粗细
    normal / bold / bolder / lighter
    */
    font-weight: normal;
}
```

## 链接 Link

```
/* @ 未访问过的链接，可以设置所有文本格式，特殊样式 */
a:link {
    color: red;
    background-color: blue;
    text-decoration: underline;
}
/* 已经访问过的链接 */
a:visited {}
/* 鼠标放在链接上时 */
a:hover {}
/* 链接被点击的那一刻 */
a:active {}
```

## 列表 List

```
/* 表格样式 */
ul ol {
    /* 表格列表项目的类型
     none：不使用项目符号
     disc：实心圆
     circle：空心圆
     square：实心方块
     demical：阿拉伯数字
     lower-alpha：小写英文字母
     upper-alpha：大写英文字母
     lower-roman：小写罗马数字
     upper-roman：大写罗马数字
     ... ...
     */
    list-style-type: circle;
    
    /* 表格列表项目的图片 */
    list-style-image: url("");
    
    /* 表格对齐方式 
      inside	列表项目标记放置在文本以内，且环绕文本根据标记对齐。
      outside	默认值。保持标记位于文本的左侧。列表项目标记放置在文本以外，且环绕文本不根据标记对齐。
      inherit	规定应该从父元素继承 list-style-position 属性的值。
      */
     list-style-position: inside;
    
     /* 缩写 */
     list-style: circle inside url("");
}
/* 兼容性表格项目解决方案
 1. 去除掉默认表格标记，然后设置填充和边距。
 2. 设置列表项目背景图片，然后取消重复。
 3. 把列表项目的背景图片定位到标记位置。
 4. 设置文本偏移位置
 */
ul {
    list-style-type: none;
    padding: 0px;
    margin: 0px;
}
ul li {
    background-image: url(sqpurple.gif);
    background-repeat: no-repeat;
    background-position: 0px 5px;
    padding-left: 14px;
}
```

## 表格 Table

```
<!DOCTYPE HTML>
<html>
    <head>
        <meta charset="UTF-8">
        <style>
            table,th,td {
                /* 表格宽高 */
                width: 100px;
                height: 100px;

                /* 颜色 */
                background-color: green;
                color: #000;
                
                /* 文字对齐 */
                text-align: right;
                vertical-align: bottom;

                /*
                 width: 宽度
                 color: 颜色
                 style: 类型
                 collapse: 是否折叠
                 */
                border-width: 5px;
                border-color: yellow;
                border-style: solid;

                /* 可以单独设置一条边，或连写设置四条边。
                颜色
                1个参数，设置4条。
                2个参数，对应上下、左右。
                4个参数，顺时针设置上右下左。
                 */
                border-width: 10px 5px;

                /* 边框是否折叠 */
                border-collapse: collapse;

                /* 表格内容内边距 */
                padding: 10px;
            }
        </style>
    </head>
    <body>
    <table>
        <tr>
            <th>Firstname</th>
            <th>Lastname</th>
        </tr>
        <tr>
            <td>Peter</td>
            <td>Griffin</td>
        </tr>
        <tr>
            <td>Lois</td>
            <td>Griffin</td>
        </tr>
    </table>
    </body>
</html>
```

## 隐藏与显示 Display / Visibility

```
selector {
    /* 隐藏之后依然会占用原来的空间 */
    visibility: hidden;
    /* 隐藏之后就不会占据空间了 */
    display: none;
    /* 变成行内元素 */
    display: inline;
    /* 变成块级元素 */
    display: block;
}
```

## 定位 Position

```
/* 相对浏览器固定，浏览器变化滚动都不变 */
position: fixed;
/* 相对于正常位置进行，默认 */
position: relative;
/* 相对于已经定位的父元素，如果父元素没有定位，则相对 html */
position: absolute;
```

## 过渡 transition

设置元素变化时的过渡动画

transition: property duration timing-function delay;

transition-property	规定设置过渡效果的 CSS 属性的名称。
transition-duration	规定完成过渡效果需要多少秒或毫秒。
transition-timing-function	规定速度效果的速度曲线。
transition-delay	定义过渡效果何时开始。

```
/* 
把鼠标指针放到 div 元素上，其宽度会从 100px 逐渐变为 300px：
*/
div
{
width:100px;
transition: width 2s;
-moz-transition: width 2s; /* Firefox 4 */
-webkit-transition: width 2s; /* Safari 和 Chrome */
-o-transition: width 2s; /* Opera */
}
```

## 阴影 shadow

box-shadow: h-shadow v-shadow blur spread color inset;

h-shadow	必需。水平阴影的位置。允许负值。
v-shadow	必需。垂直阴影的位置。允许负值。
blur	可选。模糊距离。
spread	可选。阴影的尺寸。
color	可选。阴影的颜色。请参阅 CSS 颜色值。
inset	可选。将外部阴影 (outset) 改为内部阴影。

```

```

