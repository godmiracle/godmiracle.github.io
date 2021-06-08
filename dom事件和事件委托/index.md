# DOM事件和事件委托


# 简述 DOM 事件模型

1. ## 事件流

   * ### 事件冒泡

     事件冒泡是IE 的事件流，事件是由最具体的元素接收，然后逐级向上传播，在每一级的节点上都会发生，直到传播到document对象，向Chrome这样的浏览器会冒泡到window 对象（很容易记忆，联想水里的泡泡不也这样么）。

   * ### 事件捕获

     事件捕获是Netscape浏览器开发团队提出的，很有意思，他们思想和IE 的截然相反。也就是说，从不具体的节点到最具体的节点，一般是从document对象开始传播，不过很少人用事件捕获的，还是事件冒泡用的多。

   * ### DOM 事件流

     这里规定的事件流有三个阶段： 事件捕获阶段，目标阶段，事件冒泡阶段。

     

   * ### 先捕获还是先冒泡

     2002年，w3c发布标准 文档名为DOM Level 2 Events Specification 规定浏览器应该同时支持两种调用顺序 首先按照grandfather->father->son 然后按照son->father->grandfather，开发者可以自己决定把fnYe放在捕捉阶段还是放在冒泡阶段

     ![Graphical representation of an event dispatched in a DOM tree using the DOM event flow](https://www.w3.org/TR/DOM-Level-3-Events/images/eventflow.svg)

     

     

2. ## 事件委托

   事件委托就是利用事件冒泡，只指定一个事件处理程序，就可以管理某一类型的所有事件。

   * 场景1:

     要给100个按钮添加点击事件，咋办？答：监听这个100个按钮的祖先，等冒泡的时候判断target是不是这100个按钮中的一个

   * 场景2:

     你要监听目前不存在的元素的点击事件？

     答：监听祖先，等点击的时候看看是不是监听的元素即可。

     优点：省监听数（内存），可以动态监听元素

   * 封装一个事件委托

     只要实行一个函数就可以实现事件委托要求：写出这样一个函数`on('click','#testDiv','li',fn)`当用户点击`#testDiv`里面的`li`元素时，调用fn函数要求用到事件委托

     ```javascript
     setTimeout(()=>{
       const button = document.createElement('button')
       button.textContent='click 1'
       div1.appendChild(button)
     },1000)
     
     on('click','#div1','button',()=>{//'#div'是选择器不是元素
       console.log('button 被点击啦')
     })
     function on(eventType,element,selector,fn){
       if(!(element instanceof Element)){
            element = document.querySelector(element)
          }
       element.addEventListener(eventType,(e)=>{
       const t= e.target//被点击的元素
       if(t.matches(selector)){//matches用来判断一个元素是否匹配一个选择器,selector是不是一个选择器
         fn(e)
        }
     })
     }
     ```

     

     

     


