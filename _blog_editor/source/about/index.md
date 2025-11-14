---
robots: 'index,nofollow'
menu_id: social
title: 关于
h1: ''
leftbar: [sociallist, recent]
rightbar: [sociallist, recent, lalala]
comments: false
breadcrumb: false
header: true
indent: true
---



{% banner 黄先生 一名前端开发工程师 bg:/blog/assets/banner/nebula.jpg avatar:/blog/assets/images/avatar.jpg %}
{% endbanner %}

<br>

{% quot icon:hashtag About Me %}

未完待续。。。
123456

> 1232453

## blockquote 段落引用

{% tabs active:1  %}

<!-- tab 图片 -->
{% blockquote %}
这是使用 blockquote 标签的例子
{% endblockquote %}

<!-- tab 代码块 -->
```swift
{% blockquote %}
这是使用 blockquote 标签的例子
{% endblockquote %}
```
{% endtabs %}


## Tabs 分栏容器

{% tabs active:1  %}

<!-- tab 图片 -->
{% image /blog/assets/banner/books.jpg width:300px %}

<!-- tab 代码块 -->
```swift
let x = 123
print("hello world")
```

<!-- tab 表格 -->
| a | b | c |
| --- | --- | --- |
| a1 | b1 | c1 |
| a2 | b2 | c2 |

{% endtabs %}