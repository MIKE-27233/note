# day06

# 取消搜索框轮廓线：

outline：none

## 1.省略号（单行）

### 在宽度有限的区域内

### 分三步：

#### ①设置不换行：

whitespace：控制文本在盒子里的显示方式

​    normal：默认，换行且只空格只显示一个

​    pre:文本不换行且空格也显示（原文输出）

​    pre-wrap:文本换行显示空格

​    pre-line:文本换行不显示空格

​    nowrap：不换行

②设置溢出隐藏：

overflow

​    溢出：overflow：hidden隐藏

​         overflow：scroll滚动

​         overflow：auto自动

​         overflow：visible显示

​         inherit继承

​         overf-x:横轴

​         overflow-y:纵轴

③设置省略号

text-overflow:ellipsis;省略号

text-overflow：

## 2.命名规则

### a.起名字不用中文

### b.不使用数字开头

### c.特殊符号仅限_及$符号

### d.做到见名知意

### e.驼峰命名 首字母大写

# 单页建立：

## 1.命名 建文件

### css文件与首页相同

index.html

Index.css

## 2.6个清除

*{

​    padding: 0;

​    margin: 0;

}

ul,ol{

​    list-style: none;

}

a,u{

​    text-decoration: none;

}

i,em {

​    font-style: normal;

}

b,strong{

​    font-weight: normal;

}

h1,h2,h3,h4,h5,h6{

​    font-size: 0;

​    font-weight: normal;

}

## 3.PS设置及打开样图

### 1.调出标尺

### 2.信息框

### 3. 快捷键

# 4.通栏

## 做大板块时通栏一般不设置宽度，与浏览器保持同宽

# 5.版心

## 版心默认保持在浏览器中间ji





