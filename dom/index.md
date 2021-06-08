# DOM


# DOM编程

#### JS七种数据类型

number,string,bool,symbol,null,undefined,object

#### JS五个falsy值

0,NaN,'',null,undefined

#### DOM定义

- 含义：Document Object Model 文档对象模型；浏览器往window上加一个document，JS就可以操作网页

#### 获取元素（element），也叫标签(tag)

- window.idXXX 或者 idXXX
- document.getElementById('idXXX')
- document.getElementsByTagName('div')[0]
- document.getElementsByClassName('red')[0]
- document.querySelector('#idXXX')
- document.querySelectorAll('.red')[0]

#### 获取待定元素

- 获取html元素：document.documentElement
- 获取head元素：document.head
- 获取body元素：document.body
- 获取窗口(窗口不是元素)：window
- 获取所有元素：document.all

#### 节点Node

包括(常用):

- 1表示元素Element，也叫标签Tag
- 3表示文本
- 8表示注释Coment
- 9表示文档Dcument
- 11表示文档片段DocumentFragment

#### cosole.dir(div)看原型链

- 第一层原型：HTMLDIVElement.prototype（这里包含div所有共有属性）
- 第二层原型：HTMLElement.prototype(这里面所有HTML标签共有属性)
- 第三层原型：Element.prototype(这里所有XML,HTML标签共有属性，不会以浏览器只能展示HTML)
- 第四场原型：Node.prototype(这里面所有节点共有属性，节点包括XML标签文本注释，HTML标签文本注释等)
- 第五层原型：EventTarget.prototype(里面最重要函数是addEventListener)
- 第六层原型：Object.prototype

![image](https://segmentfault.com/img/bVcO4LK)

#### 节点增加

- 创建一个标签节点

```
1. let div1=document.createElement('div')
2. document.createElement('style')
3. document.creatElement('script')
4. document.createElement('li')
```

- 创建一个文本节点

```
text1=document.createTextNode('你好')
```

- 标签里面插入文本

```
 div1.appendChild(text1)
 div1.innerText='你好' 或 div1.textContent='你好'
```

*插入页面

1. 创建标签默认处于JS线程中
2. 必须把它插到head或者body立，才会生效
3. 

```
document.body.appendChild(div)
```

4.在已有页面中元素.appendChild(div)

#### 节点的删除

- 两种方法：

1. 旧方法：parentNode.childChild(childNode)
2. 新方法：childNode.remove() //IE不支持

#### 节点的改属性

- 写标准属性

```
1. 改class:div.className='red blue'
2. 改class:div.classList.add('red')
3. 改style:div.style='width:100px;color:blue'
4. 改style的一部分:div.style.width='200px'
5. 大小写：div.style.backgroundColor='white'
6. 改data-*属性：div.dataset.x='frank'
```

- 读标准属性

```
 div.classList/a.href
 div.getAttribut('class')/a.getAttribut('href')
```

两种都可以用，但是值可能会稍微有点不同

- 改事件处理函数

1. div.onclick默认null
2. 默认点击，div不会有任何事情发生
3. 但如果把div.onclick改成一个函数fn
4. 那么点击div的时候，浏览器就会调用这个函数
5. 并且是这样被调用fn.call(div.event)
6. div会被当成this
7. event则包含了点击事件的所有信息，如坐标
8. div.addEventListener是div.onclick的升级

![image](https://segmentfault.com/img/bVcO4LJ)

- 节点改内容

1.改文本内容

```
div.innerText='xxx'
div.textContent='xxx'
```

2.改HTML内容

```
div.innerHTML='<strong>重要内容</strong>'
```

3.改标签

```
div.innerHTML=''    //先清空
div.appendChild(div2)  //再加内容
```

4.改爸爸

```
newParent.appendChild(div)
```

#### 节点的查询

- 查爸爸

```
node.parentNode 或 node.parentElement
```

- 查爷爷

```
node.parentNode.parentNode
```

- 查子代

```
node.childNodes 或 node.children
```

- 查兄弟姐妹

```
node.parentNode.childNodes  //排除自己
node.parentNode.children   //排除自己
```

- 查老大

```
node.firstChild 或 node.children[0]
```

- 查老幺

```
node.lastChild
```

- 查看上一个哥哥/姐姐

```
node.previousSibling
```

- 查看下一个弟弟/妹妹(注意这里可能查到文本节点)

```
node.nextSibling
```

- 遍历一个div里面所有的元素

```
travel = (node.fn)=>{
   fn(node)
    if(node.children){
      for(let i=0;i<node.children.length;i++){
        travel(node.children[1],fn)
      }
    }
}
travel(div1,(node)=>console.log(node))
```

#### 跨线程操作

##### 属性同步

- 标准属性

1. 对div1的标准属性修改，会被浏览器同步到页面中
2. 比如id,className,title等
3. data-*属性

- 启示：如果有自定义属性，想被同步到页面中，请使用data-作为前缀

#### Property 与 Attribute

- property属性：JS线程中div1的所有属性，叫做div1的property
- Attribut属性：渲染引擎中div1对应标签的属性，叫做attribute
- 区别：大部分时候，两者的值是相等的；但如果不是标准属性，那么它们一开始时相等，但attribute只支持字符串，而property支持字符串，布尔等类型

#### 注意

1.假设页面中有如下元素

```
<div id="test" class="red">demo</div>
```

获取该 div 元素的代码:
1) document.getElementById('test')
2) document.getElementsByClassName('red')[0]
3) window.test
4) document.querySelector('#test')
5) document.querySelectorAll('#test')[0]

2.关于节点(Node) 、元素(Element)、标签(Tag) 的关系描述:
1) 节点包括元素和文本等
2) 元素就是标签，叫法不同而已

3.要删除一个节点 x
1) x.parentNode.removeChild(x)
2) x.remove()

4.获取 x 元素的 class 属性
1) x.className
2) x.getAttribute('class')

5.将 div 的宽度设置为 100 像素
div.style.width = '100px'

6.关于以下代码，下列说法正确

```
div.onclick = function(){
    console.log(this)
    console.log(arguments[0])
}
```

1) 当用户点击该 div 时，该代码中的 this 是 div
2) 当用户点击该 div 时，arguments[0] 是事件相关的信息组成的对象

