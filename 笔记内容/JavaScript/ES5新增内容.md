# ES5新增

## 一、数组中新增的方法

### <u>**1.map**</u>

语法：arr.map(function(item,i)){

Return item*3(要对项目进行的操作)

}

含义：遍历数组，item代表每一个元素，并对其进行相应的操作

返回值：映射出来的新数组

### <u>**2.foreach**</u>

语法：arr.foreach(function(item,i){

无return

})

含义：遍历数组

返回值：无

### <u>**3.filter**</u>

语法：arr.filter(function(item,i){

return item>8

})

含义：过滤满足要求的数字内容，并输出一个新的数组

返回值：新的数组

### <u>**4.some**</u>

语法：arr.some(function(item,i){

Return item>8

})

含义：判断数组中是否有满足条件的，只要有则为true ，一个都没有则为FALSE

返回值：true or FALSE

### <u>**5.every**</u>

语法：arr.every(function(item,i){

Return item>8

})

含义：判断数组中的所有内容是否都满足条件，是则为true，但凡有一个不满足，则为false.

返回值：true/false

## 二、严格模式

1、 使用"use strict"定义严格模式
2、 严格模式可以定义在函数的最顶端或程序的最顶端

3、 在严格模式下 在变量a 没有声明时 a = 10 ; 这样的赋值会报错，定义两个相同名称的函数参数也会报错

4、 严格模式执行效率更高

## 三、this的指向

关于this：只与函数调用方式相关，与声明方式无关

### 1、全局定义的函数调用时，this就是window

		function fn(){
			console.log(this);//window
		}
	
		fn();

### 2、对象内部的方法调用函数时，this就是对象

		var obj = {
			name:'wyt',
			age:'18',
			say:function(){
				console.log(this)
			}
		}
		console.log(obj.say())

### 3.事件中函数时，this是事件源

写法一：
		`odiv.onclick = function(){`
  		`consoloe.log(this);`
	`}`

写法二：
`odiv.onclick = fn;`
`function fn(){`
   `consoloe.log(this);`
`}`

写法三：
`<button onclick = "fn(this)">点我</button>`

`function fn(a){`
   `console.log(a);//`
`}`

### 4.定时器内部的this

`setTimeOut(function(){`
 `consoloe.log(this);//事件源window`
`},10000)`
`setInterval(function(){`
 `consoloe.log(this);//事件源window`
`},10000)`

### 5.自调用函数中，this是window

`(function(){
  consoloe.log(this);//window
})()`

## 四、call()、bind()、apply()改变this指向

### 1、 call()把this的指向改变成obj

​	 语法： 函数名.call(要改变的 this 指向，要给函数传递的参数1，要给函数传递的参数2， ...)

​	 注意： 

​			会立即执行函数

​			第一个参数是你要改变的函数内部的 this 指向

​			第二个参数开始，依次是向函数传递参数

		   function fn(x,y){
	       console.log(x);
	       console.log(y);
	       console.log(this.age);
	   }
	
	   var obj = {
	       age: '18'
	   }
	
	   fn(1,2); // 输出的结果是1 2 undefined 原因是fn函数是全局函数，全局函数的 this指向window


​	   
​	   需求：想将fn内部的this指向obj,这样的话，就可以使用this.age访问到18
​	    call：
​	     作用：改变this指向的
​	     语法：函数名.call(obj,参数1,参数2...)
​	     注意：1. 会调用函数
​	           2. fn中this指向改变成obj
​	
	     fn.call(obj,1,2);// 输出的结果是1 2 18

## 2.apply():把this的指向改变成obj

语法：函数名.call(this的指向改成谁,[正常传参])

注意：fn内部的this已经 改变了，改变成obj

​			调用函数
​			this指向改变了
写法一：

    function fn(x,y){
    		console.log(x,y,this.age);
    	}
    	var obj = {
    			age:18
    	}
    fn.apply(obj,[10,20])

写法二

	var arr = [10,20]
	fn.apply(obj,arr)

###  3、bind()

​	 语法： var newFn = 函数名.bind(要改变的 this 指向，要给函数传递的参数1，要给函数传递的参数2， ...); newFn(传递参数)

​	 返回值：返回一个已经改变了 this 指向的函数


	    function fn(x,y){
	        console.log(x);
	        console.log(y);
	        console.log(this.age);
	    }
	    var obj = {
	        age: '18'
	    }
	
	    fn(1,2); // 输出的结果是1 2 undefined 原因是fn函数是全局函数，全局函数的 this指向window
	
	    bind():
	    作用：改变this指向的
	    语法：函数名.bind(obj,参数1,参数2...)
	    注意
	         1. 函数返回一个已经改变了this指向的函数
	         2. fn中this指向改变成obj
	
	    var newfn = fn.bind(obj, 1, 2)
	    newfn();