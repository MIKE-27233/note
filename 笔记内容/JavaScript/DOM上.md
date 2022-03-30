# DOM（Document Object Model):文档对象模型

## DOM

- 其实就是操作html中标签的一些能力
- 可以操作的元素如下：
  - 获取一个元素
  - 移出一个元素
  - 创建一个元素
  - 向页面李添加一个元素
  - 给元素绑定一些事件
  - 获取元素的属性
  - 给元素添加一些CSS样式
  - ...
- DOM的核心就是document对象
- document对象是浏览器内置的一个对象
- DOM：页面中的标签，我们通过js获取到以后，就把这个对象叫做DOM对象

### 获取一个元素

- 通过js代码来获取页面内的标签
- 获取到以后我们就可以操作这些标签了

### getElementById

- `getElementById`是通过标签的id名称来获取标签的

- 因为在一个页面中id是惟一的，所以获取到的就是一个元素
	
		<body> 
			<div id="box"></div>
			<script>
				var box = document.getElementById('box') 
				console.log(box) // <div></div> 
			</script> 
		</body>
	
	- 如上代码就成功获取了id为box的div

### getElementsByClassName

- `getElementsByClassName`是通过标签名的类名来获取标签

- 因为class类名可以重复使用，所以获取到了一组元素

- 哪怕class只有一个，那也是一组元素，只不过这一组中只有一个DOM

		<body>
			<div calss="box"></div>
			<script>
				var box = document.getElementsByClassName('box') 
				console.log(box) // [<div></div>] 
				console.log(box[0]) // <div></div>
			</script>
		</body>
	
	- 获取到的是一组元素，长得和数组的结构一样，但不是数组，是伪数组
	- 这个数组也是按照索引排列的，所以我们想要准确的拿到这个div，需要用索引来获取，索引的方法与数组相同

### getElementsByTagName

- `getElementByTagName`是通过标签的标签名来获取标签

- 所以也会获取到一组元素

- 如果只有一个同种标签，也是一组元素，不过其中只有一个DOM元素而已

		<body> 
			<div></div>
			<script>
				var box = document.getElementsByTagName('div') 
				console.log(box) // [<div></div>]
				console.log(box[0]) // <div></div> 
			</script>
		</body>
	
	- 和通过类名获取一样，获取到的是一个张的很像数组的元素组
	- 通过索引可以获取准确的DOM元素

### querySelector

- `querySelector`是按照选择器的方法来获取元素组
- 这个方法只能获取第一个满足条件的元素

		console.log(document.querySelector('div')) // 获取页面中的第一个 div 元素 		
		console.log(docuemnt.querySelector('.box')) // 获取页面中第一个有 box 类名的元素 
		console.log(document.querySelector('#box')) // 获取页面中第一个 id 名为 box 的元 素

### querySelectorAll

- `quertSelectorAll`是按照选择器的方式获取元素

- 唯一不同的是这个方式会获取全部的满足条件的元素，并以一个伪数组的形式返回

		console.log(document.querySelectorAll('div')) // 获取页面中的所有的 div 元素
		console.log(docuemnt.querySelectorAll('.box')) // 获取页面中所有有 box 类名的元素
	
	- 可以通过类似于数组的索引方式来精确到每一个DOM元素

### Document.body获取body

### Document.documentElement，获取html

### Document.title获取title

### document.head获取head

## 操作属性

- 通过我们获取到的元素，操作DOM元素的属性来更改页面上的效果

### innerHTML

- 获取元素内部的HTML结构

		<body> 
		<div> 
		<p>
			<span>hello</span> 
			</p> 
		</div> 
		<script> 
			var div = document.querySelector('div') 
			console.log(div.innerHTML) /* <p><span>hello</span> </p>*/ 
		</script> 
		</body>

- 设置元素的内容

		<body> 
			<div></div> 
			<script> 
				var div = document.querySelector('div') 
				div.innerHTML = '<p>hello</p>' 
			</script> 
		</body>
	
	- 设置完成之后，div里面会加入一个P元素

### innerTEXT

- 获取元素内部的文本（只能获取到文本内容，获取不到HTML标签）

		<body> 
			<div> 
				<p>
					<span>hello</span> 
				</p> 
			</div> 
			<script> 
				var div = document.querySelector('div') 
				console.log(div.innerText) // hello 
			</script> 
		</body>

- 可以设置元素内部的文本

		<body> 
			<div></div> 
			<script> 
				var div = document.querySelector('div') 
				div.innerText = '<p>hello</p>' 
			</script> 
		</body>
	
	- 为div里面增加了<p>hello</p>文本，而不是增加P标签

### getAttribute

- 获取元素的某个属性（包括自定义属性）

		<body> 
			<div a="100" class="box"></div> 
			<script> 
				var div = document.querySelector('div') 				
				console.log(div.getAttribute('a')) // 100 
				console.log(div.getAttribute('class')) // box 
			</script> 
		</body>

### setAttribute

- 给元素设置一个属性（包括自定义属性）

		<body> 
			<div></div> 
		<script> 
			var div = document.querySelector('div') 
			div.setAttribute('a', 100) 
			div.setAttribute('class', 'box') 
			console.log(div) // <div a="100" class="box"></div> 
		</script> 
		</body>

### style

- 专门用来给元素增加css样式
- 添加的都是行内样式

### className

- 专门用来操作类名（获取类名）

		<body> 
			<div class="box"></div> 
		<script> 
			var div = document.querySelector('div') 
			console.log(div.className) // box 
		</script> 
		</body>

- 也可以设置元素的类名，不过是全覆盖式的操作

		<body> 
			<div class="box"></div> 
		<script> 
			var div = document.querySelector('div') 
			div.className = 'test' console.log(div) // <div class="test"></div> 
		</script> 
		</body>
	
	- 在设置的时候，不管之前有没有类名，都会全部被设置的值覆盖

### classList

- classList.add('类名')：为元素增加一个类名
- classLlist.remove('类名')：为元素去掉类名
- classList.toggle('leiming '):切换类名

![image-20211210163507131](/Users/wyt/Library/Application Support/typora-user-images/image-20211210163507131.png)