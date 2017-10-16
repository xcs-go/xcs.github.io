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
            },
            xAxis:{
                min:0, // 设置x轴的最小值
                max:100, // 设置x轴的最大值
                name:'x',
                splitLine:{ // 设置x轴的网格
                    show:false // 默认显示
                }
            },
            yAxis:{
                min:0,
                max:120,
                name:'y',
                nameTextStyle:{ // 设置坐标轴文字的样式
                    color:'#f00'
                },
                splitNumber:12  // 设置坐标轴被分割成几段，只是一个预估值，实际上是会根据数据做一些调整.
                //nameGap:15 设置坐标轴文字与坐标轴之间的距离，默认是15
            },
            series:{  // 系列列表；图表所展示的数据，样式，线条等，在这里进行设置
                type:'line', // series.type用来设置系列图的类型；line表示的是折线图
                smooth:true, // 设置折线是否是平滑的，true表示平滑展示，false表示非平滑展示。默认为false.
                data:[
                       [0,0],
                       [15,10],
                       [40,29],
                       [30,50],
                       [60,80],
                       [80,90],
                       [100,20]
                     ],
                areaStyle:{  // 设置数据区域的样式
                      normal:{
                          color:'#ff0',
                          opacity:.8
                      }
                  },
                  lineStyle:{ // 设置线条的样式,包括线条类型，透明度，颜色等
                      normal:{
                          type:'dashaed',
                          opacity:.6,
                          color:'#0d0'
                      }
                  },
                  itemStyle:{ // 设置折线拐点的样式
                      normal:{
                          color:'#00f'
                      }
                  }
            },
            tooltip:{ // 提示框组件
                //trigger:'axis'
                formatter:function (params) {// 提示框浮层内容格式器
                    // return '折线图示例数据:' + params.data;
                    return '<div id="toolName" style="font-size:12px;"><span>折线图示例数据展示:</span><span style="font-size:14px;color:#000;">'+params.data+'</span></div>'
                },
                backgroundColor:'#f00',
                textStyle:{
                    color:'#fff'
                }
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