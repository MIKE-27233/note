## Css: cascading style sheets(层叠样式表)

![image-20220116212834536](/Users/wyt/Library/Application Support/typora-user-images/image-20220116212834536.png)

### 属性选择器：

![image-20220116213508677](/Users/wyt/Library/Application Support/typora-user-images/image-20220116213508677.png)

关于字体

![image-20220116215231057](/Users/wyt/Library/Application Support/typora-user-images/image-20220116215231057.png)

![image-20220116220511419](/Users/wyt/Library/Application Support/typora-user-images/image-20220116220511419.png)

spacing：letter-spacing：字母之前的间距

Word-spacing :单词之间的间距

text- indent：首行缩进

![image-20220116221021767](/Users/wyt/Library/Application Support/typora-user-images/image-20220116221021767.png)

pre:保留

vh:1%屏幕高度

css动画的重点：transition

​							animation

@import：在css中引入另一个css文件

伪元素：添加dom节点，用于装饰

优雅降级：使用了新的特性，再写一个给低版本用的版本。

渐进增强：写了一个基础版本的东西，再给更高更好的设备进行增加内容



react和vue要组件化生效css，组织css的作用于是全局



关于继承：关于文字的大多可以继承

​					关于盒模型大多不能继承

​					inherit:继承父本，继承到父本的计算值，不是实际值。


	例：*{box-sizing:inherit;}
	Html{box-sizing:border-box;}
	.some-uneed{box-sizing:content-box;}

​					initial:初始值

## css求值过程

dom树--filtering(对应于到该页面的css中进行筛选看是否有声明值：会获得一个或多个值)--cascading(按照来源，！important、选择器特异性，书写顺序等等选出一个优先级很高的属性值：cascaded value,在层叠比赛中，获得胜利的值)---default(如果前一步没有值，则考虑默认值，此时肯定有一个值)--resolving(进行计算，将相对值进行计算等等：比如em转为px)--formatting(计算值进行转换：比如百分比的转换为px，此时得到使用值)--constraining(限制值：考虑各层级的限制:min-height之类或将像素值的小数转为整数)--实际值(最终生效的值)

​	

# 布局（layout）

### 确定页面内容的大小和位置的算法

### 根据元素、容器、兄弟节点和内容等信息来计算

## 布局相对技术

![image-20220116231837394](/Users/wyt/Library/Application Support/typora-user-images/image-20220116231837394.png)

### 盒模型

![image-20220116231910888](/Users/wyt/Library/Application Support/typora-user-images/image-20220116231910888.png)

padding：如果用百分比，则只针对于容器的宽度。



## IFC Inline Formatting Context(行级排版上下文)

创造条件：只内含行级元素的区域

## BFC Block Formatting Context(块级排版上下文)

创造条件：根元素

​					浮动、绝对定位、inline-block

​					flex子项和grid子项

​					overflow值不是visible

​					display:flow-root;

排版规则：

- 盒子从上到下摆放
- 垂直margin合并
- BFC内盒子的margin不会与外面的合并
- BFC不会和浮动元素重叠



## FLEX BOX

- 一种新的排版上下文
- 它可以控制子盒子的
  - 拜访的流向（上下左右）
  - 摆放顺序
  - 盒子的宽高
  - 水平和垂直方向的对齐
  - 是否允许换行

![image-20220117005459027](/Users/wyt/Library/Application Support/typora-user-images/image-20220117005459027.png)

![image-20220117005517564](/Users/wyt/Library/Application Support/typora-user-images/image-20220117005517564.png)

![image-20220117010103847](/Users/wyt/Library/Application Support/typora-user-images/image-20220117010103847.png)

![image-20220117010456464](/Users/wyt/Library/Application Support/typora-user-images/image-20220117010456464.png)



## Grid布局

![image-20220117010721936](/Users/wyt/Library/Application Support/typora-user-images/image-20220117010721936.png)

Display:grid;会使元素生成一个块级的Grid容器。

使用grid-template相关属性为元素划分网格。
