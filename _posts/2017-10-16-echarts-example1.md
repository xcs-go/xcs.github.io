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
                trigger:'axis',  // 设置触发提示框组件的类型，有item(数据项图形触发，主要在散点图，饼图等无类目轴的图表中使用。)和axis(坐标轴触发，主要在柱状图，折线图等会使用类目轴的图表中使用。)
                formatter:function (params) {// 提示框浮层内容格式器
                    // return '折线图示例数据:' + params.data;
                    return '<div id="toolName" style="font-size:12px;"><span>折线图示例数据展示:</span><span style="font-size:14px;color:#000;">'+params.data+'</span></div>'
                },
                backgroundColor:'#f00',
                textStyle:{ // 设置提示框组件的文字的样式
                    color:'#fff'
                }
            }
        }
    {% endhighlight %}

- 以上是折线图的基本用法，下面我们来看看柱状图的基本用法：
  #### - 柱状图
    {% highlight javascript %}
       var xData = ['第一季度','第二季度','第三季度','第四季度'];
           var option = {
               title:{
                   text:'柱状图',
                   left:'left'
               },
               legend:{
                   data:['毛衣销售增长量','衬衫销售增长量']
               },
               tooltip:{}, // 不进行任何的配置，echarts会自动的读取数据中的内容进行显示
               xAxis:{
                   type:'category',
                   data:[]
               },
               yAxis:{
                   type:'value',
                   splitNumber:8,  // 设置y轴被分割为几段。在type设置为category时无效,该值只是一个预估值
                   min:0,
                   max:'dataMax', // 将y轴的最大值设置为dataMax;echarts会根据数据自动的计算出最大值
               },
               series:[
                   {
                       name:'毛衣销售增长量',
                       type:'bar',
                       areaStyle:{
                           normal:{
                               color:'#f00'
                           }
                       },
                       data:[10,39,20,70]
                   },
                   {
                       name:'衬衫销售增长量',
                       type:'bar',
                       areaStyle:{
                           normal:{
                               color:'#00f'
                           }
                       },
                       data:[40,15,50,70]
                   }
               ]
           };
       
           function setAxisData(data) {
              data.forEach(function(item,index){
                  option.xAxis.data.push(item);
              })
           }
           setAxisData(xData);
    {% endhighlight %}

- 以上是柱状图的基本用法，下面我们来看看饼图的基本用法：
  #### - 饼图
    {% highlight javascript %}
         var option = {
            title:{
                text:'2017年10月衣服销量',
                top:20,
                x:'center',
                //y:'middle',
                textStyle:{
                    // fontSize:20
                }
            },
            legend:{
                show:true,
                data:['毛衣','衬衫','短袖','T-shirt']
            },
            tooltip:{},
            series:{
                type:'pie',
                // roseType:'angle',
                data:[
                    {
                        name:'毛衣',value:35,
                        itemStyle:{
                            normal:{
                                color:'#00f'
                            }
                        },
                        labelLine:{   // 修改线的颜色
                            normal:{
                                show:true,
                                lineStyle:{
                                    color:'#0f0'
                                }
                            }
                        },
                        label:{   // 修改文字的颜色
                            normal:{
                                color:'#0f0'
                            }
                        }
                    },
                    {
                        name:'衬衫',value:15
                    },
                    {
                        name:'短袖',value:40
                    },
                    {
                        name:'T-shirt',
                        value:20
                    }
                    ]
                /*labelLine:{
                    normal:{
                        show:true  // 配置是否显示提示线,默认显示
                    }
                },
                label:{
                    normal:{
                        show:true // 配置是否显示扇形附近的标签文字,默认显示
                    }
                }*/
            }
         };
    {% endhighlight %}
    
- 以上是饼图的基本用法，下面我们来看看雷达图的基本用法：
  #### - 雷达图
    {% highlight javascript %}
       var option = {
          title: {
              text: '多雷达图'
          },
          tooltip: {
              trigger: 'axis'
          },
          legend: {
              x: 'center',
              data:['某软件','某主食手机','某水果手机','降水量','蒸发量']
          },
          radar: [ // 雷达图坐标组件
              {
                  indicator: [  // 设置雷达图指示器
                      {text: '品牌', max: 100},
                      {text: '内容', max: 100},
                      {text: '可用性', max: 100},
                      {text: '功能', max: 100}
                  ],
                  center: ['25%','40%'],
                  radius: 80
              },
              {
                  indicator: [
                      {text: '外观', max: 100},
                      {text: '拍照', max: 100},
                      {text: '系统', max: 100},
                      {text: '性能', max: 100},
                      {text: '屏幕', max: 100}
                  ],
                  radius: 80,
                  center: ['50%','60%'],
              },
              {
                  indicator: (function (){
                      var res = [];
                      for (var i = 1; i <= 12; i++) {
                          res.push({text:i+'月',max:100});
                      }
                      return res;
                  })(),
                  center: ['75%','40%'],
                  radius: 80
              }
          ],
          series: [
              {
                  type: 'radar',   // 雷达类型
                  tooltip: {
                      trigger: 'item'
                  },
                  itemStyle: {normal: {areaStyle: {type: 'default'}}},
                  data: [
                      {
                          value: [60,73,85,40],
                          name: '某软件'
                      }
                  ]
              },
              {
                  type: 'radar',
                  radarIndex: 1,  // 在多雷达图的时候需要配置该项
                  data: [
                      {
                          value: [85, 90, 90, 95, 95],
                          name: '某主食手机'
                      },
                      {
                          value: [95, 80, 95, 90, 93],
                          name: '某水果手机'
                      }
                  ]
              },
              {
                  type: 'radar',
                  radarIndex: 2,
                  itemStyle: {normal: {areaStyle: {type: 'default'}}},
                  data: [
                      {
                          name: '降水量',
                          value: [2.6, 5.9, 9.0, 26.4, 28.7, 70.7, 75.6, 82.2, 48.7, 18.8, 6.0, 2.3],
                      },
                      {
                          name:'蒸发量',
                          value:[2.0, 4.9, 7.0, 23.2, 25.6, 76.7, 35.6, 62.2, 32.6, 20.0, 6.4, 3.3]
                      }
                  ]
              }
          ]
      };

    {% endhighlight %}
    
- 将配置好的option作为参数传入setOption()方法中.
{% highlight javascript %}
echart.setOption(option);
{% endhighlight %}
