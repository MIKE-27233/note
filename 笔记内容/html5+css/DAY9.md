

# DAY9

## 1.锚点：实现在一个页面内实现不同位置的快速跳转

##    核心：利用超链接结合ID选择器实现

## 2.表格标签：table表格标签 caption 为表格标题标签 th为表头 tr为行 td为单元格

## 表格行分组标签：

thead

tbody：默认情况下，除caption外，全部属于tbody。（可以有多个，但是 thead和tfood只有有一个）

tfoot

## 表格标签列分组 colgroup：

前两列分为一组，span标记分组列数。

<colgroup span="2"></colgroup>

### caption 表格标题：默认居中

### th （table head）标签：默认加粗居中

###  通过table标签的属性进行调整样式

###  （全都可用于CSS中，其中cellspacing要改为 border-collapse:collapse 可以合并边框线    table-layout:fixed;固定单元格宽度，不让其岁内容分配宽度

###  empty-cells：show;显示空格子

###  Empty-cells:hide;隐藏空盒子)

width与heitht用于更改单元格的宽高
 border 加入边框
 align:用于调整表格的水平位置。
cellspacing 取消边框间距 一般写0
cellpadding:用于调整内容在单元格内的位置。一般也写0.

Rules:规定画哪种线，

行线：rows

竖线：cols

组线：groups,选择每个分组加边框。

### tr （table row）标签上的属性：

hight：
bgcolor:
align:用于调整表格的水平位置。
valing:用于调整垂直水平上的位置

### Td (tabledate）标签上的属性：

height：
width：本按照内容默认分配。
单元格合并问题
1.跨行合并：横线没有了就是跨行合并
	rowspan
2.跨列合并：竖线没有了就是跨列合并
	colspan

# 2/Form 表单标签

### Feildset:表单字段集 块级元素，默认有边框线，用于做表单分组。

Legend:可以让线处于文字中间高度，用于做表单分组的标题。

### <feildset>
	<legend>
	个人信息
	</legend>
</feildset>



## action用于描述服务器提交地址

## mathod: get获取 post 提交

### name属性：给表单起名字，一般写在table第一句话

## 表单控件：

### 	文本输入框：

### 	<input type="text">

### 密码输入框：

<input type="password">

### 清空输入框：
<input type="reset">

### 普通输入框：

<input type="button" value="按钮">

或使用 button标签

### 提交输入框：

<input type="submit">

### 单选框：需要起同样的name以编程一组按钮
性别：
男<input type="radio" name="sex">
女<input type="radio" name="sex">

### 多选框：需要起同样的name以编程一组按钮
爱好：
吃饭<input type="checkbox"  name="hobby">
睡觉<input type="checkbox"  name="hobby">

### 下拉菜单 select：需要起同样的name以编程一组按钮；默认选项需在option后加selected属性
<select name="city" id="">
        <option value="">北京</option>
        <option value="" selected>西安</option>
        <option value="">上海</option>
        <option value="">程度</option>
</select>


### 上传文件：
<input type="file">


### 多行文本输入框(文本域）：
<textarea name="" id="" cols="30" rows="10" style="resize:none">
</textarea>
需用CSS标签更改为 resize：none；以禁止用户更改大小

## 默认属性添加方式如下：

### 在属性中增加checked.

男<input type="radio" name="sex" checked>
女<input type="radio" name="sex">  

## 该属性禁用 disabled：

男<input type="radio" name="sex" disable>
女<input type="radio" name="sex">  



## Lable 优化用户体验 增大点击范围 需用ID名将选择按钮与文字相连:

性别：
    <label for="man">男</label><input  id="man" type="radio" name="sex" disabled>
    <label for="woman">女</label><input  id="woman" type="radio" name="sex"> 



## 隐藏域：有一些数据想要放到浏览器里面，不想给用户看到.

<input type="hidden">

## 图像域：

<input type="image" src="img/img01.png">



# DAY10

## #BFC:block format context.块级格式化上下文。

### 前提条件：只有块级元素才会涉及。

### BFC其实就是独立的渲染区域

## BFC布局规则：

### 	1.在BFC里面的盒子会在垂直方向上排列。

### 	2.盒子垂直方向上的距离由margin决定。

### 	3.每个元素margin的左侧，与包含块border左侧相接触。

### # 4.BFC也就是一个独立的容器，容器里的子元素布局不会影响到外面的元素。

### # 5.BFC的区域不会和浮动的元素发生重叠。（应用：双飞翼布局）

### # 6.计算BFC高度的时候，其中浮动元素也会参与计算（高度塌陷问题：子元素浮动，以至于父元素的高会受到影响）。

解决方式， 给父元素触发BFC.

### # 7.属于同一个BFC的两个盒子会发生外边缘重叠，外间距重叠。

#### 	同级关系，左右margin相融。

#### 	父子关系，给子元素加margin，父元素一同上下，此时要解决。：

##### 	1.给父元素激活BFC 使两者不属于同意BFC环境下。

##### 	2.给父元素添加上边框线 然后隐藏：transparent。

### *******BFC的触发规则：

### 	1.html就是一个BFC。

### 	2.加了浮动会触发BFC。

### 	3.定位为绝对定位和固定时。

### 	4.overflow:hidden/auto/scroll.

### 	5.display为：inline-block,flex,table-cell,table-coption,inline-flex.









