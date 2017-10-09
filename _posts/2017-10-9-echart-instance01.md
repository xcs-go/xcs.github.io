---
layout: page
title: "echarts示例"
tags: [echarts]
date: 2017-10-09
excerpt: "echarts学习"
comments: true
category: echarts
---
## 创建第一个echarts示例
  阅读该文章之前请先了解官网的基础知识或者请先看以下这篇文章<<echarts基础知识整理>><https://xcs-go.github.io/xcs.github.io//echarts-basic/>

  第一个echarts示例是新建一个柱状图；新建一个html文件，引入echarts文件，并且新建一个div容器
  {% highlight html %}
  <!--引入echarts文件-->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/echarts/3.7.1/echarts.common.min.js"></script>
  <div id = 'echarts'></div>
  {% endhighlight %}
  
  在js中，做如下设置:
  {% highlight javascript %}
  var echartsDOM = document.getElementById('echarts');
  var myEchart = echarts.init(echartsDOM);
  {% endhighlight %}
  在调用了echarts.init()方法之后，我们就需要对图表进行有关的配置。
  首先，我们先设置一个x,y轴
  {% highlight javascript %}
  var option = {
    // 配置x,y轴
    xAxis:{
        data:['apple','huawei','vivo','oppo','vivo']
    },
    yAxis:{},// 如果不设置，echarts就会根据数据进行自动计算
  }
  {% endhighlight %}
