---
layout: page
title: "Generator"
tags: [es6]
date: 2017-10-09
excerpt: "Generator学习"
comments: true
category: ES6
---
### Generator基本理解
1. Generator函数是ES6提供的一种异步编程解决方案。
2. Generator函数是一个状态机，内部封装了多个内部状态。
3. 执行Generator函数会返回一个遍历器对象,返回的遍历器对象，可以依次遍历Generator函数内部的每一个状态。

### Generator函数与普通的函数的区别
1. Generator函数的function关键字与函数名之间有一个星号(*)号。
2. Generator函数内部使用了yield表达式,定义Generator函数内部的不同状态。
{% highlight javascript %}
    function* helloWorldGenerator(){
        yield 'hello';
        yield 'world';
        return 'ending';
    }
    var hw = helloWorldGenerator();
{% endhighlight %}
