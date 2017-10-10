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
  "use strict";
  a = 10; // 报错:Uncaught ReferenceError: a is not defined
  console.log(a);
  
  // 正常模式下
  a = 10;
  console.log(a); //  10
  {% endhighlight %}
  
  - 在严格模式下，不能定义名为eval或arguments的变量，否则会导致语法错误
  {% highlight javascript %}
  // 严格模式
  "use strict";
  var eval = 5; // 报错：Uncaught SyntaxError: Unexpected eval or arguments in strict mode
  
  // 正常模式
  var eval = 5;
  console.log(eval);  // 5
  {% endhighlight %}
  
  - 在严格模式下，不能使用with语句
  {% highlight javascript %}
  "use strict";
  var a = 10;
  with(a){
    a = 20; // 报错：Uncaught SyntaxError: Strict mode code may not include a with statement
  }
  {% endhighlight %}
  
  - 在严格模式下，使用eval可以创建第三种作用域
  {% highlight javascript %}
  "use strict";
  var a = 10;
  console.log(eval("var a = 20;a")); // 20
  console.log(a); // 10
  {% endhighlight %}
  
  - 禁止this指向全局对象window
  {% highlight javascript %}
  function fn(){
    return !this;  // false => 此时this指向的是window对象
  }
  
  function fn1(){
    "use strict";
    return !this;  // true => 此时this为undefined,所以取反为true.
  }
  {% endhighlight %}
  
  所以在构造函数中,如果在创建对象的实例的时候，忘记了new关键字，那么在严格模式下就会报错
  {% highlight javascript %}
  function F(){
    "use strict";
    this.a = 1;
  }
  var aa = F(); // 报错:Uncaught TypeError: Cannot set property 'a' of undefined
  {% endhighlight %}
  
  - 在严格模式下，函数的arguments属性和caller属性不能使用
  {% highlight javascript %}
  function f1(){
  　"use strict";
  　f1.caller; // 报错
  　f1.arguments; // 报错
  }
  f1();
  {% endhighlight %}
