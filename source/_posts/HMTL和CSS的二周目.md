title: HMTL和CSS的二周目
date: 2015-11-03 21:20:41
categories: 
- 凊筠什么的最厌学了
- Web
tags: [html,css]
---

# html

## 认识标签

```
<html>
    <head>...</head>
    <body>...</body>
</html>
```

1. <html> </html>称为根标签，所有的网页标签都在<html></html>中。
<!-- more -->     
2. <head>标签用于定义文档的头部，它是所有头部元素的容器。头部元素有<title>、<script>、<style>、<link>、<meta>等标签，头部标签在下一小节中会有详细介绍。
        
3. 在`<body>`和`</body>`标签之间的内容是网页的主要内容，如`<h1>`、`<p>`、`<a>`、`<img>`等网页内容标签，在这里的标签中的内容会在浏览器中显示出来。

###  head

```
<head>
    <title>...</title>
    <meta>
    <link>
    <style>...</style>
    <script>...</script>
</head>
```
- title: 网页的标题信息，它会出现在浏览器的标题栏中
- meta:
- link
- style
- script

### body


### 常用标签

|代码|作用|
|-|-|
|`<!--注释文字 -->`|<!--注释文字 -->|
|`<p>段落文本</p>`|<p>段落文本</p>|
|`<hx>标题文本</hx>`|<h1>标题文本</h1>|
|`<em>需要强调的文本</em>`|<em>需要强调的文本</em>|
|`<strong>需要强调的文本</strong>`|<strong>需要强调的文本</strong>|
|`<span>文本</span>`|没有语义，用于设定单独样式，在head-title中设置|
|`<q>引用文本</q>`|短文本引用，解析为双引号|
|`<blockquote>引用文本</blockquote>`|长文本引用，解析为缩进|
|`<br />`|回车|
|`&nbsp;`|空格|
|`<hr />`|分割线|
|`<address>联系地址信息</address>`|可通过CSS设置样式|
|`<code>代码</code>`|代码行|
|`<pre>代码</pre>`|代码段|
|`<ul><li>`|无序列表|
|`<ol><li>`|有序列表|
|`<div>…</div>`|逻辑块|



### div

<div  id="版块名称">…</div>

### table


```
<table>
  <table summary="本表格记录2012年到2013年库存记录，记录包括U盘和耳机库存量">
  <caption>2012年到2013年库存记录</caption>
  <tr>
    <th>产品名称 </th>
    <th>品牌 </th>
    <th>库存量（个） </th>
    <th>入库时间 </th>
  </tr>
  <tr>
    <td>耳机 </td>
    <td>联想 </td>
    <td>500</td>
    <td>2013-1-2</td>
  </tr>
  <tr>
    <td>U盘 </td>
    <td>金士顿 </td>
    <td>120</td>
    <td>2013-8-10</td>
  </tr>
  <tr>
    <td>U盘 </td>
    <td>爱国者 </td>
    <td>133</td>
    <td>2013-3-25</td>
  </tr>
</table>
```

        1、<table>…</table>：整个表格以<table>标记开始、</table>标记结束。
        
        2、<tbody>…</tbody>：当表格内容非常多时，表格会下载一点显示一点，但如果加上<tbody>标签后，这个表格就要等表格内容全部下载完才会显示。如右侧代码编辑器中的代码。
        
        3、<tr>…</tr>：表格的一行，所以有几对tr 表格就有几行。
        
        4、<td>…</td>：表格的一个单元格，一行中包含几对<td>...</td>，说明一行中就有几列。
        
        5、<th>…</th>：表格的头部的一个单元格，表格表头。
        
        6、表格中列的个数，取决于一行中数据单元格的个数。
        
        7、<caption>标题文本</caption>
        
        
### a标签


    <a  href="目标网址"  title="鼠标滑过显示的文本">链接显示的文本</a>
    <img src = "myimage.gif" alt = "My Image" title = "My Image" />


## 与浏览者交互，表单标签

### form

    <form   method="传送方式"   action="服务器文件">



### input

<input></input>


    <form>
       <input type="text/password" name="名称" value="文本" />
    </form>

1. type：
    - 当type="text"时，输入框为文本输入框;
    - 当type="password"时, 输入框为密码输入框。

2. name：为文本框命名，以备后台程序ASP 、PHP使用。

3. value：为文本输入框设置默认值。(一般起到提示作用)

### textarea

<textarea></textarea>

        <textarea  rows="行数" cols="列数">文本</textarea>
    
1. `<textarea>`标签是成对出现的，以`<textarea>`开始，以`</textarea>`结束。

2. cols ：多行输入域的列数。

3. rows ：多行输入域的行数。

4. 在`<textarea></textarea>`标签之间可以输入默认值。

### 单选/多选框
-


    <input   type="radio/checkbox"   value="值"    name="名称"   checked="checked"/>
      
```
<form action="save.php" method="post" >
    <label>性别:</label>
    <label>男</label>
    <input type="radio" value="1"  name="gender" />
    <label>女</label>
    <input type="radio" value="2"  name="gender" />
</form>
```
        
1. type:

   - 当 type="radio" 时，控件为单选框

   - 当 type="checkbox" 时，控件为复选框

2. value：提交数据到服务器的值（后台程序PHP使用）

3. name：为控件命名，以备后台程序 ASP、PHP 使用

4. checked：当设置 checked="checked" 时，该选项被默认选中

### 下拉框

爱好：    <select>
  <option value="看书">看书</option>
  <option value="旅游">旅游</option>
  <option value="运动">运动</option>
  <option value="购物">购物</option>
</select>


```
    <select>
      <option value="看书">看书</option>
      <option value="旅游">旅游</option>
      <option value="运动">运动</option>
      <option value="购物">购物</option>
    </select>
```

### 提交与重置

    <input type="reset" value="重置"  />
    <input type="submit" value="提交"  />


### label标签

    <label for="控件id名称">

注意：标签的 for 属性中的值应当与相关控件的 id 属性值一定要相同。

    <label for="male">男</label>
    <input type="radio" name="gender" id="male" />

# CSS

## 注释
`/*注释语句*/`

## CSS样式

- 内联式CSS
    `<p style="color:red;font-size:12px">这里文字是红色。</p>`

- 嵌入式CSS
```
<style type="text/css">
span{
color:red;
}
</style>
```

- 外部式CSS
`<link href="base.css" rel="stylesheet" type="text/css" />`

优先级：内联式 > 嵌入式 > 外部式

## 选择器


选择器{
    样式;
}

- 类选择器

.类选择器名称{}

    <span class="stress">胆小如鼠</span>
    .stress{color:red;}

- ID选择器

＃ID选择器名称{}

    <span id="setGreen">公开课</span>   
    #setGreen{
       color:green;
    }
    
区别：ID选择器只能在文档中使用一次，类选择器能使用多次

- 子选择器：大于符号(>),用于选择指定标签元素的第一代子元素

    .food>li{border:1px solid red;}
    
- 包含（后代）选择器：加入空格,用于选择指定标签元素下的后辈元素

    .first  span{color:red;}

区别：子选择器仅是指它的直接后代，或者你可以理解为作用于子元素的第一代后代。而后代选择器是作用于所有子后代元素。

- 通用选择器

 *{color:red;}
 
- 伪类选择符：允许给html不存在的标签（标签的某种状态）设置样式
 
 a:hover{color:red;}
 
- 分类选择符

    h1,span{color:red;}
    
    
## 继承、层叠和特殊性

- 继承性
继承是一种规则，它允许样式不仅应用于某个特定html标签元素，而且应用于其后代。

-  特殊性
浏览器是根据权值来判断使用哪种css样式的，权值高的就使用哪种css样式。
标签的权值为1，类选择符的权值为10，ID选择符的权值最高为100。
**注意：**还有一个权值比较特殊--继承也有权值但很低，有的文献提出它只有0.1，所以可以理解为继承的权值最低。

```
p{color:red;} /*权值为1*/
p span{color:green;} /*权值为1+1=2*/
.warning{color:white;} /*权值为10*/
p span.warning{color:purple;} /*权值为1+1+10=12*/
#footer .note p{color:yellow;} /*权值为100+10+1=111*/
```

- 层叠
层叠就是在html文件中对于同一个元素可以有多个css样式存在，当有相同权重的样式存在时，会根据这些css样式的前后顺序来决定，处于最后面的css样式会被应用。

- 重要
某些特殊的情况需要为某些样式设置具有最高权值，可使用!important来解决。
**注意：**!important要在分号前输入
```
p{color:red!important;}
p{color:green;}
<p class="first">三年级时，我还是一个<span>胆小如鼠</span>的小女孩。</p>
```
将显示为红色。

## CSS格式化排版

|名称|用途|
|-|-|
|font-family|字体|
|font-size|大小|
|color|颜色|
|font-weight||
|font-style||
|text-decoration||
|text-indent|缩进|
|line-height|行间距|
|word-spacing|单词间隔|
|letter-spacing|字母间隔|

## CSS盒模型

在CSS中，html中的标签元素大体被分为三种不同的类型：块状元素、内联元素(又叫行内元素)和内联块状元素。

常用的块状元素有：

    <div>、<p>、<h1>...<h6>、<ol>、<ul>、<dl>、<table>、<address>、<blockquote> 、<form>

常用的内联元素有：

    <a>、<span>、<br>、<i>、<em>、<strong>、<label>、<q>、<var>、<cite>、<code>

常用的内联块状元素有：

    <img>、<input>

---

- 块级元素
    - 每个块级元素都从新的一行开始，并且其后的元素也另起一行。（真霸道，一个块级元素独占一行）
    - 元素的高度、宽度、行高以及顶和底边距都可设置。
    - 元素宽度在不设置的情况下，是它本身父容器的100%（和父元素的宽度一致），除非设定一个宽度。
<br />

-  内联元素/行内元素
    - 和其他元素都在一行上；
    - 元素的高度、宽度及顶部和底部边距`不可`设置；
    - 元素的宽度就是它包含的文字或图片的宽度，不可改变；
    - 块状元素也可以通过代码display:inline将元素设置为内联元素。
<br />

- 内联块状元素
    - 和其他元素都在一行上；
    - 元素的高度、宽度、行高以及顶和底边距都可设置。
    
- 盒模型
    - 块状元素都具有盒子模型的特征
    - 边框
        - border-style（边框样式）常见样式有：
        dashed（虚线）| dotted（点线）| solid（实线）。
        - border-color（边框颜色）中的颜色可设置为十六进制颜色，如:
        border-color:#888;//前面的井号不要忘掉。
        - border-width（边框宽度）中的宽度也可以设置为：
         thin | medium |             thick（但不是很常用），最常还是用象素（px）。
        - 四个方向表示为botton、top、right、left，可分别进行设置
    - 宽度和高度
    width和height指的是填充以里的内容范围，因此一个元素实际宽度（盒子的宽度）=左边界margin+左边框border+左填充padding+内容宽度+右填充+右边框+右边界。
    - 填充padding
    元素内容与边框之间是可以设置距离的，称之为“填充”
    - 边界margin
    **注意：** padding在边框里，margin在边框外。
    
## CSS布局模型 ##
布局模型与盒模型一样都是 CSS 最基本、 最核心的概念。 但布局模型是建立在盒模型基础之上，又不同于我们常说的 CSS 布局样式或 CSS 布局模板。如果说布局模型是本，那么 CSS 布局模板就是末了，是外在的表现形式。 

- 流动模型（Flow）
    - 块状元素都会在所处的包含元素内自上而下按顺序垂直延伸分布，因为在默认状态下，块状元素的宽度都为100%。实际上，块状元素都会以行的形式占据位置。
    - 内联元素都会在所处的包含元素内从左到右水平分布显示。
<br />
- 浮动模型 (Float)
float:left/right
- 层模型（Layer）
层布局模型就像是图像软件PhotoShop中非常流行的图层编辑功能一样，每个图层能够精确定位操作.
    - 绝对定位(position: absolute)
    需要设置position:absolute(表示绝对定位)，这条语句的作用将元素从文档流中拖出来，然后使用left、right、top、bottom属性相对于其最接近的一个具有定位属性的父包含块进行绝对定位。如果不存在这样的包含块，则相对于body元素，即相对于浏览器窗口。
    - 相对定位(position: relative)
    相对定位完成的过程是首先按static(float)方式生成一个元素(并且元素像层一样浮动了起来)，然后相对于以前的位置移动，移动的方向和幅度由left、right、top、bottom属性确定，偏移前的位置保留不动
    - 固定定位(position: fixed)
    与absolute定位类型类似，但它的相对移动的坐标是视图（屏幕内的网页窗口）本身。由于视图本身是固定的，它不会随浏览器窗口的滚动条滚动而变化，除非你在屏幕中移动浏览器窗口的屏幕位置，或改变浏览器窗口的显示大小，因此固定定位的元素会始终位于浏览器窗口内视图的某个位置，不会受文档流动影响，这与background-attachment:fixed;属性功能相同。
    
## CSS代码缩写

- 盒模型代码简写
    - 如果top、right、bottom、left的值相同，如下面代码：
    margin:10px 10px 10px 10px;
    可缩写为：`margin:10px;`
    - 如果top和bottom值相同、left和 right的值相同，如下面代码：
    margin:10px 20px 10px 20px;
    可缩写为：`margin:10px 20px;`
    - 如果left和right的值相同，如下面代码：
    margin:10px 20px 30px 20px;
    可缩写为：`margin:10px 20px 30px;`
- 颜色值缩写
关于颜色的css样式也是可以缩写的，当你设置的颜色是16进制的色彩值时，如果每两位的值相同，可以缩写一半。
- 字体缩写

```
        body{
            font:italic  small-caps  bold  12px/1.5em  "宋体",sans-serif;
        }
```

**注意：**
1. 使用这一简写方式你至少要指定 font-size 和 font-family 属性，其他的属性(如 font-weight、font-style、font-varient、line-height)如未指定将自动使用默认值。
2. 在缩写时 font-size 与 line-height 中间要加入“/”斜扛。

## 颜色值
- 英文命令颜色
- RGB颜色
- 十六进制颜色

##长度值
-像素px
-em即font-size值
-百分比

## css样式设置技巧
-  水平居中设置-行内元素
如果被设置元素为文本、图片等行内元素时，水平居中是通过给父元素设置 text-align:center 来实现的。
- 水平居中设置-定宽块状元素
满足定宽和块状两个条件的元素是可以通过设置“左右margin”值为“auto”来实现居中的。

```
    <style>
    div{
        border:1px solid red;/*为了显示居中效果明显为 div 设置了边框*/
        
        width:500px;/*定宽*/
        margin:20px auto;/* margin-left 与 margin-right 设置为 auto */
    }
    </style>
```

- 水平居中总结-不定宽块状元素方法
    - 加入 table 标签
        1. 为需要设置的居中的元素外面加入一个 table 标签 ( 包括 `<tbody>、<tr>、<td>`)。
        2. 为这个 table 设置“左右 margin 居中”（这个和定宽块状元素的方法一样）。
    - 设置 display:inline 方法
    改变块级元素的 display 为 inline 类型，然后使用 text-align:center 来实现居中效果
    - 设置 position:relative 和 left:50%;
    通过给父元素设置 float，然后给父元素设置 position:relative 和 left:50%，子元素设置 position:relative 和 left:-50% 来实现水平居中。

- 垂直居中-父元素高度确定的单行文本
父元素高度确定的单行文本的竖直居中的方法是通过设置父元素的 height 和 line-height 高度一致来实现的。

    height:100px;
    line-height:100px;

- 垂直居中-父元素高度确定的多行文本
    - 使用插入 table (包括tbody、tr、td)标签，同时设置 vertical-align：middle。
    - 在 chrome、firefox 及 IE8 以上的浏览器下可以设置块级元素的 display 为 table-cell，激活 vertical-align 属性，但注意 IE6、7 并不支持这个样式。
    
- 隐性改变display类型