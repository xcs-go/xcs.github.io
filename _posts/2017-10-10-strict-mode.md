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
