---
title: How to write an Hexo Blog
date: 2018-10-05 22:28:14
tags: 
 - hexo
 - blog
---

![](../../../../blogImg/20181004.jpg)
## 前言
使用hexo+yilia方式搭建GitHub Pages个人博客，记录使用markdown语法编辑自己第一篇博客。
<!--more-->
## 开始学习
`hexo`使用`markdown`语法的纯文本编辑，使用默认**post布局**方式新建的**文件后缀名.md**文件存放在**我们的站点目录下/source/_post文件夹**下。

## 文件生成方式：
`hexo new layout 文件名`，例如：`hexo new post HelloWorld`
如果文件名中有空格则必须给文件名加引号`hexo new post 'Hello World'`
`layout`是可选的，默认为`post`,**layout**有哪些呢，我们可以到我们的站点目录下的`scaffolds`文件夹下查看也可以编辑现有的Layout文件。

## post模板:
```
---
title: How to write an hexo blog
date: 2018-10-05 22:28:14
tags: -
---
```

1.有的时候我们想给自己写的blog分类就可以对post文件进行修改，修改后我们以后再写文章就不用再次添加了
注意：`分号之后必须留空格！！！`
```
---
title: How to write an hexo blog
date: 2018-10-05 22:28:14
categories: -
tags: -
---
```

2.接下来我们可以使用 `markdown编辑器`来编辑我们的博客文章了，我们可以直接在`Visual Studio Code`里面找到/source/_post/下面新生成的博客.md文件双击默认打开。

3.博客编辑完成之后在shell终端执行部署命令：
```
hexo clean
hexo g
hexo d
```