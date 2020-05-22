# fed-e-task-01-01
作业
### 问题1：请说出下列程序的执行结果
	var a = []
	for(var i = 0;i < 10; i++){
		a[i] = function() {
			console.log(i)
		}
	}
	a[6]()
结果：10
解释：因为var声明的变量会进行变量提升，当for循环结束后i变为变为了10，当执行时i已经改为了10

### 问题2：结果为报错
	var tmp =123
	if(true){
		console.log(tmp)
		let tmp
	}
解释：
（1）代码块内let一旦对某个变量进行了声明，就存在了暂时性死区，也就是该块内所用变量都是此变量。
（2）let声明的变量不存在变量提升，需要先声明后使用，此题使用了未经声明的变量，故而报错。

### 问题3：结合ES6的新语法，用最简单的方式找出最小值
	var arr = [12,34,32,89,4]
答案：
console.log(Math.min(...arr)) ==>4
解释：
（1）Math.min()用于查找一组数字中最小的值，但如果有无法转换为number的数据结果为NaN,因为给定的数据都是数值，所以便采用了此方法
（2）...arr可以将数组展开，直接作为Math.min()的参数传入

### 问题4：详细说明var、let、const 三种声明变量方式直接的具体差别

答：
	（1）是否变量提升：var声明的变量会存在提升（可以先使用再声明，但不建议），而后两者声明的变量不存在变量提升（必须先声明再使用，否则报错）
	（2）作用域：var声明的变量作用域为全局作用域或函数作用域，而后两者声明的变量都是块级作用域，只能在块内使用
	（3）是否可以重复声明：var声明的变量可以重复声明,如果多次声明只进行值替换。而后两者不可以重复声明
	（4）const声明的常量，如果是引用数据类型，不可更改指向。声明时必须赋值，而另外两者可以先声明再赋值
	
### 问题5：请说出下列代码的执行结果
	var a = 10
	var obj = {
		a:20,
		fn(){
			setTimeout(()=>{
				console.log(this.a)
			})
		}
	}
	obj.fn()
结果：20
解释：谁调用它，它指向谁，不改变this指向。

### 问题6：简述Symbol类型的用途
答：
主要用于在开发过程中定义唯一的key,减少协调工作中key冲突问题

### 问题7：说说什么是深拷贝、什么是浅拷贝
答：
浅拷贝就是两者指向同一内存地址，更改一个会对另一个产生影响
深拷贝就是指向不同的内存地址，相互更改不会产生影响
		let sevnA = [10,20,30,40]
		let sevnB = sevnA
		sevnB[0]=100
		console.log(sevnA)  //结果是[ 100, 20, 30, 40 ] 此时sevnA和sevnB指向同一内存地址
解决浅拷贝个人常用方式是JSON.parse(JSON.stringify（））

### 问题8：谈谈你是如何理解js异步编程的，EventLoop是做什么的？什么是宏任务，什么是微任务？

（1）js任务分为同步任务和异步任务，
同步任务也就是阻塞任务，后续任务需要等待它执行结束后才能执行
异步任务就是不等待执行结果，继续向后执行。js中setTimeout、setInterval、Promise、等都是异步任务。
既然不等待异步的执行结果，那我们就要在异步任务执行完成后通知js继续执行它的回调函数，这个时候就用到了EventLoop。
（2）EventLoop，我个人理解为它会在执行栈的同步任务结束后进行扫描EventQueue中是否存在待执行的微任务，有就将微任务放入到执行栈进行执行，当执行栈执行结束后又再次去查找Queue是否存在待执行的微任务、宏任务。直至执行栈、queue全部都执行结束。
（3）任务队列分为微任务和宏任务，微任务可以理解为VIP任务，可以优先于宏任务执行。



### 问题9：将下面的异步代码用Promise改进一下
	setTimeout(function(){
		var a = 'hello ';
		setTimeout(function(){
			var b = 'lagou ';
			setTimeout(function(){
				var c = "I love U";
				console.log(a + b + c)
			},10)
		},10)
	},10)
	改造后
	const promise = new Promise(function(resolve,reject){
		setTimeout(resolve('hello '),10)
	})
	promise
	.then((res)=>{
		return new Promise(function(resolve,reject){
			setTimeout(resolve(`${res}lagou `),10)
		})
	})
	.then((res)=>{
		return new Promise(function(resolve,reject){
			setTimeout(resolve(`${res}I love U`),10)
		})
	})
	.then((res)=>{
		console.log(res)
	})
	输出结果为 hello lagou I love U
### 问题10：简述TypeScript和JavaScript的关系
答:ts属于js的超集，使用ts可以将我们js的弱类型语言增强，使得我们减少因类型错误引起的bug.
我们的ts代码编译后是正常的js文件
	
### 问题11：谈谈你认为的TypeScript的优缺点
答：
优点：使用TS可以减少因类型变化产生的未知错误，可以更加稳定健全
缺点：增加了学习成本和时间成本，对老代码的重构工作量会比较大。
