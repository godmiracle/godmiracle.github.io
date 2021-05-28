# JS函数的执行时机


# JS 函数的执行时机

* 解释为什么如下代码会打印 6 个 6

  ```html
  let i = 0
  for(i = 0; i<6; i++){
    setTimeout(()=>{
      console.log(i)
    },0)
  }
  ```

  因为setTimeout是一个异步任务，执行到这里的操作会被浏览器丢到另一个任务队列里去，浏览器这时候会继续往下执行，把下面的代码都执行完了才会来执行setTimeout函数里的操作， 这时候因为for循环已经把i加到6了，所以输出的全部都是6。

* 写出让上面代码打印 0、1、2、3、4、5 的方法

  ```html
  for(let i = 0; i<6; i++){
    setTimeout(()=>{
      console.log(i)
    },0)
  }
  ```

* 除了使用 for let 配合，还有什么其他方法可以打印出 0、1、2、3、4、5

  ```html
  let i
  for(i = 0; i<6; i++){
      const x = i
      setTimeout(()=>{
        console.log(x)
      })
  }
  
  ```

  ```html
  let i
  for(i = 0; i<6; i++){
      setTimeout((value)=>{
        console.log(value)
      },0,i)
  }
  ```

  


