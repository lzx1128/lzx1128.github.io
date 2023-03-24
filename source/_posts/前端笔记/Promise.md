---
title: Promise基础教程
description: 🥪本文汇总Promise基础教程 ，可作为文档进行查询
mathjax: true
tags:
 - Promise
categories:
 - 前端笔记
abbrlink: 303
sticky: 2
cover: https://s1.vika.cn/space/2022/12/29/bd9e858c5ae44d74a300efaf70aafff3
swiper_index: 2
date: 2023-03-20 18:19:03
updated: 2023-03-20 22:00:00
---

# Promise
 ## 1. Promise的介绍

* 它是一门新的技术（ES6中引入），是JS中进行异步编程的新解决方法，解决了就方案中的回调地狱问题。

* 在promise的语法上来看，**它是一个构造函数**；promise对象用来封装一个异步操作并可以获取成功或失败的结果值。

* 状态改变上分为两种情况：且一个promise对象的状态只能改变一次

  ​	pending ----> resolved

  ​	pending ----> rejected

* promise的基本流程：如下图所示

  ![image-20200915182146260](C:%5CUsers%5CAdministrator%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200915182146260.png)

## 2. Promise的基本使用

```js
// 创建promise对象，刚创建的对象状态为pending，指定执行器函数
const p = new Promise((resolve,reject)=>{
    // 在执行器函数中启动异步任务
    fs.readFile("./index.html",(err,data)=>{
        // 如果状态为失败，就调用reject()
        if (err) reject(err);
        // 如果状态为成功，就调用resolve()
        resolve(data);
    });
});
// promise对象的状态改变后，就调用then方法
p.then(value=>{
    console.log("成功");
},reason=>{
    console.log("失败");
})
```

## 3. Promise中的API

### 	1.	 实例对象的方法

* Promise构造函数，new Promise（excutor{ }），执行器函数（同步）

* Promise.prototype.then(onResolved, onRejected) ------ 成功的回调函数，失败的回调函数（异步）

* Promise.prototype.catch(onRejected），专门用来解决失败的回调函数（异步）

  .then()方法中可以只传入成功的回调函数，失败的回调都交给catch来解决

### 	2.   函数对象的方法

  * Promise.resolve() 接收一个参数，返回Promise对象
    1. 如果传入的参数是非Promise类型的数据，那么返回的这个promise对象的状态是resolve，值就是传入的参数的值
    2. 如果传入的参数是一个Promise对象，那么传入的promise对象的状态就决定了返回的这个promise对象的状态，值就是里面的promise对象中的值
    3. 作用：快速对数据进行包裹，进行promise的转换，方便后面的操作。
  * Promise.reject()接收一个参数，始终是返回一个失败的promise对象
    	1. 无论传入的参数是什么，结果都是一个失败状态的Promise对象，且失败的值就是传入的参数的值。
* Promise.all()，接收的参数是一个数组，且每个值都是一个Promise对象，返回的结果也是一个promise对象 
  	1. 如果数组中所有对象的状态都为成功，那么返回的promise对象的状态为成功，成功的值和数组中的顺序一一对应；如果有一个为失败，那么返回的promise对象的状态就为失败，且失败的值就是那么失败的对象的值，如果几个值都失败了，那么谁先失败谁就决定结果。
* Promise.race() 接收的参数是一个数组，且每个值都是一个Promise对象，返回的结果也是一个promise对象 ，结果由最先改变状态的那个promise决定。

## 4. async / await （回调地狱的终极解决方案）

async函数是Generator函数的语法糖。但是相比Generator而言，async不需要调用next方法才能执行，它自带执行器（await）。

* 语义

  async表示函数里有异步操作，await表示紧跟在后的表达式需要**等待结果**

* await的返回值

  await后面，可以跟Promise对象（异步）或原始类型的值（Number，String，Boolean）（同步）; 如果它的返回值是Promise对象，就可以使用then指定下一步的操作；如果是非Promise对象，就返回相应的值。

  ```js
  async function f(){
      return await 123; // 相当于return 123
  }
  f().then(v=>console.log(v)); // 123
  //************************************
  
  // 如果await后面的Promise是reject状态，整个async函数会中断执行。这时需要catch来接收reject的参数
  async function f() {
        await Promise.reject("出错了");
  }
  
  f().then((v)=>{console.log(v)})
     .catch((e)=>{console.log(e)}) //出错了
  
  // ********************************************
  
  // 如果不希望第一异步操作失败去影响第二个异步操作，可以使用try...catch..来处理
  async function fn(){
      try{
          await Promise.reject("出错了");
      }catch(e){
          return await Promise.resolve("成功执行了");
      }
  }
  fn().then(v=>{console.log(v)}) // 成功执行了
  	.catch(e=>{console.log(e)});
  ```

  

* async函数内部如果有return的值，会成为then方法的参数

  ```js
  async function f(){
      return "hello async";
  };
  f().then(v=>{console.log(v)}); // hello async
  ```

* async后面的Promise对象的状态变化

  由于async函数返回的都是Promise对象，因此，必须等到async内部所有的await命令后面的Promise对象都执行完，才会发生状态变化；除非遇到return语句或者抛出错误。（也就是说，只有当async函数内部的异步操作都执行完，才会执行then方法的回调函数）。

## 5. promise中的几个关键问题

 1. 如何改变promise的状态

    * resolve 函数	pending ----> resolve
    * reject 函数       pending ----> reject
    * 抛出异常 throw   pending ----> reject

	2.  一个promise指定多个回调函数（也就是调用多个then或catch方法），都会调用吗？

    ```js
    let p = new Promise((resolve,reject)=>{
        resolve("成功")
    });
    p.then(value =>{
        console.log(value);
    });
    p.then(value =>{
        alert(value);
    })
    ```

    * 只要promise的状态改变了，那么**对应的回调都会运行**

	3. 改变promise的状态和指定回调函数那个先执行? (都有可能)

    这两个的执行顺序主要是由执行器函数内部封装的任务决定的，如果封装的是同步任务，那么promise对象的状态先改变，指定回调后执行；如果封装的是异步任务，那么情况就反过来了；

    大多数情况下，都是指定回调在前（then调用），改变状态在后（resolve，reject）；

	4. promise.then()的返回的新promise对象的结果由什么决定？

    由then指定的回调函数执行的结果决定

    * 抛出异常，新promise的状态变为rejected，reason为抛出的异常
    * 返回的是非promise的任意数据，新promise的状态变为resolved，value为返回的值
    * 返回的是另一个新的promise，这个promise的状态就会成为then返回的那个promise对象的状态

	5. 使用then方法的链式调用来串联多个操作任务，当使用了then的链式调用，可以在最后再进行失败的回调，这时利用了promise的异常穿透原理；想要中断链式调用时，就在回调函数中返回一个pending状态的promise对象。

    ```js
    new Promise((resolve,reject)=>{
        resolve("Ok");
    })
    .then(value=>{
        console.log(value,1111);
    })
    .then(value=>{
        console.log(value,2222);
        // 如果不想执行到3333，就返回一个pending状态的promise对象
        // return new Promise(()=>{});
    })
    .then(value=>{
        console.log(value,3333);
    }).catch(reason=>{
        console.log(reason,4444);
    })
    /*
    输出结果为:
     ok 1111
     undefined 222   结果为undefined是因为前一个then没有返回值，默认为undefined
     undefined 333 
    */
    
    ```

## 6. JS异步之红队列和微队列

### 1. 原理图

![img](https://img-blog.csdnimg.cn/20191111155015676.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDAxMzgxNw==,size_16,color_FFFFFF,t_70)

### 2. JS中用来存储待执行回调函数的队列包含2个：

宏队列：用来保存待执行的宏任务（回调）

		* 定时器的回调
		* DOM事件回调
		* AJAX回调

微队列：用来保存待执行的微任务（回调）

* promise回调
* MutationObserver回调

JS的执行顺序：先执行同步任务，碰到异步任务就将其放入对应的异步任务队列中（宏队列&微队列）；同步任务执行完成后，每次准备执行宏队列之前，先检查微队列中是否有任务在等待执行，有就先执行微队列的任务；最后再执行宏队列中的待执行任务。

## 7. promise的相关题目

* 第一题

  ```js
  setTimeout(()=>{
      console.log(1)
    },0)
  Promise.resolve().then(()=>{
      console.log(2)
  })
  Promise.resolve().then(()=>{
     console.log(4)
  })
  console.log(3);
  // 3 2 4 1
  ```

* 第二题

  ```js
  setTimeout(() => {
      console.log(1)
    }, 0)
  new Promise((resolve) => {
    	console.log(2)
    	resolve()
  }).then(() => {
      console.log(3)
  }).then(() => {
      console.log(4)
  })
    console.log(5)
  // 2 5 3 4 1
  ```

* 第三题

  ```js
  const first = () => (new Promise((resolve, reject) => {
      console.log(3)
  	let p = new Promise((resolve, reject) => {
        console.log(7)
        setTimeout(() => {
          console.log(5)
          resolve(6)
        }, 0)
        resolve(1)
      })
      resolve(2)
      p.then((arg) => {
        console.log(arg)
      })
  }))
  first().then((arg) => {
      console.log(arg)
  })
  console.log(4)
  // 3 7 4 1 2 5
  ```

* 第四题

  ```js
  setTimeout(() => {
      console.log("0")
    }, 0)
    new Promise((resolve,reject)=>{
      console.log("1")
      resolve()
    }).then(()=>{        
      console.log("2")
      new Promise((resolve,reject)=>{
        console.log("3")
        resolve()
      }).then(()=>{      
        console.log("4")
      }).then(()=>{       
        console.log("5")
      })
    }).then(()=>{  
      console.log("6")
    })
  
    new Promise((resolve,reject)=>{
      console.log("7")
      resolve()
    }).then(()=>{         
      console.log("8")
    })
  // 1 7 2 3 8 4 6 5 0
  ```

  





















