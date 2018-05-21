[TOC]

## 1. SEO - 搜索引擎优化

搜索引擎优化 (SEO) 是提高一个网站在搜索引擎中的排名（能见度）的过程。如果网站能够在搜索引擎中有良好的排名，有助于网站获得更多的流量。

搜索引擎优化需要修改一个网站的HTML源代码和网站内容。搜索引擎优化策略应在网站建设之前就纳入网站的发展，尤其是网站的菜单和导航结构。

### 1.1 手动向搜索引擎提交网站

目前大多数搜索引擎提供了网站的提交路口，我们可以通过他们提供的入口提交站点，让搜索引擎能够及时抓取网站的数据。

- 360搜索引擎登录入口：<http://info.so.360.cn/site_submit.html>
- 百度搜索网站登录口：<http://www.baidu.com/search/url_submit.html>
- 百度单个网页提交入口：<http://zhanzhang.baidu.com/sitesubmit>
- Google网站登录口：<https://www.google.com/webmasters/tools/submit-url?hl=zh-CN>
- bing(必应)网页提交登录入口：<http://www.bing.com/toolbox/submit-site-url>
- 搜狗网站收录提交入口:<http://www.sogou.com/feedback/urlfeedback.php>
- SOSO搜搜网站收录提交入口:<http://www.soso.com/help/usb/urlsubmit.shtml>

通常情况下，您需要输入网站完整的URL，包括 http:// 前缀。

实例: [http://www.w3cschool.cc/](http://www.google.com/)

你只需要向搜索引擎提交你的站点首页即可，搜索引擎会根据你的站点页面关联的链接找到其他页面。

你还可以在网页中添加描述和关键字，但不要期望这些影响您的网站排名。

搜索引擎索引会定期更新。如果你的站点有修改或者页面已删除，搜索引擎会定期进行修改与清理。

并不是所有的链接都会出现在搜索引擎当中。

## 2. meta标签

Meta标签给搜索引擎提供了许多关于网页的信息。这些信息都是**隐含信息**,意味着对于网页自身的访问者是不可见的。

通常情况下，`<meta>` 标签会包含一个`name`属性，用来设置元数据。元数据的值放在`content`属性里面。你可以在`<meta>`标签中使用各种名称/值对，让我们来看看其中的一些。

### 2.1 name=”description”

description标签可能是最有用的标签之一。顾名思义，它会给搜索引擎提供关于这个网页的简短的描述。

```html
<meta name="description" content="网站介绍" />
```

这个标签曾经在搜索排名中占有很大的权重，但随着算法的不断的更新升级，它的地位也逐渐降低。它虽然不会提高网站排名，但是，因为它会被用在搜索引擎的结果页，所以依然有用。

当用户搜索的关键词与之相匹配时，会以粗体显示突出显示。这就是为什么一个好的页面说明 (利用关键字的) 可以显示更多与用户相关的信息，进而提高了点击率。推荐的`description`长度为`160` 个字符。

### 2.2 name=”keywords”

这个标签在过去很重要，但是现在却没什么价值了。现在没有一个主流的搜索引擎使用meta keywords来判断网页的内容了。

在meta keywords标签里面，你可以存储几个关于网页内容的关键字。然而，它却不会提高你的排名。如果你想要实现它(尽管我不知道你为什么这样做)你可以用如下代码：

```html
<meta name=”keywords” content=”meta tags,search engine optimization” />
```

### 2.3 name=”robots”:搜索引擎是否可以进入网页

Meta robots标签管理着搜索引擎是否可以进入网页，你可以用它来允许或不允许搜索引擎来获取你的网页、进入你网页中的子链接或对你的网页存档。例如：

```html
<!-- 禁止搜索引擎爬取 -->
<meta name=”robots” content=”noindex, nofollow” />
<!-- 允许搜索引擎爬取 -->
<meta name="robots" content="index,follow" /> 
```

## 3 title标签

在所有的HTML文档中，`title`标签都是不可缺少的。它定义了整个文档的标题，如下所示：

```html
<title>Title of the page</title>
```

标题通常会显示在两个不同的地方;浏览器的头部标签和搜索结果页。这就意味着title标签在点击率(CTR)和排名上有很重要的影响。

一个好的标题应该包含**关键字**，而且最好放在标题的开头部分。请记住，那些匹配到用户搜索的关键字会以粗体显示。

标题的长度要限制：谷歌会限制标题为**70个字符**，所以偶尔你可能需要书写一个合适的标题。

## 4. 推广人员去各大网站推广链接

微信朋友圈，微博、论坛等推广网站链接，让搜索引擎加快爬取。

## 参考资料



[Web 搜索引擎优化| 菜鸟教程](http://www.runoob.com/web/web-search.html)

[Meta 标签与搜索引擎优化](http://www.w3cplus.com/html5/meta-tags-and-seo.html)

