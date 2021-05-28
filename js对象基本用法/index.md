# JS对象基本用法


# JS对象基本用法

* 声明对象的两种语法

  `let obj ={}`

  `let obj = new Object({}) `

* 如何删除对象的属性

  `delete obj.xxx`或`delete obj['xxx']`

* 如何查看对象的属性

  1. 查看自身所有属性

     `Object.keys(obj)`

  2. 查看自身+共有熟悉

     `console.dir(obj)`

     或者自己依次用`Object.keys`打印出`obj.__proto__`

  3. 判断一个属性是自身的还是共有的

     `obj.hashOwnProperty('toString')`

* 如何修改或增加对象的属性

  1. 修改自身直接赋值

     `obj['name']='jack'`

  2. 修改自身批量赋值

     `Object.assign(obj,{age:18,gender:'man'})`

  3. 修改共有熟悉

     `Object.prototype.toString = 'xxx'`

  4. 修改隐藏属性

     `Object.create(common)`

* 'name' in obj和obj.hasOwnProperty('name') 的区别

  前者不光检测当前对象，还会检测当前对象原型链中是否具有这个属性，后者只在当前对象自身上检测。

  


