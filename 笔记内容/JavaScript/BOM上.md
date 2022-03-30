

#  BOM（Browser Object Model):浏览器对象模型

## BOM

- 其实是就是操作浏览器的一些能力

- 其实我们可以操作的内容如下：

  - 获得一些浏览器相关信息（窗口的大小）
  - 操作浏览器进行页面跳转
  - 获取当前浏览器地址栏的信息
  - 操作浏览器的滚动条
  - 浏览器的信息（浏览器的版本）
  - 让浏览器出现弹出框（alert/confirm/prompt)

- BOM的核心就是window对象
- window是浏览器内置的一个对象，里面包含着操作浏览器的方法

### 获取浏览器窗口的尺寸

- `innerHeight`和  `innerWidth`

- 这两个方法分别是用来获取浏览器窗口的高度和宽度（包含滚动挑的）

		var windowHeight = window.innerHeight
		console.log(windowHeight)
		
		var windowWidth = window.innerWidth
		console.log(windowWidth)

![image-20211210142235770](/Users/wyt/Library/Application Support/typora-user-images/image-20211210142235770.png)

### 浏览器的弹出层

- `alert`是在浏览器弹出一个提示框

			window.alert('我是一个提示框')
	
	![image-20211210142404891](/Users/wyt/Library/Application Support/typora-user-images/image-20211210142404891.png)

- `confirm`是在浏览器弹出一个询问框

		window.confirm('你确定吗')

![image-20211210142603535](/Users/wyt/Library/Application Support/typora-user-images/image-20211210142603535.png)

- 询问框一般情况会有一个自己设定的询问内容和两个按钮
- 当你点击确定的时候，返回值为true
- 当你点击取消的时候，返回值为false



- `prompt`是在浏览器弹出一个输入框

		var str = window.prompt('请输入内容')
		console.log(str)

![image-20211210142851608](/Users/wyt/Library/Application Support/typora-user-images/image-20211210142851608.png)

- 输入框一般会有一个自定的提示信息和一个输入框及两个按钮
- 点击取消是，返回null
- 输入内容并点击确定时，得到了你的输入内容

### 

### 浏览器的地址信息

- 在window中有个一对象叫做`location`
- 用于收集储存浏览器的地址栏内部信息

#### location.href

- `location.href`这个属性是浏览器的地址栏中的地址信息

- `location.href` 这个属性可以赋值

		window.location.href='https://www.baidu.com/'

- 书写了之后，会直接跳转

#### location.reload

- `Loocation.reload()`这个方法会重新加载页面，相当于刷新

		window.location.reload()
	
	- 注！：不要写在全局，不然浏览器就会一直处于刷新装填
	
	

## 浏览器的历史记录

- window中有一个对象叫history
- 用于收集储存历史记录信息

#### history.back

- History.back是用来回退历史记录，回到上一个页面，相当于浏览器上的后退按钮

		window.history.back()
	
	- 前提是我们有一个上一级页面

#### History.forword

- History.forword是渠道下一个历史记录，也就是渠道下一个页面，相当于前进键

		window.history.forword()
	
	- 前提是我们进行过回退操作，不然历史记录没有下一个页面

#### History.go(num)

- num=0  刷新
- num=1 向前进一个页面
- num=-1向后退一个页面

## 定时器

- 在js中，有两种定时器，倒计时定时器和间隔定时器

### 倒计时定时器

- 倒计时多少时间以后执行函数

- 语法：setTimeout(需要执行的函数，多长时间以后执行)时间的单位是毫秒，1s=1000ms

- 会在设定好的时间之后，执行函数

		var timerId1 = setTimeout(function(){
			console.log('执行！')
		}，1000)
		console.log(timerId)//1（此处显示的是返回值）
	
	- 只会执行一次，将不再执行
	- 返回值是，当前定时器是页面中的第几个计时器

#### 间隔定时器

- 每间隔多长时间就进行一次函数

- 语法：`setInterval(要执行的函数,时间)`
	
		var timerId2 = setInterval (function(){
			console.log('我十秒钟执行一次')
		}，10000)
		console.log(timerId)//2 此处为返回值，因前面有一个所以是2
	
	- 此处每隔10秒执行一次
	- 只要不关闭会一直执行
	- 返回值同样是计时器的计数

#### 定时器的返回值

- 设置定时器的时候，他的返回值是不分`setTimeout`和`setInterval`的
- 只要有个一定时器，那么就多一个数



#### 关闭定时器

- 前面我们给定时器命名的时候，就是在标记这是第几个定时器

- 我们有两个方式来关闭定时器 `clearTimeout`和`clearInterval`

		var timerId = setTimeout(function () { 
		console.log('倒计时定时器') 
		}, 1000) 
		clearTimeout(timerId)
	
	- 关闭定时器之后，将不再执行
	
	
		var timerId2 = setInterval(function () { 
		console.log('间隔定时器') 
		}, 1000)
		clearInterval(timerId2)

- 原则上，
  - `clearInterval`关闭`setInterval`
  - `cliearTimeout`关闭`setTimeout`

- 但其实可以通用