---
title: html笔记
date: 2021-09-14 14:53:22
tags: summary
categories: HTML
---

```html
<html></html>
```



## 标签

/////成对出现，开始标签和结束标签

```html
<br />
```

////单标签

### 标签分类：

包含（父子）关系和并列关系

```html
<html>
    <head> </head>
    <body> </body>
</html>
```



常用标签：

#### ①语义标签：

```html
<h1> - <h6> ////按重要性递减，都是标题标签，都是占一行的
 <h1 style="text-align:center;"> ....</h1>
    ///代表文本居中的意思

<p> </p> ////段落标签
////不要在<p>里嵌套块级元素，如嵌套p或div
<br/>
```

////换行标签,单标签

e.g:

黄色标记

```
<p><mark>考研宝典</mark></p>
```

#### ②文本格式化标签

```html
   加粗<strong></strong> <b></b>
   倾斜<em></em> <i></i>
   删除线<del></del> <s></s>
   下划线<ins></ins> <u></u>
   下标：<sub></sub> 上标：<sup></sup>

```





（前者语义更强烈）

#### ③无语义（装内容）

```html
<div> division（分区）直接占一行的一个盒子
 e.g:
    <div id="sports">///id属性提供唯一的标识
<span> span(跨度)一行有好几个盒子
style属性定义样式信息
<span style="color: red;">杨倩</span>
```

注释标签：<!--这是一个注释-->



#### 插入...的标签

插入链接标签：  <a>

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title> my html</title>
</head>
<body>
<!--这是一个注释-->
<a href="http://ximena.top">这是一个链接使用了 href 属性</a>

</body>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">

    <title>第一个页面</title>
</head>

<body>
    <!--外部链接-->
    <div style="text-align:center;">
        <div id="top">
            <h1>千古绝句</h1>
            <hr>
            <h2>《赤壁怀古》</h2>
            <p><img
                    src="src=http---i0.hdslb.com-bfs-article-720c7ad1bc307647d4f969d0c33c0215bcd42c72.jpg&refer=http---i0.hdslb.jpg">
            </p>
            <p>苏轼</p>
        </div>
        <div id="content">
            <p>大江东去浪淘尽</p>
            <p>千古风流人物</p>
            <hr>
        </div>
        <div id="footer">
            <a href="#top">返回顶部</a>
        </div>
    </div>

</body>

</html>
```

#### 图片标签

```html
<img src="图片路径" width="宽度值" height="高度值" title="提示文字" alt="替换文本">
```

width和height的单位单位是 为像素点px

title为鼠标放在图像上显示的文本

无法载入图像时显示alt信息 







## 列表


```html
<ul>
<li> … </li>
<li> … </li>
<li> … </li>
</ul>

<ul style="list-style-type: none;">
   默认为实心圆
<li></li>
<li></li>
<li></li>
</ul>
```

list-style-type 样式取值(部分)：

<ul style="list-style-type:">
   <li>none：无标记</li>
    <li>disc：实心圆(默认)</li>
    <li>circle：空心圆</li>
    <li>square：实心方块</li>
    <li>decimal：数字(从1开始)</li>
</ul>



< base >为基本的链接地址和链接目标

该标签作为HTML文档中所有的链接标签的默认链接:

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title> my html</title>
</head>
<body>
<!--这是一个注释-->
<base href="http://ximena.top/friends/" target="_blank">
<a href=""> 这是一个链接 </a>
</body>
</html>
```

## 特殊符号：

```

空格 &nbsp;
< &lt; 
> &gt; 
& &amp;
£ &pound;
¥ &yen;
© &copy;
® &reg;
™ &trade;
× &times;
```

图片标签

```html
<img src="图片路径" width="宽度值" height="高度值" title="提示文字" alt="替换文本">
```

width和height的单位单位是 为像素点px

title为鼠标放在图像上显示的文本

无法载入图像时显示alt信息 





## 表格


<div>
    <table border="1" width="值" height="值">
     <!--边框厚度 和 表格宽度/高度-->
        <tr>
            <th>学号</th> 
            <th>姓名</th> 
            <th>院系</th>
            <th colspan="2">操作</th>
        </tr>
        <tr> 
            <td>2021001</td>
            <td>张无忌</td>
            <td>计算机学院</td>
            <td>编辑</td>
            <td>删除</td>
        </tr>
        <tr> 
            <td>2021002</td>
            <td>令狐冲</td>
            <td>计算机学院</td>
            <td colspan="2"></td>
        </tr>
    </table>
</div>

​     

  源码

```html
<table border="1" width="600px">
<caption>学生名单</caption>
<tr>
    <th>学号</th> 
    <th>姓名</th> 
    <th>院系</th>
    <th colspan="2">操作</th>
    <!--colspan代表了格子所占列-->
</tr>
<tr> 
    <td>2021001</td>
    <td>张无忌</td>
    <td>计算机学院</td>
    <td>编辑</td>
    <td>删除</td>
</tr>
<tr> 
    <td>2021002</td>
    <td>令狐冲</td>
    <td>计算机学院</td>
    <tr colspan="2"></tr>
</tr>

</table>
```

rowspan代表跨几行

## Form表单


form为块级结构，会换行

表单通常用于向指定的 URL 提交用户数据

<form action="URL" method="get或post"
  表单元素.....
 <input type="submit" value="提交">
<input type="reset" value="重填">
</form>

```html
<form action="URL" method="get或post">
表单元素…
<input type="submit" value="提交">
<input type="reset" value="重填">
</form>
```





practise:

<div id="login">
    <form action="data.html" method="get">
        <div>
            <label>
                用户名<input="text" name="username" value="用户名" title="提示信息" >
            </label>
            <span style="color:red">*</span>
        </div>
        <div>
            <label>
                密&nbsp;&nbsp;&nbsp;码
                <input type="password" name="qwd"  maxlength="8" placeholder="长度8个字符">
            </label>
            <span style="color:red">*</span>
        </div>
        <div>
        <input type="submit" value="提交">
        <input type="reset" value="重填">
        </div>
        <div id="tip" style="font-size:12px;">
             <p>说明：用户名和密码必填</p>
        </div>
    </form>
    <form>
        <div>
            <table>
            <input type="radio" name="sex" value="male" checked="checked"> 男
             <!-- check设置为选中状态-->
            <input type="radio" name="sex" value="female">女
            </table>
        </div>
    </form>
</div>


```html
<div id="login">
    <form action="data.html" method="get">
        <div>
            <label>
                用户名<input="text" name="username" value="用户名" title="提示信息" >
            </label>
            <span style="color:red">*</span>
        </div>
        <div>
            <label>
                密&nbsp;&nbsp;&nbsp;码
                <input type="password" name="qwd"  maxlength="8" placeholder="长度8个字符">
            </label>
            <span style="color:red">*</span>
        </div>
        <div>
        <input type="submit" value="提交">
        <input type="reset" value="重填">
        </div>
        <div id="tip" style="font-size:12px;">
             <p>说明：用户名和密码必填</p>
        </div>
        <div>
            <input type="radio" name="sex" value="male" checked="checked"> 男
             <!--check为设置为选中状态-->
            <input type="radio" name="sex" value="female">女
        </div>
    </form>
</div>
```



复选：

<div>
<from>
  爱好： 
<label>
  <input type="checkbox" name="like" value="football">足球
</label>
<label>
<input type="checkbox" name="like" value="basketball">篮球
</label>
</from>




```html
<div>
        <from>
            爱好：
            <label>
                <input type="checkbox" name="like" value="football">足球
            </label>
            <label>
                <input type="checkbox" name="like" value="basketball">篮球
            </label>
        </from>
</div>
```

