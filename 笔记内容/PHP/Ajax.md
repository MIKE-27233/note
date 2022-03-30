# Ajax

## 1.Ajax的概念

AJAX（Asynchronous Javascript And XML）是异步的javascript和XML

传统网站中，如果需要更新页面内容，必须重载整个网页页面。

ajax是可以在不刷新加载整个页面的情况下，对网页的某部分进行更新。

## 2.同步交互和异步交互

同步交互：客户端向服务器端发送请求，必须等到结果返回，才能进行其他的业务操作![image.png](https://cdn.nlark.com/yuque/0/2021/png/707513/1640618000784-957bfbb3-89ad-4093-92ce-968074a26e60.png?x-oss-process=image%2Fresize%2Cw_808%2Climit_0)

异步交互：客户端向服务器端发送请求，不必等到结果返回，就可以进行其他的业务操作。![image.png](https://cdn.nlark.com/yuque/0/2021/png/707513/1640617974734-88652fe1-6c3c-4808-a3ea-b3b7b4786c0a.png?x-oss-process=image%2Fresize%2Cw_986%2Climit_0)

### 3.Ajax的核心对象

### 3.1Ajax的核心对象是XMLHttpRequest

即AJAX的异步操作，和服务器交互主要依赖该对象。![image.png](https://cdn.nlark.com/yuque/0/2021/png/707513/1640621045041-6194a0ee-e193-482a-9fc6-19d24236655a.png?x-oss-process=image%2Fresize%2Cw_1166%2Climit_0)

以前浏览器负责显示页面和发送请求接收响应(和后端交互)。两件事情同一时刻只能做件，没法同时进行。这样会让用户感觉不好(友好性不好)，比如:当浏览器发送请求时，就没法显示内容，这时浏览器中是空白显示，给用户的感觉不好。

   现代浏览器，使用XMLHttpRequest对象，可以把浏览器解脱出来，可以让浏览器只负责显示，而完成请求的事情由XMLHttpRequest对象负责。这样两者各负其责，效率更高，效果更好，用户体验很好，用户永远不会看到浏览器空白。

### 3.2XMLHttpRequest是一个对象

其中的属性与如下几点

| **属性名**             | **备注**                                  |
| ---------------------- | ----------------------------------------- |
| **onreadystatechange** | 当每次状态改变所触发事件处理程序（会4次） |
| **readyState**         | 请求状态码。                              |
| **responseText**       | 从服务器端返回的数据的字符串形式          |
| **status**             | 请求的响应状态。404(未找到) 200(就绪)     |

		在客户端与服务器的通信过程中，
		XMLHttpRequest.readyState 体现着当前请求以及服务端响应的状态。
		它的值有
		0：初始化，XMLHttpRequest对象还没有完成初始化
		1：载入，XMLHttpRequest对象开始发送请求
		2：载入完成，XMLHttpRequest对象的请求发送完成
		3：解析，XMLHttpRequest对象开始读取服务器的响应
		4：完成，XMLHttpRequest对象读取服务器响应结束
		xhr.readyState属性值是0、1、2、3、4。其中状态4代表响应完成。
		-----------------------------------------------------------------------
		服务器响应完成之后，我们通常会使用 XMLHttpRequest.status代表响应中的数字状态码。
		代表着我们的 Ajax 请求的状态成功与否。
		
		200 服务器已经成功处理了请求并响应到网页
		404 请求失败，请求所希望得到的资源未被在服务器上发现（一般都是请求路径的错误）
		500 服务器遇到错误，无法完成请求

### ###3.3编写Ajax的步骤

#### 3.3.1创建对象   创建XMLHttpRequest对象
		let xht = new XMLHttpRequest

#### 3.3.2设置请求参数

	xhr.open('请求方式',‘请求路径','是否异步')
	xhr.open('method','url','async')
						method:代表HTTP请求的方法名，比如 get post
						url: 代表想要发送请求的路径
						async：代表是否异步，默认为异步

#### 3.3.3发送请求
	xhr.send()

#### 3.3.5接受响应
	xhr.onreadystatechange = function(){
		if(xhr.onreadystate == 4 && xhr.status == 200){
			xhr.responseText 响应回的数据
		}
	}