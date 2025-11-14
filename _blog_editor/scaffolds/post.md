---
# 基本信息
title: {{ title }} # 文章标题
date: {{ date }} # 文件建立日期
tags: [] # 文章标签
categories: [] # 文章分类 [设计开发, iOS开发] 这样写就只会显示「设计开发」一级分类，而在文章页面顶部则会显示完整的面包屑导航。
description: # excerpt 也可 纯文本的页面摘要。
# 封面
cover: # 文章封面；在文章列表页面或者其他位置显示的文章摘要卡片上面的图片称之为「文章封面」
banner: # 横幅图片 直接对应链接即可 https://xxxx.jpg
poster: # 海报（可选，全图封面卡片）
  topic: 标题上方的小字 # 可选
  headline: 大标题 # 必选
  caption: 标题下方的小字 # 可选
  color: 标题颜色 # 可选 默认为跟随主题的动态颜色 # white,red...
# 插件
# sticky: # 数字越大越靠前
mermaid:
katex: 
mathjax: 
# 可选
topic: 专栏 id
author: Humphrey
references: 参考文献；格式： - '[xxxx文档](https://www.abc.com/...)'
# comments: 设置 false 禁止评论
# indexing: 设置 false 避免被搜索
breadcrumb: 设置 false 隐藏面包屑导航
leftbar: [左侧菜单]
rightbar:
h1: 设置为 '' 隐藏标题
type: tech # 文章类型 tech: 默认技术类文章, story: 图文类文章
open_graph:
  # 覆盖 OpenGraph
  # 如果分享到社交平台的缩略图不理想，可以通过这个特性覆盖为自己想要的：
  image: 
---