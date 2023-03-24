---
title: React全家桶
description: 🥙本文汇总React全家桶 ，可作为文档进行查询
mathjax: true
tags:
 - React
categories:
 - 前端笔记
abbrlink: 400
sticky: 2
cover: https://s1.vika.cn/space/2022/12/29/e716acea2d0946348091e84e2d70f0ea
swiper_index: 2
date: 2023-03-20 18:19:03
updated: 2023-03-20 22:00:00
---
# React全家桶(技术栈)

 英文官网:https://reactjs.org

### 一、简介

#### 1.介绍描述

​    ① 用于动态构建用户界面的 JavaScript 库(只关注于视图)

​    ②由Facebook开源

#### 2.特点

-  声明式编码
- 组件化编码  
- React Native 编写原生应用
-  高效（优秀的Diffing算法）

#### 3.高效原因

   使用虚拟(virtual)DOM, 不总是直接操作页面真实DOM

   DOM Diffing算法, 最小化页面重绘

### 二、基本使用

```HTML
<body>
		<!-- 准备好一个容器，用于让react渲染用 -->
		<div id="test"></div>
		<!-- 引入react核心库 -->
		<script type="text/javascript" src="../js/react.development.js"></script>
		<!-- 引入react-dom，用于支持react操作DOM -->
		<script type="text/javascript" src="../js/react-dom.development.js"></script>
		<!-- 引入babel，用于将jsx转为js -->
		<script type="text/javascript" src="../js/babel.min.js"></script>

		<!-- 下面一定要将javascript改为babel，含义是：让babel翻译script标签中的代码。 -->
		<script type="text/babel"> 
			
			//1.创建虚拟DOM
			const VDOM = <h1>Hello,React</h1> //此处一定不要写引号，因为VDOM不是字符串！！！
			
			//2.利用ReactDOM.render(虚拟DOM,容器) 方法将虚拟DOM插入指定容器
			ReactDOM.render(VDOM,document.getElementById('test'))
			
		</script>
	</body>
```

#### 1.创建虚拟DOM的两种方式

  ==①==

```javascript
const VDOM = (
				<h1 id="title">
					<span>Hello,React</span>
				</h1>
			)
```

②（不推荐）

 -----------------------React.createElement(标签名,{标签属性},标签体内容)

```javascript
const VDOM = React.createElement('h1',{id:'title'},'Hello,React')
```

#### 2.虚拟DOM与真实DOM

- 虚拟DOM的本质就是Object类型的一般对象。
- 虚拟DOM比较“轻”，真实DOM比较“重”，因为虚拟DOM是给react用的,无需那么多的属性。
- 我们编码时基本只需要操作react的虚拟DOM相关数据，虚拟DOM对象最终都会被React转换为真实的DOM。

#### <span style='color:red'>3.jsx的语法规则</span>

-         **<span style='color:red'>创建虚拟DOM时，不要用引号</span>。**
-        **标签中想混入js表达式，需要用<span style='color:red'> {}</span>包裹。**
-             **<span style='color:red'>根标签</span>必须只有<span style='color:red'>一个</span>**
-             **标签必须<span style='color:red'>闭合</span>**
-             **<span style='color:red'>样式的类名</span>，不要用class，必须用<span style='color:red'>className</span>**
-              **<span style='color:red'>内联的样式</span>要用 <span style='color:red'>style={{}}</span>形式去写**
-              **标签可以随意的编写：**

​                  **(1).若标签首字母是【小写】的，则react会尝试将当前的jsx标签对应成一个html标签**

​                          **若对应成了，直接渲染，展示。**

​                          **若无法对应，直接报错！**

​                  **(2).若标签首字母是【大写】的，则react会查找Haha组件的定义的位置**

​                          **若找见了，直接渲染Haha组件**

​                          **若未找见，报错(Haha is not defined)**

#### 4.区分js语句与js表达式

​       ①表达式：一个表达式会产生一个值，可以放在任何一个需要值的地方下面这些都是表达式：
​												(1). a
​												(2). a+b
​												(3). demo(1)
​												(4). arr.map() 
​												(5). function test () {}
​        ②语句(代码)：下面这些都是语句(代码)：
​												(1).if(){}
​												(2).for(){}
​												(3).switch(){case:xxxx}

#### 备注：

==①数组（Array）.map( )方法==：

​                   用来生成 / 创建一个新数组。
​                           其结果是 该数组中的每个元素 调用一次提供的函数后的返回值。
​                           map 不修改原数组本身  

​                   所以map方法必须有返回值，如果没有return，那么新数组的每一项都为undefined，数组的个数与原数组一样

<span style='color:red; font-size:18px; font-weight:700'> ②react可以自动遍历数组，但是不可以遍历对象</span>



### 三、模块与组件、模块化与组件化

#### 1.模块与模块化

-  理解：向外提供特定功能的js程序, 一般就是一个js文件
-  为什么要拆成模块：随着业务逻辑增加，代码越来越多且复杂。
-  作用：复用js, 简化js的编写, 提高js运行效率

   ==当应用的js都以模块来编写的, 这个应用就是一个模块化的应用==

#### 2.组件与组件化

- 理解：用来实现局部功能效果的代码和资源的集合(html/css/js/image等等)
- 为什么要用组件： 一个界面的功能更复杂
- 作用：复用编码, 简化项目编码, 提高运行效率

  ==当应用是以多组件的方式实现, 这个应用就是一个组件化的应用==

#### 3.组件

<span style='color:red'>**①函数式组件**</span>

```javascript
<script type="text/babel"> 
			//1.定义组件(函数式组件)
			function MyComponent(){//函数式组件 函数名字开头大写
				console.log(this); //此处的this是undefined，因为经过babel的编译后，开启了严格模式。
				return <h2>我是用函数定义的组件（适用于【简单组件】的定义）</h2>
			}
			//2.渲染组件到页面 
			ReactDOM.render(<MyComponent/>,document.getElementById('test'))
			/* 
			  执行了ReactDOM.render后，发生了什么？
			  1.React发现了<MyComponent/>标签，去寻找MyComponent组件定义的位置，发现MyComponent是用函数定义的。
			  2.React调用MyComponent并获取MyComponent返回的虚拟DOM，随后转为真实DOM，随后渲染到页面。
			 */
</script>
```

<span style='color:red'>**②类式组件**</span>

```javascript
<script type="text/babel"> 
			//定义组件
			class MyComponent extends React.Component{
				//render是放在哪里的？ —————— MyComponent的原型对象上，是给MyComponent的实例对象用的。
				render(){
					console.log(this); //MyComponent的实例对象 <==> MyComponent组件实例对象
					return <h2>我是用类定义的组件（适用于【复杂组件】的定义）</h2>
				}
			}
			//渲染组件到页面
			ReactDOM.render(<MyComponent/>,document.getElementById('test'))
			/* 
			  执行了ReactDOM.render后，发生了什么？
			  1.React发现了<MyComponent/>标签，去寻找MyComponent组件定义的位置，发现MyComponent是用类定义的。
			  2.React new了一个MyComponent实例对象--m
			  3.通过m调用到了MyComponent原型上的render方法，并获取到了返回的虚拟DOM，随后转为真实DOM，放在页面。
			 */
</script>
```

#### 4.组件实例的三大核心属性

①state：

   state是组件对象最重要的属性, 值是对象(可以包含多个key-value的组合)

   state(状态机)通过更新组件的state来更新对应的页面显示(重新渲染组件)。

基本使用

```javascript
<script type="text/babel"> 
			//1.定义组件----类式组件
			class Weather extends React.Component{
				//构造器调用几次？-------- 看你组件用几次
				constructor(props){
					super(props)
					this.state = {isHot:true,wind:'微风'} //初始化状态,isHot用于标识天气热不热
					this.changeWeather = this.changeWeather.bind(this) //解决this指向问题
				}
				//changeWeather调用几次？-------- 看你点几次
				changeWeather(){
					//若构造器中不做处理，那么下面的this是undefined，因为changeWeather不是通过实例调用的，而是作为点击的回调去使用，且类中的方法自动开启了严格模式。
					//console.log('changeWeather的this是',this); 

					//严重注意：状态(state)中的值是不能直接修改的！！！！下面这一行就是直接修改
					//this.state.isHot = true
                    
					//获取原来的state中的isHot值
					const {isHot} = this.state
					//更新状态
					this.setState({isHot:!isHot}) //此处更新状态是一个合并的动作，不是替换	
				}
				//render调几次？--------- 1+n次（n是更新状态的次数）
				render(){
                    //React中的绑定单击事件是onClick其中C大写
					return <h1 onClick={this.changeWeather}>今天天气很{this.state.isHot ? '炎热' : '凉爽'}，{this.state.wind}</h1>
				}
			}			
			//2.渲染组件
			ReactDOM.render(<Weather/>,document.getElementById('test'))
</script>
```

==简写模式==

```javascript
<script type="text/babel"> 
			//1.定义组件----类式组件
			class Weather extends React.Component{
				state = {isHot:true,wind:'微风23'} //初始化状态
				//事件的回调都需要写成赋值语句+箭头函数的形式
				changeWeather = ()=>{
					console.log('changeWeather');
					const {isHot} = this.state
					this.setState({isHot:!isHot})
				}
				render (){
					return (
						<h1 onClick={this.changeWeather}>
							今天天气很{this.state.isHot ? '炎热' : '凉爽'}，{this.state.wind}
						</h1>
					)
				}
			}
			//2.渲染组件
			ReactDOM.render(<Weather/>,document.getElementById('test'))
</script>
```

##### 注意:

​                          <span style='color:red'> 组件中render方法中的this为组件实例对象</span>

​                           <span style='color:red'>  组件自定义的方法中this为undefined，如何解决？</span>
​                                     <span style='color:red'>a)强制绑定this: 通过函数对象的bind()</span>
​                                     <span style='color:red'>b)箭头函数:通过箭头函数的this由外层作用域的this决定这一特性</span>

​                             <span style='color:red'>状态数据，不能直接修改或更新 需要通过setState({})</span>

②props：

​     每个组件对象都会有props(properties的简写)属性，值是对象(包括函数式组件)

​     组件标签的所有属性都保存在props中

​     ==通过标签属性从组件外向组件内传递变化的数据==

基本使用

```javascript
<script type="text/babel"> 
			//定义组件(类)
			class Person extends React.Component{
				render(){
					const {name,age,sex} = this.props
					return (
						<ul>
							<li>姓名：{name}</li>
							<li>性别：{sex}</li>
							<li>年龄：{age}</li>
						</ul>
					)
				}
			}
			//渲染组件
			ReactDOM.render(<Person name="tom" sex="女" age="18"/>,document.getElementById('test'))
			const p1 = {
				name:'程老师',
				sex:'男',
				age:18
			}
		//下面的...p1，并不是原生js里的{...p1},babel+react环境就可以让展开运算符展开一个对象，但是仅仅适用于传递标签属性！！
			ReactDOM.render(<Person {...p1}/>,document.getElementById('test2'))
</script>
```



对props中的属性值进行类型限制和必要性限制:

```javascript
//引入prop-types，用于制定对props限制的具体规则 
<script type="text/javascript" src="../js/prop-types.js"></script>
<script type="text/babel"> 
			//定义组件(类)
			class Person extends React.Component{
				//对传给Person组件的props进行类型的限制
				static propTypes = {
					name:PropTypes.string, //限制name必须为字符串类型
					sex:PropTypes.string.isRequired,//限制sex必须为字符串类型，且是必要属性
					age:PropTypes.number,//限制age必须为数值类型
					address:PropTypes.string, //限制address必须为字符串类型
				}
				//对传给Person组件的props进行默认值的设置
				static defaultProps = {
					address:'中国'
				}
</script>
```





函数组件的props属性（了解）

```javascript
<script type="text/babel"> 
			function Person(props){
				const {name,age,sex,address} = props
				//对传给Person组件的props进行类型的限制
				return(
					<ul>
						<li>姓名：{name}</li>
						<li>性别：{sex}</li>
						<li>年龄：{age}</li>
						<li>地址：{address}</li>
					</ul>
				)
			}
			Person.propTypes = {
				name:PropTypes.string, //限制name必须为字符串类型
				sex:PropTypes.string.isRequired,//限制sex必须为字符串类型，且是必要属性
				age:PropTypes.number,//限制age必须为数值类型
				address:PropTypes.string, //限制address必须为字符串类型
			}
			//对传给Person组件的props进行默认值的设置
			Person.defaultProps = {
				address:'中国'
			}

</script>
```



####  备注：

​     ①script type="text/babel" 经过==babel==编译的 开启严格模式 ==普通函数内部的this指向由window变为undefined==

​     ② ES6==类(class)==中所有方法自动开启了严格模式 ==普通函数内部的this指向由window变为undefined==

​     ③扩展运算符(...)无法展开一个对象，但可以通过 const newObject ={...object} 进行对象复制
