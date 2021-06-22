# Js常见面试题


# Js常见面试题

1. 什么是闭包？闭包的用途是什么？闭包的缺点是什么？

   * 闭包

     如果一个函数用到了外部的变量，那么这个函数加这个变量就叫做闭包

     ```js
     function A(){
         let a = 1
         function B() = {
             console.log(a)
         }
     }
     ```

   * 用途

     一是常常用来'间接访问一个变量'，而是让这个变量的值始终保持在内存中。

   * 缺点

     由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在IE中可能导致内存泄露。解决方法是，在退出函数之前，将不使用的局部变量全部删除。

     闭包会在父函数外部，改变父函数内部变量的值。所以，如果你把父函数当作对象（object）使用，把闭包当作它的公用方法（Public Method），把内部变量当作它的私有属性（private value），这时一定要小心，不要随便改变父函数内部变量的值

2. call、apply、bind 的用法分别是什么？

   * call() 方法使用一个指定的 this 值和单独给出的一个或多个参数来调用一个函数。

     `function.call(thisArg, arg1, arg2, ...)`

   * apply() 方法调用一个具有给定this值的函数，以及以一个数组（或类数组对象）的形式提供的参数。

     `func.apply(thisArg, [argsArray])`

   * bind() 方法创建一个新的函数，在 bind() 被调用时，这个新函数的 this 被指定为 bind() 的第一个参数，而其余参数将作为新函数的参数，供调用时使用。

     `function.bind(thisArg[, arg1[, arg2[, ...]]])`

   * 相同之处

     改变函数体内 this 的指向。

   * 不同之处

     call、apply的区别：接受参数的方式不一样。

     bind：不立即执行。而apply、call 立即执行。

3. 请说出至少 10 个 HTTP 状态码，并描述各状态码的意义。

   * 100 - 继续。客户端应继续其请求

   * 200 - 请求成功。一般用于GET与POST请求
   * 201 - 已创建。成功请求并创建了新的资源
   * 202 - 已接受。已经接受请求，但未处理完成
   * 301 - 资源（网页等）被永久转移到其它URL
   * 302 -  临时移动。与301类似。但资源只是临时被移动。客户端应继续使用原有URI
   * 404 - 请求的资源（网页等）不存在
   * 405 - 客户端请求中的方法被禁止
   * 406 - 服务器无法根据客户端请求的内容特性完成请求
   * 500 - 内部服务器错误
   * 502 - 作为网关或者代理工作的服务器尝试执行请求时，从远程服务器接收到了一个无效的响应

4. 如何实现数组去重？
   假设有数组 `array = [1,5,2,3,4,2,3,1,3,4]`,你要写一个函数 unique，使得到的值为 `unique(array) = [1,5,2,3,4]`，也就是把重复的值都去掉，只保留不重复的值。

   * 使用Set

     ```js
     function unique(array){
       return Array.from(new Set(array))
       // 可简化return [...new Set(array)]
     }
     var array = [1,5,2,3,4,2,3,1,3,4]
     console.log(unique(array))
     // [1,5,2,3,4]
     ```

     对象不会去重。

   * 不使用Set

     ```js
     function unique(arr) {
       let map = new Map();
       let array = [];  // 数组用于返回结果
       for (let i = 0; i < arr.length; i++) {
         if(map.has(arr[i])) {  // 如果有该key值
           map.set(arr[i], true); 
         } else { 
           map.set(arr[i], false);   // 如果没有该key值
           array .push(arr[i]);
         }
       } 
       return array ;
     }
     var array = [1,5,2,3,4,2,3,1,3,4]
     console.log(unique(array))
     // [1,5,2,3,4]
     ```

     对象不会去重。

5. DOM 事件相关,事件委托是什么，怎么阻止默认动作，怎么阻止事件冒泡？

   * 事件委托

     利用事件冒泡的原理，让自己所触发的事件，让其父元素代替执行。

   * 阻止默认动作

     ```js
     非IE浏览器：event.preventDefault()
     IE浏览器：window.event.returnValue  = false
     
     function stopDefault(e) {
       //阻止默认浏览器动作(W3C)
       if (e && e.preventDefault) e.preventDefault();
       //IE中阻止函数器默认动作的方式
       else window.event.returnValue = false;
       return false;
     }
     
     ```

     

   * 阻止事件冒泡

     ```js
     非IE浏览器：event.stopPropagation()
     IE浏览器：window.event.cancelBubble = true
     
     function stopBubble(e){
         // 如果提供了事件对象，则是非IE浏览器下
         if(e && e.stopPropagation){
             // 因此它支持W3C的stopPropagation()方法
             e.stopPropagation()
         }else{
             // IE浏览器下，取消事件冒泡
             window.event.cancelBubble = true
         }
     }
     
     ```

     

6. 如何理解 JS 的继承？

   * 基于原型继承

     ```js
     function Parent(value){
         this.val = value // 实例属性
     }
     Parent.prototype.getValue = function(){ // 原型属性
         console.log(this.val)
     }
     function Child(value){
         Parent.call(this,value) // 借用构造函数来继承实例属性
     }
     Child.prototype = new Parent() // 原型链继承
     const child = new Child(1)
     child.getValue() // 1
     child instancof Parent // true
     ```

     

   * 基于class继承

     ```js
     class Parent{
         constructor(value){
             this.val = value
         }
         getValue(){
             console.log(this.val)
         }
     }
     class Child extends Parent{
         constructor(value){
             super(value)
         }
     }
     let child = new Child(1)
     child.getValue() // 1
     child instanceof Parent // true
     
     ```

     

7. 给出正整数数组 `array = [2,1,5,3,8,4,9,5]`，请写出一个函数 sort，使得 sort(array) 得到从小到大排好序的数组 `[1,2,3,4,5,5,8,9]`，新的数组可以是在 array 自身上改的，也可以是完全新开辟的内存。（不得使用 JS 内置的 sort API）

   * ```js
     let min = (numbers) => {
             if (numbers.length > 2) {
                 return min(
                     [numbers[0], min(numbers.slice(1))]
                 )
             } else {
                 return Math.min.apply(null, numbers)
             }
         }
         let minIndex = (numbers) =>{ return  numbers.indexOf(min(numbers))}
             // 求出某个数字下标
     
     
         let sort = (numbers) => {
             if (numbers.length > 2) {
                 let index = minIndex(numbers)
                 console.log(`index:${index}`)
                 let min = numbers[index]
                 console.log(`min:${min}`)
                 numbers.splice(index, 1)
                 console.log(`numbers:${numbers}`)
                 return [min].concat(sort(numbers))
             } else {
                 return numbers[0] < numbers[1] ? numbers : numbers.reverse()
             }
         }
         array = [2,1,5,3,8,4,9,5]
         console.log(sort(array))
     ```

     

8. 你对 Promise 的了解？

   * Promise 的用途

     Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。

   * 如何创建一个 new Promise

     `return new Promise(((resolve, reject) => ))`

   * 如何使用 Promise.prototype.then

     then() 方法返回一个 Promise。它最多需要有两个参数：Promise 的成功和失败情况的回调函数。

     ```js
     const promise1 = new Promise((resolve, reject) => {
       resolve('Success!');
     });
     
     promise1.then((value) => {
       console.log(value);
       // expected output: "Success!"
     });
     ```

     

   * 如何使用 Promise.all

     Promise.all() 方法接收一个promise的iterable类型的输入，并且只返回一个Promise实例， 那个输入的所有promise的resolve回调的结果是一个数组。这个Promise的resolve回调执行是在所有输入的promise的resolve回调都结束，或者输入的iterable里没有promise了的时候。它的reject回调执行是，只要任何一个输入的promise的reject回调执行或者输入不合法的promise就会立即抛出错误，并且reject的是第一个抛出的错误信息。

     ```js
     const promise1 = Promise.resolve(3);
     const promise2 = 42;
     const promise3 = new Promise((resolve, reject) => {
       setTimeout(resolve, 100, 'foo');
     });
     
     Promise.all([promise1, promise2, promise3]).then((values) => {
       console.log(values);
     });
     // expected output: Array [3, 42, "foo"]
     
     ```

     

   * 如何使用 Promise.race

     **`Promise.race(iterable)`** 方法返回一个 promise，一旦迭代器中的某个promise解决或拒绝，返回的 promise就会解决或拒绝。

     ```js
     const promise1 = new Promise((resolve, reject) => {
       setTimeout(resolve, 500, 'one');
     });
     
     const promise2 = new Promise((resolve, reject) => {
       setTimeout(resolve, 100, 'two');
     });
     
     Promise.race([promise1, promise2]).then((value) => {
       console.log(value);
       // Both resolve, but promise2 is faster
     });
     // expected output: "two"
     
     ```

9. 跨域

   * 什么是同源

     Javascript只能与同一个域中的页面进行通讯。

     协议相同、端口相同、域名相同。

   * 什么是跨域

     跨域，是指浏览器不能执行其他网站的脚本。它是由**浏览器的同源策略**造成的，是浏览器对JavaScript实施的安全限制。

   * JSONP 跨域

     网页通过添加一个`<script>元素`，向服务器请求 JSON 数据，服务器收到请求后，将数据放在一个指定名字的回调函数的参数位置传回来。

     优点：兼容IE、跨域。

     缺点：读不到HTTP状态码、只支持GET请求不支持PSOST

   * CORS 跨域

     CORS是一个W3C标准，全称是"跨域资源共享"（Cross-origin resource sharing）。 它允许浏览器向跨源服务器，发出XMLHttpRequest请求，从而克服了AJAX只能同源使用的限制。

     普通跨域请求：只需服务器端设置Access-Control-Allow-Origin

     带cookie跨域请求：前后端都需要进行设置

10. 对前端的理解

    * 最贴近用户的程序员
    * 实现页面交互，提升用户体验
    * 技术更新迭代快但核心还是HTML，CSS， JavaScript
    * 学会查文档，搜索答案
    * 从一个个小目标开始实现
    * 不要只会调用api，要理解和学习自己封装。


