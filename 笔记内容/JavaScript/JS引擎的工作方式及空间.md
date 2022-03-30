# JS引擎的工作方式及栈、堆空间

## 1.栈、堆空间

### 1.1栈和堆

栈(stack)会自动分配内存空间，会自动释放。堆(heap)动态分配的内存，大小不定也不会自动释放。

### 1.2基本类型和引用类型

基本类型：简单的数据段，存放在栈内存中，占据固定大小的空间。

​	基本类型包括：number string undefined null boolean

[引用类型](https://www.zhihu.com/search?q=引用类型&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A"142681436"})：指那些可能由多个值构成的对象，保存在堆内存中,包含引用类型的变量实际上保存的不是变量本身，二十指向该对象的指针。

​	引用数据类型：object array

### 1.3 [传值](https://www.zhihu.com/search?q=传值&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A"142681436"})和传址

从一个向另一个变量复制引用类型的值，复制的其实是指针，因此两个变量最终指向同一个对象。即复制的是栈中的地址而不是堆中的对象。

从一个变量复向另一个变量复制基本类型的值，会创建这个值的副本。

## 2.JS引擎的工作方式

JS引擎是一个可以编译和解释我们JS代码的强大组件。JS在执行前，引擎用几微妙就可以编译代码。这种功能被称为及时编译（JIT）。

JS引擎：

​	V8：由 Google Chrome 和 Node.j s使用

​	SpiderMonkey ：用于Firefox

​	JavaScriptCore：Safari/WebKit使用

## JS引擎和全局内存（Global Memory）

本片重点为执行阶段：

	var num = 2;
	function pow(num) {
		return num * num;
	}

问：浏览器如何执行上述代码？

答：浏览器读取代码，然后浏览器执行代码。

​	上述的回答应该是大部分人的回答，但其实，读取这段代码的不是浏览器，而是JS引擎。一旦遇到了第一行，就会将几个声明放入全局内存，也就是 global memory。

​	**全局内存（也成为堆）**是JS引擎保存变量和函数声明的地方。所以在接触到上述代码时，全局代码发生如下变化。	（增加了两个声明）

![clipboard.png](https://segmentfault.com/img/bVbsKg5?w=650&h=325)

即使示例只有变量和函数，也要考虑你的JS代码在更大的环境中运行：在浏览器中或在Node.js中。 在这些环境中，有许多预定义的函数和变量，称为**全局变量**。 全球记忆将比num和pow更多。

上例中，没有执行任何操作，但是如果我们像这样运行函数会怎么样呢：

	var num = 2;
	function pow(num) {
	return num * num;
	}
		pow(num);

现在事情变得有趣了。当函数被调用时，JavaScript引擎会为**全局执行上下文**和**调用栈**腾出空间。

但调用堆栈是一个堆栈数据结构：这意味着元素可以从顶部进入，但如果它们上面有一些元素，它们就不能离开，JS 函数就是这样的。

一旦执行，如果其他函数仍然被阻塞，它们就不能离开调用堆栈。请注意，这个有助于你理解“JavaScript是单线程的”这句话。

回到我们的例子，当函数被调用时，JS引擎将该函数推入调用堆栈

![clipboard.png](https://segmentfault.com/img/bVbsKg6?w=650&h=325)

同时，JS 引擎还分配了一个**全局执行上下文**，这是运行JS代码的全局环境，如下所示

![clipboard.png](https://segmentfault.com/img/bVbsKg7?w=650&h=325)

想象全局执行上下文是一个海洋，其中全局函数像鱼一样游动，多美好！ 但现实远非那么简单， 如果我函数有一些嵌套变量或一个或多个内部函数怎么办？

即使是像下面这样的简单变化，JS引擎也会创建一个**本地执行上下文**:
