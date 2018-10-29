# 概述

HTML 主要用于设置标签。

速查表
https://www.w3cschool.cn/html/html-quicklist.html

## 主要架构

```
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
        <base target="_self">
    </head>
    <body>
    </body>
</html>
```

### \<head>

#### title

* 定义了浏览器工具栏的标题
* 当网页添加到收藏夹时，显示在收藏夹中的标题
* 显示在搜索引擎结果页面的标题

```
<title>Title of the document</title> 
```

#### base

* 标签描述了基本的链接地址/链接目标，该标签作为HTML文档中所有的链接标签的默认链接:

```
<base href="//www.w3cschool.cn/images/" target="_blank">
```

* target - 跳转时的动作
    * _self - 本页跳转
    * _blank - 新开页面

#### link

* 定义了文档与外部资源之间的关系。
* 通常用于链接到样式表

```
<link rel="stylesheet" type="text/css" href="mystyle.css">
```

#### style

* 定义了HTML文档的样式文件引用地址.
* 指定样式文件来渲染HTML文档

```
<style type="text/css">        
    body { background-color:yellow }        
    p { color:black }        
</style>
```

#### meta

* 描述了一些基本的元数据。
* 提供了元数据。元数据也不显示在页面上，但会被浏览器解析。
* 通常用于指定网页的描述，关键词，文件的最后修改时间，作者，和其他元数据。
* 元数据可以使用于浏览器（如何显示内容或重新加载页面），搜索引擎（关键词），或其他Web服务。
* \<meta>一般放置于 \<head>区域

```
// 为搜索引擎定义关键词
<meta name="keywords" content="HTML, CSS, XML, XHTML, JavaScript">

// 为网页定义描述内容
<meta name="description" content="Free Web tutorials on HTML and CSS">

// 定义网页作者
<meta name="author" content="Hege Refsnes">
```

```
// 每30秒钟刷新当前页面
<meta http-equiv="refresh" content="30">
```

#### script

* 用于加载脚本文件，如： JavaScript。

```
<!--  插入 JavaScript  -->
<script>
    document.write("Hello World!")
</script>


<!--  如果浏览器不支持 JavaScript 弹出的提示  -->
<script>
    document.write("Hello World!")
</script>
<noscript>抱歉，你的浏览器不支持 JavaScript!</noscript>
```

## 注释

```
<!-- 这是一个注释 -->
```

## 颜色

```
// 3位16进制
#000

// 6位16进制
#000000

// RGB
rgb(0,0,0)

// RGBA
rgb(0,0,0,0)

// 百分比
rgb(0%, 0%, 0%)
```

## 字符实体

```
显示结果    描述    实体名称    实体编号
       -  空格    - &nbsp;  -  &#160;
    <  -  小于号   - &lt;   - &#60;
    >  -  大于号   - &gt;   - &#62;
    &  -  和号   - &amp;   - &#38;
    "  -  引号   - &quot;  -  &#34;
    '  -  撇号    - &apos; (IE不支持)  -  &#39;
    ￠ -   分   - &cent;   - &#162;
    £  -  镑   - &pound;   - &#163;
    ¥  -  人民币/日元   - &yen;   - &#165;
    €  -  欧元   - &euro;   - &#8364;
    §  -  小节   - &sect;   - &#167;
    ©  -  版权   - &copy;   - &#169;
    ®  -  注册商标   - &reg;   - &#174;
    ™  -  商标   - &trade;   - &#8482;
    ×  -  乘号   - &times;   - &#215;
    ÷  -  除号   - &divide;   - &#247;
```

# 标签

## 标题 Heading

```HTML
    <h1>标题H1-H6</h1>
    <h2>标题H1-H6</h2>
    <h3>标题H1-H6</h3>
    <h4>标题H1-H6</h4>
    <h5>标题H1-H6</h5>
    <h6>标题H1-H6</h6>
```

## 段落 paragraph

```
<p>段落内容</p>
```

## 文本格式化标签 

```
    <p>
        文本（<b>粗体字体 blod</b>）字体对比
        <br />
        文本（<strong>h5 粗体字体，加重语气</strong>）字体对比
    </p><br /><br />

    <p>
        文本（<i>斜体字体 italic</i>）字体对比
        <br />
        文本（<em>h5 斜体字体，重文字</em>）字体对比
    </p><br /><br />

    <p>
        文本（<small>小号字体</small>）字体对比
    </p><br /><br />

    <p>
        文本（<sub>下标字</sub>）字体对比
        <br />
        文本（<sup>上标字</sup>）字体对比
    </p><br /><br />

    <p>
        文本（<ins>插入字</ins>）字体对比
        <br />
        文本（<del>删除字</del>）字体对比
    </p><br /><br />
```

```
<code>定义计算机代码</code>
<kbd>定义键盘码</kbd>
<samp>定义计算机代码样本</samp>
<var>定义变量</var>
<pre>定义预格式文本</pre>

<abbr>定义缩写</abbr>
<address>定义地址</address>
<bdo>定义文字方向</bdo>
<blockquote>定义长的引用</blockquote>
<q>定义短的引用语</q>
<cite>定义引用、引证</cite>
<dfn>定义一个定义项目。</dfn>
```

## 链接 anchor

```
<a href="http://www.w3cschool.cn">这是一个链接</a>
<a href="#">空链接，跳转到页首</a>
<a href="#id">跳转到该页面指定 id 标签位置</a>
<a href="url#id">跳转到指定页面指定 id 标签位置</a>
```

## 图像 image

* 单独设置 width/height 会自动按比例变大缩小。
* src = source - 资源 url
* alt - 资源找不到时显示的填充文本
* usemap - 使用 map 标签

```
<img src="pulpit.jpg" alt="Pulpit rock" width="304" height="228">
```

### 图像点击 map area

可以设置图片当中某些区域能进行点击

```
<img src="planets.gif" width="145" height="126" alt="Planets" usemap="#planetmap"> 

<map name="planetmap"> 
    <area shape="rect" coords="0,0,82,126" alt="Sun" href="sun.gif"> 
    <area shape="circle" coords="90,58,3" alt="Mercury" href="merglobe.gif"> 
    <area shape="circle" coords="124,58,8" alt="Venus" href="venglobe.gif"> 
</map>  
```

## 表格

```
    <p>普通表格</p>

    <table border="1">
        <tr>
            <td>row 1, col 1</td>
            <td>row 1, col 2</td>
        </tr>
        <tr>
            <td>row 2, col 1</td>
            <td>row 2, col 2</td>
        </tr>
    </table>
```

```
    <p>完整表格</p>
    <!--
    align 相对于父视图居中
    cellspacing 单元格间距
    cellpadding 单元格内边距
      -->
    <table border="1" width="400xp" height="200xp" align="center" cellspacing="0" cellpadding="20xp">
        <caption>表格标题</caption>
        <thead>
            <tr>
                <th>head, col 1</th>
                <th>head, col 2</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>row 1, col 1</td>
                <td>row 1, col 2</td>
            </tr>
            <tr>
                <td>row 2, col 1</td>
                <td>row 2, col 2</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td>foot, col 1</td>
                <td>foot, col 2</td>
            </tr>
        </tfoot>
    </table>
```

```
    <p>合并单元格</p>
    <!-- 
    colspan - cell 占据多少列
    rowspan - cell 占据多少行 
    -->
    <table border="1", cellspacing="0", width="400xp", height="400xp">
        <tr>
            <td colspan="2">row 1, col 1</td>
            <!--<td>row 1, col 2</td>-->
            <td>row 1, col 3</td>
        </tr>
        <tr>
            <td rowspan="2">row 2, col 1</td>
            <td>row 2, col 2</td>
            <td>row 2, col 3</td>
        </tr>
        <tr>
            <!--<td>row 2, col 1</td>-->
            <td>row 2, col 2</td>
            <td>row 2, col 3</td>
        </tr>
    </table>
```

## 列表

### 有序列表

```
 <ol>
     <li>Coffee</li>
     <li>Milk</li>
 </ol> 
```

### 无序列表

```
 <ul>
     <li>Coffee</li>
     <li>Milk</li>
 </ul> 
```

### 自定义列表

自定义列表是一个序列列表。

* dt - 序列头，可以有0或多个dd
* dd - 序列体

```
<dl>
    <dt>Coffee
        <dd>- black hot drink</dd>
        <dd>- black hot drink</dd>
    </dt>
    <dt>Milk
        <dd>- white cold drink</dd>
        <dd>- white cold drink</dd>
    </dt>
</dl>
```

## 区块标签

* 区块元素 - 自起一行
    * h / p / ul / table / div
* 内联元素 - 行内
    * b / td / a / img / span

```
<div>
    用于划分界面布局的块
</div>

<span>用于在一行内指定一个小区域</span>
```

## 表单

* form 表单（action: 点击 submit 的时候发送数据到哪里）
    * input 输入框
        * text 明文输入框
        * password 密码输入框
        * radio 单选框
        * checkbox 复选框
        * button 按键
        * submit 提交按钮
        * image 图片按钮
        * hidden 不会显示的标签，用于通过代码静默收集数据
    * label 标签，可以对设置了 id 的 input 进行绑定，点击后开始输入
    * select 列表数据

```
<!-- 表单
    form 表单（action: 点击 submit 的时候发送数据到哪里）
        input 输入框
            text 明文输入框
            password 密码输入框
            radio 单选框
            checkbox 复选框
            button 按键
            submit 提交按钮
            image 图片按钮
            hidden 不会显示的标签，用于通过代码静默收集数据
        label 标签，可以对设置了 id 的 input 进行绑定，点击后开始输入
        select 列表数据
-->

<form action="http://www.baidu.com">
    <!--  普通输入框  -->
    <p> 
        账号： <input type="text" value="默认值", placeholder="填充值">
    </p>
    
    <!--  密码输入框  -->
    <p>
        密码： <input type="password" value="123">
    </p>
    
    <!--  单选输入框，name 设置重复才能互斥，checked 默认选中  -->
    <p>
        类型：
        <input type="radio" name="form_type" checked="checked"> 开启
        <input type="radio" name="form_type"> 关闭
    </p>
    
    <!--  复选输入款  -->
    <p>
        爱好：
        <input type="checkbox"> 网球
        <input type="checkbox"> 羽毛球
    </p>
    
    <!--  按钮  
        submit: 默认的提交按钮，form 的 action 表示会提交的数据到达哪个服务器位置。提交的内容，是一件设置的 name 的标签。格式为 action/?name=value&name=value 
    -->
    <p>
        <input type="button" value="按钮文字" onclick="alert('按钮事件信息')">
        <input type="submit">
    </p>
    
    <!--  图片：点击后也会有 submit 事件  -->
    <p>
        <input type="image" src="_image/xx.png" value="时间" onclick="alert('弹出嘻嘻')">
    </p>
    
    <!--  隐藏输入框  -->
    <p>
        <input type="hidden" value="js 获取数据">
    </p>
    
    <!--  select 标签，下拉列表；selected 默认值  -->
    <select>
        <optgroup label="列表分组 1">
            <option>列表数据 1</option>
            <option>列表数据 2</option>
            <option selected="selected">列表数据 3</option>
        </optgroup>
        <optgroup label="列表分组 2">
            <option>列表数据 1</option>
            <option>列表数据 2</option>
            <option selected="selected">列表数据 3</option>
        </optgroup>
    </select>

    <!-- 多行文本输入框 -->
    <textarea></textarea>
</form>
```

```
<!-- label 标签，把文本跟输入框关联，点击 label 会进入输入框 -->
<form action="">
    <p>
        <label for="account">账号：</label>
        <input type="text" id="account" placeholder="名字">
    </p>
    <p>
        <label for="password">密码：</label>
        <input type="text" id="password">
    </p>
</form>
```

```
<!--  带边框的表单 -->
<form action="">
    <fieldset>
        <!-- 表单名字 -->
        <legend>Personal information:</legend>
        <!-- 内容 -->
        Name: <input type="text" size="30"><br>
        E-mail: <input type="text" size="30"><br>
        Date of birth: <input type="text" size="10">
    </fieldset>
</form>
```

```
<!--  用户输入时弹出提示列表  -->
<form action="/statics/demosource/demo-form.php" method="get">
    <input list="browsers" name="browser">
    <datalist id="browsers">
        <option value="Internet Explorer">
        <option value="Firefox">
        <option value="Chrome">
        <option value="Opera">
        <option value="Safari">
    </datalist>
    <input type="submit">
</form>
<p><strong>注意:</strong> Internet Explorer 9（更早IE版本），Safari不支持 datalist 标签。</p>
```

```
<!--  可用于简单计算的标签 output -->
<form oninput="x.value=parseInt(a.value)+parseInt(b.value)">0
<input type="range" id="a" value="50">100
+<input type="number" id="b" value="50">
=<output name="x" for="a b"></output>
</form>

<p><strong>注意:</strong>  Internet Explorer 不支持 output 标签。</p>
```

## 页面内页面框架

```
<!--  在网页中打开另一个网页  -->
<iframe src="http://www.baidu.com" frameborder="0"></iframe>

<!--  点击后才打开  -->
<iframe src="/statics/demosource/demo_iframe.htm" name="iframe_a"></iframe>
<p><a href="https://www.w3cschool.cn" target="iframe_a">W3CSCHOOL.CN</a></p>
<p><b>注意：</b> 因为 a 标签的 target 属性是名为 iframe_a 的 iframe 框架，所以在点击链接时页面会显示在 iframe框架中。</p>
```

## 媒体

### object embed 辅助插件

辅助应用程序（helper application）是可由浏览器启动的程序。辅助应用程序也称为插件。
辅助程序可用于播放音频和视频（以及其他）。辅助程序是使用 \<object> 标签来加载的。
使用辅助程序播放视频和音频的一个优势是，您能够允许用户来控制部分或全部播放设置。
插件可以通过 \<object> 标签或者 \<embed> 标签添加在页面中。object 和 embed 元素都通过添加对浏览器不直接支持的插件的支持来扩展浏览器的功能。 
大多数辅助应用程序允许对音量设置和播放功能（比如后退、暂停、停止和播放）的手工（或程序的）控制。

```
<!--  插入 flash  -->
<object width="400" height="50" data="/statics/demosource/bookmark.swf"></object>
<embed width="400" height="50" src="bookmark.swf">
```

### Audio 音频

```
<!--  使用 embed -->
<embed height="50" width="100" src="horse.mp3">

<!--  使用 object -->
<object height="50" width="100" data="horse.mp3"></object>

<!--  使用 audio ：先播放 horse.mp3，不行播放 horse.ogg，不然提示失败  -->
<audio controls>
    <source src="horse.mp3" type="audio/mpeg">
    <source src="horse.ogg" type="audio/ogg">
    Your browser does not support this audio format.
</audio>

<!--  最好的解决方案  -->
<audio controls height="100" width="100">
   <source src="horse.mp3" type="audio/mpeg">
   <source src="horse.ogg" type="audio/ogg">
   <embed height="50" width="100" src="horse.mp3">
</audio>
```

### Videos 视频

```
<!--  embed 标签  -->
<embed src="intro.swf" height="200" width="200">

<!--  使用 object -->
<object data="intro.swf" height="200" width="200"></object>

<!--  使用 video ：先播放 movie.mp4，不行播放 movie.ogg，movie.webm，不然提示失败  -->
<video width="320" height="240" controls>
   <source src="movie.mp4" type="video/mp4">
   <source src="movie.ogg" type="video/ogg">
   <source src="movie.webm" type="video/webm">
   Your browser does not support the video tag.
</video>

<!--  最好的解决方案  -->
<video width="320" height="240" controls>
    <source src="movie.mp4" type="video/mp4">
    <source src="movie.ogg" type="video/ogg">
    <source src="movie.webm" type="video/webm">
    <object data="movie.mp4" width="320" height="240">
        <embed src="movie.swf" width="320" height="240">
    </object> 
</video>
```


```

```


```

```


```

```

# 单行标签

```
<hr> - 添加一行横线
<br /> - 换行
```

# CSS

* CSS 添加方式
    * 内联样式 - 在HTML元素中使用"style" 属性
    * 内部样式表 - 在HTML文档头部 <head> 区域使用<style> 元素 来包含CSS
    * 外部引用 - 使用外部 CSS 文件

```
// 内联
 <p style="color:black;margin-left:20px;">This is a paragraph.</p> 
 
 // 内部
 <head>
     <style type="text/css">
         body {background-color:yellow;}
         p {color:black;}
     </style>
 </head>
 
 // 外部
  <head>
     <link rel="stylesheet" type="text/css" href="mystyle.css">
 </head> 
```

# 共用属性

* class:    为html元素定义一个或多个类名（classname）(类名从样式文件引入)
* id:         定义元素的唯一id
* style:    规定元素的行内样式（inline style）
* title:      描述了元素的额外信息 (作为工具条使用)


