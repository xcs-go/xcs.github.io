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

- 调用echarts.init()方法
    {% highlight javascript %}
    var dom = document.getElementById('echart');
    var echart = echarts.init(dom);
    {% endhighlight %}

- 配置option,根据不同的图表类型进行不同的配置
  #### - 折线图
    {% highlight javascript %}
        var option = {
            title:{  // 设置图形标题
                text:'echarts基础图之折线图',
                left:'center', // 设置标题在水平方向上的位置
                top:'20', // 设置标题在垂直方向上的位置
                textStyle:{  // 设置标题文字的样式
                    color:'#f00'
                }
            }
            series:{
                type:'line', // series.type用来设置系列图的类型；line表示的是折线图
            }
        }
    {% endhighlight %}

  #### - 柱状图
    {% highlight javascript %}
        var option = {
            
        }
    {% endhighlight %}

  #### - 饼图
    {% highlight javascript %}
         var option = {
                
         }
    {% endhighlight %}
    
  #### - 地理图
    {% highlight javascript %}
        var option = {
            
        }
    {% endhighlight %}

  #### - 雷达图
    {% highlight javascript %}
        var option = {
            
        }
    {% endhighlight %}
    
- 将配置好的option作为参数传入setOption()方法中.
{% highlight javascript %}
echart.setOption(option);
{% endhighlight %}
