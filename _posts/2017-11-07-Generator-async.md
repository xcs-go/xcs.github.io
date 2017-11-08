---
layout: page
title: "Generator函数的异步调用"
tags: [es6]
date: 2017-11-07
excerpt: "Generator函数异步调用学习"
comments: true
category: ES6
---
### 传统的异步编程实现方式：
- 回调函数
- 事件监听
- 发布／订阅
- Promise对象

### ES6中通过Generator函数实现了异步编程
#### 协程的Generator函数实现
Generator函数就是一个封装的异步任务，异步操作需要暂停的地方，都用yield语句注明。
{% highlight javascript %}
    function* gen(x){
        let y = yield (x + 1);
        return y;
    }
    let g = gen(1);
    g.next();  // {value:3,done:false}
    g.next(); //  {value:undefined,done:true}
{% endhighlight %}

### Generator函数的数据交换及其错误处理
Generator函数能封装异步任务的主要原因有以下两个
- 能暂停执行(yield)
- 能恢复执行(next)

next返回的value，是generator函数向外输出数据，next方法还可以接收参数，向generator函数体内传递数据.
{% highlight javascript %}
    function* gen(x){
            let y = yield (x + 1);
            return y;
        }
        let g = gen(1);
        g.next(); // {value:3,done:false}
        g.next(1); // {value:1,done:true}
{% endhighlight %}

generator函数内部还可以捕捉到该函数外部抛出的错误
{% highlight javascript %}
    function* gen(x){
        try{
            let y = x + 2; 
        }catch(e){
            console.log(e);  // 出错了
        }
    }
    let g = gen(1);
    g.next(); // {value:3,done:false}
    g.throw('出错了');
{% endhighlight %}

### Thunk函数
Thunk函数是自动执行Generator函数的一种方式
#### Thunk函数的含义
编译器的'传名调用'实现，一般情况下是将参数放到一个临时函数中，再将这个临时函数传入函数体。这个临时函数就叫做Thunk函数。
{% highlight javascript %}
    function m(x){
        return x + 2;
    }
    m(y + 1);
    // 等同于以下的代码
    let thunk = function(){
        return y + 1;
    }
    function m(thunk){
        return thunk() + 2;
    }
{% endhighlight %}
### javascript语言中的Thunk函数
javascript是传值调用,它的Thunk函数含义和以上说的Thunk函数是有区别的。在JS中，Thunk函数替换的不是表达式，而是多参数函数，
将其替换成一个只接受回调函数作为参数的单参数函数。
{% highlight javascript %}
    // 正常版本的readFile
    fs.readFile(filename,callback);
    //Thunk版本的readFile
    let Thunk = function(filename){
        return function(callback){
            return fs.readFile(filename,callback);
        }
    }
    let readFileThunk = Thunk(filename);
    readFileThunk(callback);   // Thunk函数
{% endhighlight %}
所有的函数，只要参数有回调函数，就能写成Thunk函数的形式。
{% highlight javascript %}
    // ES5版本
    var Thunk = function(fn){
        return function(){
            var args = Array.prototype.slice.call(argument);
            return function(callback){
                return fn.apply(this,args);
            }
        }
    }
    // ES6版本
    const Thunk = function(fn){
        return function(...args){
            return function(callback){
                return fn.call(this,...args,callback);
            }
        }
    }
{% endhighlight %}
根据上面的转换器，生成如下的读区文件的Thunk函数
{% highlight javascript %}
    const readFileThunk = function(fs.readFile);
    readFileThunk(filename)(callback);  // Thunk函数
{% endhighlight %}

### Thunkify模块
Thunkify模块是生产环境的转换器,使用方式如下:
{% highlight javascript %}
    const thunkify = require('thunkify');
    const fs = require('fs');
    const read = thunkify(fs.readFile);
    read('hello.txt')(callback);
{% endhighlight %}

### Generator函数的流程管理
使用Thunk函数可以用来做Generator函数的流程管理。具体还需要继续理解... 

### co模块
co模块是用来Generator函数的自动执行的。
{% highlight javascript %}
    const gen = function* (){
        let x = yield readFile('afile');
        let y = yield readFile('bfile');
        console.log(x.toString());
        console.log(y.toString());
    }
{% endhighlight %}
co模块可以让开发者不要写Generator函数的执行器，只需要将Generator函数作为参数传入co模块中,就会自动执行。
{% highlight javascript %}
    const co = require('co');
    co(gen);
{% endhighlight %}
co函数返回的是一个promise对象，所以可以使用then方法继续执行。
