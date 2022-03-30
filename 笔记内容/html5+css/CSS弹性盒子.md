# 弹性盒子

## 怪异盒子(IE盒子)

### Box-sizing:border-box;

padding，border不撑大盒子，而是把内容区减小，不需要手动调整已经预设好的盒子大小，预设的width大小为盒子总宽大小。

## 标准盒子（W3C官方盒子）

### Box-sizing:content-box;

padding，border会撑大盒子，预设的width大小仅限内容区大小。

## 弹性盒子：用来控制子元素的布局方式。

### 1.a：容器==父元素（放盒子的元素）

### 	b：项目==子元素（所有放在弹性盒子里的元素）

### 2.形成弹性盒子的语句：在父元素上写display:flex;

### 3.特点：

##### 1）项目默认横向显示。

##### 2）当项目总宽度大于容器，不会超出或换行排列，而是挤压项目的宽。

##### 3）当容器成为弹性盒子之后，所有项目都可以直接设置宽高度。

##### 4）margin:auto;可以横纵都能生效。

### 4.设置主轴方向：项目都是默认沿着主轴排列

##### 默认横向排列，主轴为X轴。

##### 1）flex-direction:row（X）；column(Y);row-reverse(X轴反向排列)；column-reverse(Y轴反向排列)

### 5.项目在主轴的排列方式（对齐方式）

##### 1）justify-content:flex-start(从起点开始排列);

##### 									flex-end(从终点开始排列);

##### 									center(从中间开始排列);

##### 									space-between(两端对齐);	

##### 									space-around(自动分配项目左右间距，项目间的距离是靠边距离的double);	

##### 									space-evenly(自动分配剩余空间，每个间距都是一样的);					

### 6.项目在侧轴的排列方式（对齐方式）

##### 1）align-items:

##### flex-start(从起点开始排列);

##### 									flex-end(从终点开始排列);

##### 									center(从中间开始排列);

##### 									space-between(两端对齐);	

##### 									space-around(自动分配项目左右间距，项目间的距离是靠边距离的double);	

##### 									space-evenly(自动分配剩余空间，每个间距都是一样的);

##### 									<u>streth(拉伸，在不设置该方向的值时，默认效果为拉伸);</u>	

##### 									baseline(基线，跟flex:start;等效果);	

### 7.控制项目自动换行

##### flex-wrap:no-wrap

##### 					wrap

##### 					wrap-reverse:反向换行

### 8.多行项目对齐方式（同侧轴排列方式）

##### align-content:flex-start(从侧轴起点开始排列);

##### 									flex-end(从侧轴终点开始排列);

##### 									center(从侧轴中间开始排列);

##### 									space-between(两侧轴端对齐);	

##### 									space-around(侧轴自动分配项目左右间距，项目间的距离是靠边距离的double);	

##### 									space-evenly(侧轴自动分配剩余空间，每个间距都是一样的);					

##### 									<u>streth(拉伸，在不设置该方向的值时，默认效果为拉伸);</u>	


<hr>
## 添加在项目上的属性：

##### 1）align-self:(自己在侧轴上位置)

##### flex-start(从起点开始排列);

##### 									flex-end(从终点开始排列);

##### 									center(从中间开始排列);

##### 									space-between(两端对齐);	

##### 									space-around(自动分配项目左右间距，项目间的距离是靠边距离的double);

##### 									space-evenly(自动分配剩余空间，每个间距都是一样的);

##### 									<u>streth(拉伸，在不设置该方向的值时，默认效果为拉伸);</u>

##### 									baseline(基线， 跟flex:start;等效果);

##### 2）order:(控制项目的排列顺序，一般不建议调整)

##### <u>后面加值，类似于z-index，但默认值均为0</u>

##### 3）<u>flex:用于一组的项目进行总大小剩余空间分配</u>

##### 后加数字，为所标注参与划分的所占份数。

##### 4）flex-shrink:控制元素是否挤压;

##### 

