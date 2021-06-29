# 浅析MVC


# 浅析 MVC

1. MVC 三个对象分别做什么，给出伪代码示例

   * M（Model）：数据模型，负责数据及其相关的任务

     ```js
     const m = {
         data: {...},
         methods: {
             增、删、改、查...
         }
         ...
     }
     
     ```

   * V（View）：视图，负责用户界面

     ```js
     const v = {
         element: xxx,
         template: yyy,
         render(data){
             渲染用户视图
         }
         ...
     }
     ```

     

   * C（Controller）：控制器，用于控制应用程序的流程，处理用户事件，组织调度M和V更新数据和视图

     ```js
     const c = {
         bindEvents(){
             绑定用户事件    
         }
         ...
     }
     ```

2. EventBus 有哪些 API，是做什么用的，给出伪代码示例

   * eventBus是一个对象，它可以用来完成上述M、V、C对象间的通信。

     eventsBus提供了on、off、trigger等方法，用来处理事件。

     ```js
     m = {
         data: {...},
         methods: {
             ...
             update(data){
                 修改m.data
                 eventBus.trigger(A)
             }
         }
     }
     ```

3. 表驱动编程是做什么的（可以自己查查资料）

   * 表驱动法是一种编程模式——从表里查找信息而不是使用逻辑语句。
     随着逻辑复杂性的增加，if/else 或switch中的代码将变得越来越肿，所以我们常说数据比程序逻辑更易驾驭。表驱动法就是将这些逻辑中的数据与逻辑分开，从而减少逻辑的复杂度

     以一个月的天数为例，我们要写一串if/else 或者switch/case 来表达逻辑:

     ```js
     if(1 == iMonth) {iDays = 31;}
       else if(2 == iMonth) {iDays = 28;}
       else if(3 == iMonth) {iDays = 31;}
       else if(4 == iMonth) {iDays = 30;}
       else if(5 == iMonth) {iDays = 31;}
       else if(6 == iMonth) {iDays = 30;}
       else if(7 == iMonth) {iDays = 31;}
       else if(8 == iMonth) {iDays = 31;}
       else if(9 == iMonth) {iDays = 30;}
       else if(10 == iMonth) {iDays = 31;}
       else if(11 == iMonth) {iDays = 30;}
       else if(12 == iMonth) {iDays = 31;}
     ```

     但是我们把数据存到一张表里，就不需要冗余的逻辑了。

     ```js
     const month = {
       monthTable: [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31],
       get days(month, year) {
         // (year % 4 === 0) && (year % 100 !== 0 || year % 400 === 0) 闰年逻辑 
         return [month - 1];
       }
     }
     
     ```

     

4. 我是如何理解模块化的

   * 将一个复杂的程序依据一定的规则(规范)封装成几个块(文件), 并进行组合在一起
   * 块的内部数据与实现是私有的, 只是向外部暴露一些接口(方法)与外部其它模块通信
   * 可以随时修改某个模块的功能，不影响其他的模块

   

