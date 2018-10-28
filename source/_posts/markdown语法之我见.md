---
title: Markdown语法之我见
date: 2018-10-05 23:39:05
tags: 
 - markdown语法
---
![](../../../../blogImg/20181005.jpg '雨后山水图')
## 前言
&nbsp;&nbsp;&nbsp;&nbsp;**markdown语法**简洁明了，易于掌握，所以用它来写作是件既效率又舒服的事情。我们所熟知的和一些大型CMS，如Joomla!、Drupal等都能很好的支持markdown语法。我是因为公司编写前端周报博文时开始接触到了markdown，此外GitHub、Gitlab项目库中的readme文件也存在着markdown语法，因此作为一个前端开发人员，需掌握基本的markdown语法。
&nbsp;&nbsp;&nbsp;&nbsp;markdown 是一种轻量级纯文本格式的标记语言，通过简单的标记语法，能将普通文本内容换成有效的并且具有一定格式的XHTML(或者HTML,PDF)文档，它的目标是实现易读易写，成为一种适用于网络的书写语言。
&nbsp;&nbsp;&nbsp;&nbsp;markdown 不是想要取代 HTML，甚至也没有要和它相近，它的语法种类很少，只对应 HTML 标记的一小部分 markdown 的构想不是要使得 HTML 文档更容易书写。在我看来， HTML 已经很容易写了。markdown 的理念是，能让文档更容易读、写和随意改。HTML 是一种发布的格式，markdown 是一种书写的格式。就这样，markdown 的格式语法只涵盖纯文本可以涵盖的范围。
<!--more-->
## markdown常用基本语法

### 1. 标题

#### 1.1 [h1~h6]
在想要设置为标题的文字前面加#来表示
一个#是一级标题，二个#是二级标题，以此类推。支持六级标题。
一般#作为文章大标题，只有一个，### 作为段落标题。
```
# ~ ######
```

#### 1.2 分级标题（上下文标题）
注：`= - `最少可以只写一个，兼容性一般
```
一级标题
======================
二级标题
---------------------
```


### 2. 字体

#### 2.1 加粗
要加粗的文字左右分别用两个*号包起来

#### 2.2 斜体
要倾斜的文字左右分别用一个*号包起来

#### 2.3 斜体加粗
要倾斜和加粗的文字左右分别用三个*号包起来

#### 2.4 删除线
要加删除线的文字左右分别用两个~~号包起来
```
**这是加粗的文字**
*这是倾斜的文字*`
***这是斜体加粗的文字***
~~这是加删除线的文字~~
```
示例：
**这是加粗的文字**
*这是倾斜的文字*
***这是斜体加粗的文字***
~~这是加删除线的文字~~


### 3. 代码

#### 3.1 单行代码：代码之间分别用一个反引号包起来
```
`代码内容`
```

#### 3.2 代码块：代码之间分别用三个反引号包起来，且两边的反引号单独占一行
```
(```)
  代码...
  代码...
  代码...
(```)
```
>注：为了防止转译，前后三个反引号处加了小括号，实际是没有的。这里只是用来演示，实际中去掉两边小括号即可。

#### 3.3 代码块缩进表示法
>tab 或四个空格

#### 3.4 语法高亮显示
```
(```)javascript
var num = 0;
for (var i = 0; i < 5; i++) {
    num+=i;
}
console.log(num);
(```)
```
演示:
```javascript
var num = 0;
for (var i = 0; i < 5; i++) {
    num+=i;
}
console.log(num);
```


### 4. 引用
#### 4.1 单行式
```
>hello Schnappi
```

#### 4.2 多行式
```
>hello Schnappi
hello Schnappi
hello Schnappi
或者
>hello Schnappi
>hello Schnappi
>hello Schnappi
```
演示:
>hello Schnappi
>hello Schnappi
>hello Schnappi

#### 4.3 多层嵌套
```
> aaaaaaaaa
>> bbbbbbbbb
>>> cccccccccc
```
演示:
> aaaaaaaaa
>> bbbbbbbbb
>>> cccccccccc


### 5. 链接
#### 5.1 内链式
注：`{:target="_blank"}`跳转方式兼容性一般 ，多数第三方平台不支持跳转
语法：
```
[超链接名](超链接地址 "超链接title")
title可加可不加
[简书](http://jianshu.com)
[百度](http://baidu.com "百度一下"){:target="_blank"}
```
示例：
[简书](http://jianshu.com)
[百度](http://baidu.com "百度一下")

#### 5.2 email邮件链接
><example@example.com>


### 6. 图片
#### 6.1 内链式
```
![](../../../../blogImg/20181005.jpg '雨后山水图')
```

#### 6.2 插入图片带有链接
```
[![](./01.png '百度')](http://www.baidu.com){:target="_blank"}        // 内链式

[![](./01.png '百度')][5]{:target="_blank"}                       // 引用式支持度不高，一般不这么用。
[5]: http://www.baidu.com
```
示例：
[![](../../../../blogImg/20181005.jpg '雨后山水图')](https://www.bilibili.com/video/av32043189?from=search&seid=6491458486993806776)


### 7. 视频插入
>注：Markdown 语法是不支持直接插入视频的,普遍的做法是插入HTML的 iframe 框架，通过网站自带的分享功能获取，如果没有可以尝试第二种方法,就是是伪造播放界面，实质是插入视频图片，然后通过点击跳转到相关页面。

代码1：
多数第三方平台不支持插入`<iframe>视频`
```
<iframe height=80% width=100% src='https://www.bilibili.com/video/av32043189?from=search&seid=6491458486993806776' frameborder=0 'allowfullscreen'></iframe>
```
演示：
<iframe height=450 width=100% src='https://www.bilibili.com/video/av32043189?from=search&seid=6491458486993806776' frameborder=0 'allowfullscreen'></iframe>
代码2：
```
[![](../../../../blogImg/20181005.jpg '雨后山水图')](https://www.bilibili.com/video/av32043189?from=search&seid=6491458486993806776){:target="_blank"}
```

### 8. 序表
#### 8.1 有序
注：序列`.`后保持空格
```
1. one
2. two
3. three
```
演示：
1. one
2. two
3. three

#### 8.2 无序
```
* one
* two
* three
```
演示：
* one
* two
* three

#### 8.3 序表嵌套
```
1. one
    1. one-1
    2. two-2
2. two 
    * two-1
    * two-2
```
演示：
1. one
    1. one-1
    2. two-2
2. two 
    * two-1
    * two-2