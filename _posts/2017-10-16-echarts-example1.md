---
layout: page
title: "echarts示例之常用图形绘制"
tags: [echarts]
date: 2017-10-09
excerpt: "echarts学习"
comments: true
category: echarts
---
### 绘制echarts图形的基本步骤
  创建的方法和上一篇中介绍到的方法一样，主要有以下几步:
  1. 调用echarts.init()方法将容器dom传入.
  2. 设置option配置项，配置需要展示的数据，样式等.
  3. 调用setOption()方法，将配置好的option传入即可.

### 根据以上的基本步骤绘制常用图

- 引入echarts.js文件
{% highlight html %}
<script src="https://cdnjs.cloudflare.com/ajax/libs/echarts/3.7.1/echarts.common.min.js"></script>
{% endhighlight %}
- 新建一个Dom容器，用来渲染Echarts图
{% highlight html %}
<div id='echart'></div>
{% endhighlight %}

#### - 折线图


#### - 柱状图


#### - 饼图


#### - 地理图


#### - 雷达图
