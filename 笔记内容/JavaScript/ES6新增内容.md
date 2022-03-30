# ES6新增内容

## 1、let和const关键字

###     **1.1.let用来声明变量,它的用法类似于var，但是所声明的变量，只在let命令所在的代码块内有效,类似于C，C++,JAVA局部变量的概念。**

   let/const和var的区别：

​	   1. 预解析：var会进行预解析，let/const不会，所以不会产生全局变量污染

​	   2. 变量重名：var定义变量可以重名，let/const不允许在同一个作用域下，定义重名变量

​	   3. 块级作用域：var没有块级作用域，let/const有

	1. 预解析：var会进行预解析，let/const不会
	var命令会发生"变量提升"现象,也就是预解析，即变量可以在声明之前使用，值为undefined。
	这种现象多多少少是有些奇怪的，按照一般的逻辑，变量应该在声明语句之后才可以使用。
	// var 的情况
	console.log(foo);// 输出undefined
	var foo = 2;
	
	// let 的情况
	console.log(bar);// 报错   ReferenceError
	let bar = 2;
	也就意味着被let声明的变量，必须先定义在使用。
	
	2. 变量重名：var定义变量可以重名，let/const不允许在同一个作用域下，定义重名变量
	var a = 123;
	var a = 123; //可以实现
	
	let b = 123;
	let b = 123; //Identifier 'a'has already been declared
	3.块级作用域：var没有块级作用域，let/const有
	{
	   var a = 10;
	   let b = 123;
	}
	console.log(a);
	console.log(b)
	上面代码在代码块之中，
	分别用let和var声明了两个变量。然后在代码块之外调用这两个变量，结果let声明的变量无法被打印，
	var声明的变量返回了正确的值。这表明，let声明的变量只在它所在的代码块有效。
	
	再如：
	for(let i=0; i<10; i++){
	   document.write(i);
	}
	document.write(i)；
	//x 看不到
	上面代码中，计数器i只在for循环体内有效，在循环体外引用就会报错。

### 1.2.let和const的区别：

	   1. 声明时赋值 
	   1. 值的修改：const不支持值得修改，定义了就是常量，必须在声明时赋值。


 	const PI = 3.1415926;// PI是常量，永远不变的量
 	let a = 10;
 	a = 20;
 	console.log(a);
 	PI = 19;
 	console.log(PI);//报错

## 2.箭头函数

### 2.1定义函数

​	function fn ( ){}

​	var fn = function () {}

​	(Function(){})()     自调用函数

### 2.2箭头函数的语法

实际上是赋值式的一种变态

		var fn = function(){}
		var fn = ()=>{}

注意：

2.2.1当你的形参只有一个的时候, 可以不写小括号

	var fn = (a)=>{console.log(a)}
	var fn = a = > {console.log(a)}

2.2.2当函数体只有一行代码时，大括号可以不写

	var fn = (a) => {console.log(a)} 
	--因为只有一个形参所以成为
	var fn = a =>{console.log(a)}
	--因为只有一行代码所以成为
	var fn = a => console.log(a)

2.2.3当函数体只有一行代码时，return可以不写

	var fn = (x,y) => {return(x+y)}
	因为只有一行代码所以成为
	var fn = (x,y) => x+y

2.2.4箭头函数内没有this，this指向上下文环境

## 3、解构赋值

### 3.1 解构赋值 快速从对象或者数组中获取一些数据，分为解构数组和解构对象

​	       解构数组 语法: var [ 变量1, 变量2, 变量3, ... ] = 数组

​	       解构对象 语法: var { 键名1, 键名2, 键名3, ... } = 对象

​		           解构对象的时候起一个别名

3.1.1对于数组


	var arr = [12,43,32,3,32];
	// console.log(arr[0],arr[1],arr[2],arr[3]);
	// 解构赋值的语法：var [a,b,c,d,e]  = arr;
	// 作用：相当于a,b,c,d,e分别存储的是12,43,32,3,32
	var [a,b,c,d,e]  = arr;
	console.log(a,b,c,d,e);

3.1.2对于对象

	var obj = {name:"zhangsan",age:"18",sex:"男"}
	// console.log(obj.name,obj.age,obj.sex);
	// console.log(obj['name'],obj['age'],obj['sex']);
	
	// for(let k in obj){
	//     console.log(obj[k]);//只能使用[]语法，因为[]语法是支持变量的
	// }
	// 解构赋值的语法：let {name,age,sex} = obj;
	
	let {name,age,sex} = obj;
	console.log(name,age,sex);

### 3.2结构数组的用途

	解构赋值的用途：
	用途一：解构赋值可以让一个函数返回多个值使用 []
	function fn(){
	    return [1,2,3];
	}
	let a = fun();let [x,y,z] = fun();
	console.log(a);
	console.log(x,y,z);


​	
​	案例：
​	返回1~100能被3整除的数之和，以及这样的数有多少个。
​	function is3(){
​	    let sum = 0;
​	    let count = 0;
​	    for(let i=1; i<=100; i++){
​	        if(i%3==0){
​	            sum += i;
​	          count++;
​	        }
​	    }
​	    return [sum,count];
​	}
​	let [sum,count] = is3();
​	console.log(sum,count);
​	
​	用途二：
​	解构赋值可以实现两个数的交换
​	let a=10,b=20;
​	[a,b] = [b,a];
​	console.log(a,b);

### 4、默认参数

​       4.1 概念：给函数的形参设置一个默认值, 当你没有传递实参的时候, 默认参数会生效
​	       语法：function fn(a = 10, b = 20) { }  参数a的默认值是10

	// 将函数的形参位置设置一个默认参数，该默认参数在没有传递实参时生效
	
	function fn(a=10,b=20){
	    console.log(a,b);
	}
	 
	fn();//此时会输出默认参数
	
	fn(1,2)此时会覆盖默认参数

###    5、扩展运算符

​       5.1     概念：展开合并运算符,主要是操作 数组 和 对象 的运算符号（...）

​	          作用：展开、合并

​		   展开：可以展开对象或者展开数组

	var arr = [21, 34, 54, 2, 5]
	console.log(arr);//(5) [21, 34, 54, 2, 5]
	console.log(...arr);//把数组的元素一个一个的展开开来
	
	// 合并
	function fun(...arr){
	    console.log(arr);//将传递的形参合并成一个数组
	}
	
	fun(1,2,3,4,5)	

###  6、Set和map集合

​       Set：数据结构，类似于数组，但是它的值不会重复（自动去重）

​	   Set的属性和方法

​	   属性：size获取元素的长度

​	   方法：add(ele) 向Set中添加元素

​             delete(ele)  删除

​             has(ele)  是否包含某个元素，返回布尔值

​             clear()： 清空set集合


	Set集合特点自动去重实现数组去重 ：
		let arr =[2,3,4,2,3,4,2,3,4];
		let set = new Set(arr);
		let arr = Array.from(set);//Number("123");
		console.log(arr);

map也是一种数据结构，类似于对象

​	   属性：size获取元素的长度

​	   方法： 

​	         设置键值对 set(key,value)

​               获取       get(key)

​               删除       delete(key)

​               清空       clear()

​               包含       has(key)    返回布尔值

	<script>
	    // map的遍历:
	    let map = new Map();
	    map.set("1", "校长"); 
	    map.set("2", "小明"); 
	    map.set("3", "老王");//map.delete("3");map.clear();
	    console.log(map.has("0"));
	    console.log(map.get("2"));
	    console.log(map);
	    for (let t of map) {
	        console.log(t[0] + t[1]); //0代表Key 1代表value
	    }
	map的遍历:
	for(let t of map){
	    console.log(t[0] + t[1]); //0代表Key 1代表value
	}
	</script>

for..of循环，

	  for..of和for..in的小小总结：
	    for..in：ES5提出  for..ofES6
	    数组：for.in循环可以遍历数组，遍历的是下标（字符串类型），for.of可以遍历数组，遍历的是值
	    对象：for..in循环遍历对象,for..of不可以遍历对象
	    map集合：for..of可以遍历map集合，for..in不能遍历map集合