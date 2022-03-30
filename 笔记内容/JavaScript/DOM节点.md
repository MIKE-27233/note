# DOM节点

### 节点：w3c：页面上的所有内容都可以成为节点，DOM的最小单元就是节点

- 主要分类	
  - 标签：元素节点；	nodeType		1
  - 属性：属性节点；	nodeType		2    
  - 文本：文本节点；	nodeType		3  
  - 注释：注释节点；	nodeType		8
  - 文档：文档节点；	nodeType		9

- 如何获取节点：通过节点之间关系来获取
  - 父节点.firstChild
  - 节点.nextSibling
  - 节点.previousSibling 节点的上一个兄弟节点
  - 父节点.lastChild:  父节点的最后一个子节点
  - 节点.parentNode: 节点的父节点
  - 父节点.childNodes: 获取所有的子节点（伪数组）
- 获取元素节点：
  - 父节点.firstElementChild: 获取父元素的第一个元素节点
  - 节点.nextElementSibling:  节点的下一个兄弟元素节点
  - 节点.previousElementSibling:  节点的上一个兄弟元素节点
  - 父节点.lastElementChild:  父节点的最后一个子元素节点
  - 节点.parentElement: 节点的父元素节点（兼容性不好，不用它）
  - 父节点.children: 获取所有的子元素节点（伪数组)

### 节点的共有属性：

- 节点.nodeType:

​            元素节点  1  (**)

​            属性节点  2

​            文本节点  3

​            注释节点  8

​            文档节点  9

- 节点.nodeName

​            元素节点的nodeName值都是大写的标签名

- 节点.nodeValue

### 节点的操作：

- 创建节点：

  ​           语法：document.createElemet('标签名')

  ​           返回值：创建好的元素节点

- 追加节点：

  ​           语法：父节点.appendChild(子节点)

  ​           含义：将子节点追加到父节点的尾部

  ​           例子：document.body.appendChild(子节点)

- 插入节点

  ​           语法：父节点.insertBefore(子节点, 谁的前面的谁)

  ​           含义:将子节点插入到父节点的指定位置

  ​           例子：oBox.insertBefore(oBtn,oBox.firstChild); 将button插入到oBox的头部

- 替换节点

  ​           语法：父节点.replaceChild(新节点,旧节点(位置))  不常用

- 删除节点：

  ​           语法：父节点.removeChild(子节点)

  ​                 节点.remove()    最常用

- 克隆节点

  ​           语法：节点.cloneNode(true/false)

  ​           作用：克隆出来一个节点

  ​                  true:代表克隆元素本身和元素的子元素以及后代

  ​                  false:代表克隆元素本身