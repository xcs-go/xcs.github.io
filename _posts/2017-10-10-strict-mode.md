---
layout: page
title: "javascript严格模式"
tags: [javascript,strict]
date: 2017-10-10
excerpt: "javascript严格模式"
comments: true
category: javascript
---

## 严格模式
  ES5引入了严格模式的概念。在严格模式下，会对某些不安全的操作抛出错误。
  
## 全局严格模式
  要在整个js文件中启用严格模式，只需要在js文件的最顶部添加下面一行代码即可:
  {% highlight javascript %}
    "use strict";
  {% endhighlight %}

## 局部严格模式
  如果在函数内部最顶部添加了'use strict';则在该函数内部启用了严格模式
  {% highlight javascript %}
  function useStrict(){
    "use strict";
    // do something 
  }
  {% endhighlight %}  

## 严格模式对编写代码的影响
  常见的影响有以下几个:
 
  - 在严格模式下，变量的声明必须使用var开始，不能省略，在正常模式下，可以省略，省略即为全局变量。
  {% highlight javascript %}
  
  // 严格模式下
  "use strict"
  a = 10; // 报错:Uncaught ReferenceError: a is not defined
  console.log(a);
  
  // 正常模式下
  a = 10;
  console.log(a); //  10
  {% endhighlight %}
