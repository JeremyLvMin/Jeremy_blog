---
title: test
date: 2017-06-24 15:37:14
tags:
---
在平时的工作之中，需要应用到垂直居中的场景较多。这里简单总结下使用css实现的三种方法，也是我比较常用的方案。

###### 第一种，简约而不简单的==行高==

- 单行文本


针对单行文本，处理起来比较简单，设定行高值为所需高度即可实现，举个栗子：
html：

```html
<div class="mid-text">
    单行文本固定高度内垂直居中
</div>
```

```css
.mid-text {
    width: 400px;
    margin: 0 auto;
    border: 1px solid #ddd;
    /* 以下为重点 */
    line-height: 200px;
    text-align: center;
}
```

效果图

![image](http://static.lvmin.me/o_1b6j4baej1bqa1gdc1l2a1j6nerr7.png)


**- 多行文本**
多行文本主要应用于未知文本长度的场景，这种需求可以通过行高搭配vertical-align属性来实现。

html

```html
<div class="mid-text">
    <div class="inner">
        这是第一行文本
        <br> 这是第二行文本
    </div>
</div>
```
css
```css
.mid-text {
    width: 400px;
    border: 1px solid #ddd;
    text-align: center;
    /* 以下为重点 */
    line-height: 200px;
    font-size: 0;
}
.inner {
    /* 以下为重点 */
    display: inline-block;
    vertical-align: middle;
    font-size: 14px;
    line-height: 1.4em;
}
```
效果图

![image](http://static.lvmin.me/o_1b6ksu1cru0krfm961vs2lq87.png)

这里有一个关键点需要注意一下，就是font-size:0这个属性值，这跟基线有点关联。对于vertical-align属性，摘录下w3c的定义：
> 该属性定义行内元素的基线相对于该元素所在行的基线的垂直对齐。允许指定负长度值和百分比值。这会使元素降低而不是升高。在表单元格中，这个属性会设置单元格框中的单元格内容的对齐方式。

在这里行高我设定的是300px,.inner相对于父元素的基线居中对齐，所以inner的位置会受到父元素基线位置的影响，故而在父元素中将font-size置零。

- 图片的居中控制

图片的居中处理需求出现的频次也是比较高的，同样使用行高搭配vertical-align属性也可以轻松实现。

html
```html
<div class="mid-img">
    <img src="http://static.lvmin.me/o_1b6j4ulb81k07mbv1uoo1p456ib7.jpg">
</div>
```
css

```css
.mid-img {
    width: 400px;
    border: 1px solid #ddd;
    text-align: center;
    /* 以下为重点 */
    line-height: 300px;
    font-size: 0;
}
.mid-img img {
    /* 以下为重点 */
    vertical-align: middle;
}
```
效果如下

![image](http://static.lvmin.me/o_1b6j6qhcarqk1lm31s0852u1jg97.png)

###### 第二种，黑魔法的==表格==
在过去的相当长时间内很多前端谈表格色变，由于曾经一段时期内，很多人滥用表格的很多布局特性去做页面的布局，这当然违背了表格的语义和原本设计功能。不可否认，表格确实带有很多神奇的特性，在某些情况下，我也会利用表格去实现一些功能，比如在这里我就是用它来实现垂直居中的需求。

html

```html
<div class="wrap">
    <div class="cell">
        这是一段测试文本这是一段测试文本这是一段测试文本这是一段测试文本
    </div>
</div>
```
css

```css
.wrap {
    width: 400px;
    /* 以下为重点 */
    display: table;
}
.cell {
    /* 以下为重点 */
    display: table-cell;
    height: 200px;
    border: 1px solid #ddd;
    vertical-align: middle;
}

```
效果图


![image](http://static.lvmin.me/o_1b6kujpej1iei6luvpnrah1nku7.png)

这种方式的优点是代码简单，而且可居中的元素也比较多，单行文本多行文本图片全都不在话下。

###### 第三种，absolute和padding
上面两种方案都是适用于内容区域高度不一定固定的场景，也是业务中最长遇见的场景，但是偶尔会遇到==内容区域尺寸已经固定==，继而需要垂直居中的业务情景，这种需求解决起来就比较简单了。这里简单罗列一下，就不详细描述了。
1. 上下设定等值padding。这个也是最常用的
2. 利用绝对定位。例如：

```
.inner {
    position: absolute;
    top: 50%;
    marigin-top: -height;
}
```


以上。

##测试
## 测试