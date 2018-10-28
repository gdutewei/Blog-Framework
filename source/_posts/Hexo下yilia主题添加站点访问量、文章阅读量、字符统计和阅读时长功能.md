---
title: Hexo下yilia主题添加站点访问量、文章阅读量、字符统计和阅读时长功能
date: 2018-10-06 14:34:13
tags: 
 - hexo 
 - yilia
---

![](../../../../blogImg/20181006.jpg)

## 前言
&nbsp;&nbsp;&nbsp;&nbsp;想必很多小伙伴在搭建了自己的博客站点，并且发布自己写的一篇博客之后，都想了解一下博客站点的访客量、文章的阅读量、文章的字数以及阅读时长等，下面就让我们开始这段神奇之旅，为我们的博客站点添加以上功能吧。
<!-- more -->

## 引入不蒜子
>注意：不蒜子有两种统计算法

1.pv的方式，单个用户连续点击n篇文章，记录n次访问量
```html
    <span id="busuanzi_container_site_pv">
        总访问量<span id="busuanzi_value_site_pv"></span>次
    </span>
```
2.uv的方式，单个用户连续点击n篇文章，只记录1次访客数
```html
    <span id="busuanzi_container_site_uv">
        总访客<span id="busuanzi_value_site_uv"></span>人次
    </span>
```

## 添加是否开启统计功能的配置
找到yilia主题的配置文件`themes/yilia/_config.yml`，添加`footer`字段，加入一个配置，这里我们暂且命名为`counter`，即
```yml
# footer的设置
footer:
  # visitors count
  counter: true
```

## 修改yilia主题的模板文件
由于是把访问量统计放在网页的footer，所以我们需要修改的模板文件是`theme/yilia/layout/_partials/footer.ejs`。我们在合适的位置加入：
```html
<footer id="footer">
  <div class="outer">
    <div id="footer-info">
    	<div class="footer-left">
    		&copy; <%= date(new Date(), 'YYYY') %> <%= config.author || config.title %>
			</div>
      	<div class="footer-right">
      		<a href="http://hexo.io/" target="_blank">Hexo</a>  Theme <a href="https://github.com/litten/hexo-theme-yilia" target="_blank">Yilia</a> by Litten
      	</div>
    </div>
	</div>
	<!-- 添加代码 -->
	<% if (theme.footer.counter) {%>
        <script async src="//dn-lbstatics.qbox.me/busuanzi/2.3/busuanzi.pure.mini.js"></script>
        <span id="busuanzi_container_site_pv">总访问量<span id="busuanzi_value_site_pv"></span>次</span>
        <span class="post-meta-divider">|</span>
        <span id="busuanzi_container_site_uv">总访客<span id="busuanzi_value_site_uv"></span>人次</span>
	<% } %>
	<!-- 添加代码结束 -->
</footer>
```

## 添加文章访问量
文章的访问量显示在文章里面，所以在`article.ejs`里加上文章访问量的标签:
>注意：这里需要判断首页时不显示文章阅读量，否则会出现统计错误。

```html
<div class="article-info article-info-index">
      <%if(post.top){%>
        <div class="article-pop-out tagcloud">
          <i class="icon-tuding"></i>
          <a class="article-tag-list-link color3">置顶</a>
        </div>
      <% } %>
      <%- partial('post/tag') %>

      <!-- 添加代码开始 -->
      <% if (!index){ %>
        <span id="busuanzi_container_page_pv" style="color: #999">
          |&nbsp;阅读量(<span id="busuanzi_value_page_pv"></span>)
        </span>
      <% } %>
      <!-- 结束 -->
      
      <%- partial('post/category') %>
      <% if (index && theme.show_all_link){ %>
        <p class="article-more-link">
          <a class="article-more-a" href="<%- url_for(post.path) %>"><%= theme.show_all_link %> >></a>
        </p>
      <% } %>

      <% if (!index && theme.share_jia){ %>
        <%- partial('post/share') %>
      <% } %>
      <div class="clearfix"></div>
    </div>
```

## 添加字数统计和阅读时长功能
1.安装 hexo-wordcount ：在博客目录下打开Git Bash Here 输入以下命令：
```
yarn add hexo-wordcount --save
```
2.文件配置：在`theme\yilia\layout\_partial\post`下创建`word.ejs`文件：
```html
<div style="margin-top:10px; color: #999">
    <span>
      <span>
        <span>  字数统计: </span>
        <span><%= wordcount(post.content) %>字</span>
      </span>
    </span>
    <span>
      &nbsp; | &nbsp;
      <span>
        <span>  阅读时长: </span>
        <span><%= min2read(post.content) %>分</span>
      </span>
    </span>
</div>
```
然后在`themes/yilia/layout/_partial/article.ejs`中添加:
```html
<header class="article-header">
        <%- partial('post/title', {class_name: 'article-title'}) %>
        <% if (!post.noDate){ %>
            <%- partial('post/date', {class_name: 'archive-article-date', date_format: null}) %>
            <!-- 需要添加的位置 -->
            <!-- 开始添加字数统计-->
            <% if(theme.word_count && !post.no_word_count){%>
            <%- partial('post/word') %>
            <% } %>
            <!-- 添加完成 -->
        <% } %>
      </header>
```
3.开启功能：在站点的`_config.yml`中添加下面代码：
```yml
# 是否开启字数统计
#不需要使用，直接设置值为false，或注释掉
word_count: true
```
效果预览：https://gdutewei.github.io