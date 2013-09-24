---
layout: post
title: "定制Octopress"
date: 2013-09-22 14:12
comments: true
categories: tech
---

## 引子 ##

今天重新设置了一下我的Blog，主要是参考其他Octopress以及官方文档，现在看起来还是比较漂亮。其实自从高考之后，几乎就没写过什么文章，但是最近看了很多Blog以及微信公众帐号的文章，感觉作为一枚程序员，语言表达能力对于职业生涯是至关重要的，比如说招聘时都可能让你填写Blog地址。所以呢，可能的话，还是多读一读、写一写。所以呢，今天就把我的Configure记录下来。

<!-- more -->

## 安装主题 ##

自带的主题其实还是不错的，但是太大众化了，太是需要有点个性。

我使用主题的是「[whitelake](https://github.com/gehaxelt/CSS-WhiteLake)」。

安装的过程也很简单：

```
$ cd octopress
$ git clone https://github.com/gehaxelt/CSS-WhiteLake.git .themes/whitelake
$ rake install['whitelake']
$ rake generate
```

之后的话，执行`rake deploy`部署一下就可以了。

更多第三方插件和主题等资源的话，参见[wiki](https://github.com/imathis/octopress/wiki)。

## 添加评论和分享功能 ##

这里的话其实我是直接使用octopress内置的disqus评论功能以及twtter和facebook的分享功能的，这在国内可能比较稀缺，但是这设置起来简单多了，二者这些都比国内的复制品好多了。

设置的应该不用说明，有帐号的话，直接在`_config.yml`添加并打开就可以了。

## 让博客中的链接在新窗口打开 ##

其实很简单，在`a`标签里面添加`target="_black"`属性就可以实现。但是Markdown本身不支持，我们又不可能去修改HTML文件。

可以参考：「[在Octopress中为markdown的超链接加上target="_blank"](http://www.blogjava.net/lishunli/archive/2013/01/20/394478.html)」。只需要在`/source/_includes/custom/head.html`文件末尾添加如下脚本即可:
``` javascript
<script type="text/javascript">

function addBlankTargetForLinks () {
  $('a[href^="http"]').each(function(){
      $(this).attr('target', '_blank');
  });
}

$(document).bind('DOMNodeInserted', function(event) {
  addBlankTargetForLinks();
});

</script>

```

## 404 公益页面 ##

在`/source`目录下添加`404.markdown`即可。本博客使用的是腾讯的公益404，推荐大家使用，为社会贡献一份力量。

```

---

layout: page

title: "404 Error"

date: 2013-4-21 02:35

comments: false

sharing: false

footer: false

---

<script type="text/javascript" src="http://www.qq.com/404/search_children.js" charset="utf-8"></script>

```

## 在博文末尾添加原文链接、版权 ##

详情参见博客：「[为octopress每篇文章添加一个文章信息](http://codemacro.com/2012/07/26/post-footer-plugin-for-octopress/)」。

文中没有提及的是，为了做好美化，还需要增加一段针这块区域的css：

编辑`sass/custom/_style.scss`，在末尾增加如下内容： 

``` css
.post-footer{margin-top:10px;padding:5px;background:none repeat scroll 0pt 0pt #eee;font-size:90%;color:gray}
```

这样，原文链接和版权信息就能很好的和正文内容分离开了。

## 给中英文之间加空格 ##

参见博文：「[给中英文间加个空格](http://xoyo.name/2012/04/auto-spacing-for-octopress/)」。

注意ruby文件的编码：复制博文中的代码时，需要去掉前面注释，让`#encoding:UTF-8`语句暴露在.rb文件的第一句。否则，`rake generate`时，会报错无法识别`\p{Han}`。

##Tips

既然是个博客站点，就算是web产品啦，可以考虑下SEO。推荐博文：「[《Octopress中的SEO》](http://codemacro.com/2012/09/06/octopress-seo/)」。
