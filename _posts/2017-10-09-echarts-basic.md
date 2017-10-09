---
layout: page
title: "echarts基础知识整理"
tags: [echarts]
date: 2017-10-09
excerpt: "echarts学习"
comments: true
category: echarts
---
## 什么是echarts?
ECharts，一个纯 Javascript 的图表库,可以同时运行在pc和移动端。兼容了目前市场上的主流浏览器。
其底层依赖轻量级的 Canvas 类库 ZRender。

## echarts的特点：
- echarts提供了丰富的图表类型，比如我们常见的柱状图，折线图，饼图，k线图等。  
- echarts提供了多坐标系的支持，如直角坐标系，极坐标系，地理坐标系
- 移动端优化：减少了图标库的体积，加载速度更快。
- 交互式数据：如 legend visualMap dataZoom tooltip等。例如设置了legend可以通过点击legend，实现有关的数据是否显示；设置visualMap可以实现拖拽显示与之对应的数据。
- 处理大批量的数据
- 多维度展示数据
- 动态数据展现
- 丰富的特效

更多信息请参考官网: <http://echarts.baidu.com/feature.html> 

## 在项目中使用
- 根据项目的需求选择相应的文件下载，详细信息参考官网: <http://echarts.baidu.com/download.html>
- 引入echarts文件
    > 引入echarts文件有以下几种方法：
    {% highlight html %}
    <!-- 引入下载的ECharts 文件 -->
    1. <script src="echarts.min.js"></script>
    2. <!-- 通过cdn引入ECharts文件 -->
       <script src="https://cdnjs.cloudflare.com/ajax/libs/echarts/3.7.1/echarts.common.min.js"></script>
    3. <!-- 在webpack中使用 -->
        在终端执行以下代码:
          npm install echarts --save
        在项目中通过require引入Echarts。
          var echart = require('echarts');
    {% endhighlight %} 
       
- 定义一个具有一定高度和宽度的DOM容器。用来展示ECharts渲染完成后的图表。
   {% highlight html %}
      <!-- 需要在样式表中设定宽高 -->
      <div id="echarts"></div>
   {% endhighlight %}
- 在js中，通过调用echarts.init()方法，并且将用于展示echarts图表的容器作为参数传入。
    {% highlight javascript %}
    var echartsDOM = document.getElementById('echarts');
    var myEcharts = echarts.init(echartsDOM);
    {% endhighlight javascript %}
- 调用实例的setOption()方法进行有关配置
    {% highlight javascript %}
    var option = {进行有关的配置};
    myEcharts.setOption(option);   
    {% endhighlight %}
