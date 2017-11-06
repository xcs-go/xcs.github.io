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
3. Generator函数是分段执行的。
{% highlight javascript %}
    function* helloWorldGenerator(){
        yield 'hello';
        yield 'world';
        return 'ending';
    }
    var hw = helloWorldGenerator();
{% endhighlight %}

### 理解Generator函数的遍历器对象
    调用Generator函数之后，该函数并不会执行，也不会将结构返回，而是指向内部状态的指针对象(也就是调用Generator函数生成的遍历器对象),
    所以，如果希望Generator函数有返回结果，那么就必须调用遍历器对象的next()方法，让指向内部状态的指针进行移动（移向下一个状态）,每次移动遇到yield表达式或者return就会停下来。
具有如下特点:

- 调用next方法，指向遍历器对象的指针就开始从函数头部或者上一次停下来的地方开始执行。
- 指针移动时遇到yield或return表达式就会停止下来。
- yield是暂停的标志，next方法可以将已经暂停的恢复执行.

### 调用next方法返回的对象
{% highlight javascript %}
    hw.next();  // {value:'hello',done:false}
    hw.next();  // {value:'world',done:false}
    hw.next();  // {value:'ending',done:true}
    hw.next();  // {value:undefined,done:true}
{% endhighlight %}

    根据以上的调用我们知道，每次调用next()方法，都会返回一个value,done作为key的对象.
    value属性表示的是当前的内部状态的值，是yield表达式后面的表达式的值,done表示的是遍历是否已经结束，
    当遇到return或者函数运行完成没有值的时候(undefined)，done的值会变为true，表示遍历已经结束了，否则为false
    表示遍历没有结束.
    
### next()传参
    yield自身并没有返回值(undifined);其提供了generator函数暂停执行的功能并将yield后面的表达式的结果作为返回对象的value值。
    在调用next()方法的时候，可以给该方法传递一个参数，传递给该方法的参数将会作为上一个yield表达式的返回值。
    {% highlight javascript %}
    function* math (x){
        let y = 2 * (yield x + 2);
        let z = yield (y/3);
        return x + y + z;
    }
    const m = math(4);
    m.next();   // {value:6,done:false}
    m.next(12); // {value:8,done:false}
    m.next(10); // {value:38,done:true}
    {% endhighlight %}
    如果想要在第一次调用next()的时候就传递参数的话，可以在generator函数内部再封装一层.
    {% highlight javascript %}
    function wrapper(generatorFunction){
        return function(..args){
            let generatorObject = generatorFunction(...args);
            generatorObject.next();
            return generatorObject;
        }
    }
    const wrapped = wrapper(function* (){
        console.log(`first input:${yield}`);
        return 'Done';
    });
    wrapped().next('hello');
    {% endhighlight %}
    
### for...of循环
for...of循环能够自动的遍历Generator函数时生成的Itenerator对象，并且此时不需要再调用next(）方法。
{% highlight javascript %}
    function* foo(){
        yield 1;
        yield 2;
        yield 3;
        yield 4;
        yield 5;
        return 6;
    }
    for (let v of foo()){
        console.log(v); // 1,2,3,4,5,6
    }
{% endhighlight %}
⚠️:一旦next方法的返回对象的done属性变成了true,那么for..of循环就会结束，并且不会将done变成true的value属性给遍历出来（不包含该value值）。
使用for...of循环可以遍历任何具有Itenerator接口的对象,⚠️原生的javascript对象没有Itenerator接口，所以for...of不能对原生的javascript对象进行遍历,如果想要对
原生的javascript对象进行遍历的话，可以通过Generator函数给原生的对象加上Itenerator接口。
{% highlight javascript %}
    function* objectEntries(obj){
        let propKeys = Reflect.ownKeys(obj);
        for (let prop of propKeys){
            yield [prop,obj[prop]];
        }
    }
    const jane = {first:'Jane',last:'doe'};
    for(let [key,value] of objectEntries(jane)){
        console.log(`${key}:${value}`); // first:'Jane';last:'doe'
    }
{% endhighlight %}
另外一种给原生对象添加Itenerator接口的方法是添加到对象的Symbol.iterator属性上。

除了for...of以外，扩展运算符(...),解构赋值和Array.from方法内部都是调用了遍历器接口。
{% highlight javascript %}
    function* nums(){
        yield 1;
        yield 2;
        return 3;
        yield 4;
    }
    // 扩展运算符
    [...nums()] // [1,2]
    // 结构赋值
    let [x,y] = nums(); // x 1,y 2
    // Array,from(nums()); // [1,2]
{% endhighlight %}
    
    

