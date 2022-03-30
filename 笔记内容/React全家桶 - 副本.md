

# 全球新闻发布系统

## 1.项目前期准备

### 项目初始化

1 create-react-app 项目名 创建项目

2.在项目中删除没有的初始化文件  并且新建index.js（全局配置文件）与app.js

**index.js** 全局配置文件

````
import React from 'react'
import ReactDOM from 'react-dom'

import App from "./app.js"
ReactDOM.render(
	<App></App>,
	document.getElementById('root')
)
````

**app.js** 根组件

````jsx
let App=()=>{
    return (
        <>
            我是根组件
        </>
    )
}
export default App
````

**css模块化**

react中使用普通的css样式表会造成作用域的冲突，css定义的样式的作用域是全局，在Vue 中我们还可以使用scope来定义作用域，但是在react中并没有指令一说，所以只能另辟蹊径了。 所以我们可以使用css模块化来解决这个问题

在传统代码中如果有两个组件  并且有相同的类名   在渲染组件的时候样式就会被污染

### css模块化

1.创建xxx.module.css文件用来编写css （不要用标签选择器 尽量用class选择器）写入你的样式

```css
.demoh{
    color:yellow;
}
```

2.在组件中引用css  并且使用

```jsx
import React, { Component } from 'react'
// 1.引用
import style from "./demo.module.css"
export default class demo extends Component {
  render() {
    return (
      <>
      {/* 2.使用 */}
        <h2 className={style.demoh}>我是第一个组件</h2>
      </>
    )
  }
}

```

### 项目中使用scss与反向代理

#### scss 

如果在项目上面直接使用scss  (尝试修改css文件)

项目会报 如下错误

```
Compiled with problems:X

ERROR in ./src/demo.module.scss (./node_modules/_css-loader@6.7.1@css-loader/dist/cjs.js??ruleSet[1].rules[1].oneOf[8].use[1]!./node_modules/_postcss-loader@6.2.1@postcss-loader/dist/cjs.js??ruleSet[1].rules[1].oneOf[8].use[2]!./node_modules/_resolve-url-loader@4.0.0@resolve-url-loader/index.js??ruleSet[1].rules[1].oneOf[8].use[3]!./node_modules/_sass-loader@12.6.0@sass-loader/dist/cjs.js??ruleSet[1].rules[1].oneOf[8].use[4]!./src/demo.module.scss)

Module Error (from ./node_modules/_sass-loader@12.6.0@sass-loader/dist/cjs.js):
Cannot find module 'sass'
Require stack:
- C:\Users\54407\Desktop\react全家桶\myapp\node_modules\_sass-loader@12.6.0@sass-loader\dist\utils.js
- C:\Users\54407\Desktop\react全家桶\myapp\node_modules\_sass-loader@12.6.0@sass-loader\dist\index.js
- C:\Users\54407\Desktop\react全家桶\myapp\node_modules\_sass-loader@12.6.0@sass-loader\dist\cjs.js
- C:\Users\54407\Desktop\react全家桶\myapp\node_modules\_loader-runner@4.2.0@loader-
```



所以我们下载scss模块

cnpm install --save sass

即可在项目中安装sass

#### 反向代理

详见之前内容

## 2.路由

### 路由架构

在没有授权登录的时候不会进入到NewSandBox相关内容 会被重定向到/login   

<img src=".\img\1aa.png" alt="1aa" style="zoom:50%;" />

### 路由创建

1.下载路由 npm install --save react-router-dom@5

2.创建路由文件夹与容纳路由的文件(router文件夹与index.js路由文件)

3.设置路由 切记路由模式设置成Hash模式 Browser模式的话打包上线会有404(也可以打包项目时候修改 不形象项目开发)

4.设置路由模式

````jsx
import React, { Component } from 'react'
// 引用路由模式
import {HashRouter} from "react-router-dom"
export default class index extends Component {
  render() {
    return (
        // 设置路由模式
       <HashRouter>


       </HashRouter>
      
    )
  }
}

````

5.创建components 与 views 文件夹 并且创建登录页面 与 首页NewSandBox 路由页面与路由配置

6.设置基础页面权限

```jsx
import React, { Component } from 'react'
// 引用路由模式
import { HashRouter, Route, Redirect, Switch } from "react-router-dom"
import Login from "../views/login.jsx"
import NewSandBox from "../views/NewSandBox.jsx"
export default class index extends Component {
  render() {
    return (
      // 设置路由模式
      <HashRouter>
        <Switch>
          <Route path="/login" component={Login} />
          {/* 判断用户是否登陆过如果有那么就进入首页 否则 重定向到登录页面 */}
          {/* <Route path="/" render={() =>{return 判断用户是否登陆过 ? <NewSandBox /> : <Redirect to="/login" />*/}  
          <Route path="/" render={() =>{return localStorage.getItem("token") ? <NewSandBox /> : <Redirect to="/login" />
         } } />
        </Switch>

      </HashRouter>

    )
  }
}

```

## 3首页基本设置

下图大家会发现在首页中 左侧 与 右侧顶部 是不会变化的   右侧下面区域才是我们需要每次点击导航需要改变的内容所以我们可以使用二级路由来完成

![2b](.\img\2b.png)1.创建左侧和右侧顶部的组件 在components下创建leftList.jsx与rightTop.jsx用来容纳

2.在首页NewSandBox.jsx中引用两个组件

````jsx
// 引用左侧与右侧顶部的组件
import LeftList from "../components/leftList.jsx"
import RightTop from "../components/rightTop.jsx"
let NewSandBox=()=>{
  return (
      <div>
           <div>
                {/* 使用 */}
                <LeftList />
                <RightTop />
      		</div>
      </div>
  )
}
export default NewSandBox

````

3.设置右侧下半部分的二级路由

![1cc](.\img\1cc.png)

![3](.\img\3.png)

1.创建二级路由页面 分别为在views文件夹下

创建home文件夹 home.jsx(首页欢迎页面)  

创建user-manage文件夹并在其中创建list.jsx用户列表页面    

创建right-manage文件夹中新建 list.jsx 角色列表组件 roleList.jsx权限列表组件

创建no文件夹 no.jsx  404错误页面

2.配置路由规则 在NewSandBox.jsx中配置

```jsx

// 引用左侧与右侧顶部的组件
import LeftList from "../components/leftList.jsx"
import RightTop from "../components/rightTop.jsx"

// 引用二级路由页面
import Home from "./home/home.jsx"
import Rlist from "../views/right-manage/list.jsx"
import RoleList from "../views/right-manage/roleList.jsx"
import Ulist from "../views/user-manage/list.jsx"
import No from "../views/no/no.jsx"

import { Route, Switch, Redirect } from "react-router-dom"
let NewSandBox = () => {
  return (
    <div>
      <div>
        {/* 使用 */}
        <LeftList />
        <RightTop />

        {/* 配置二级路由规则 */}
        <Switch>
          <Route path="/home" component={Home} />
          <Route path="/user-manage/list" component={Ulist} />
          <Route path="/right-manage/list" component={Rlist} />
          <Route path="/right-manage/roleList" component={RoleList} />
          {/* 设置重定向保证第一次进入就显示欢迎页面home */}
          <Redirect from="/" to="/home" exact />
          {/* 在设置404错误页面 */}
          <Route component={No} />
        </Switch>
      </div>
    </div>
  )
}
export default NewSandBox

```

## 4.Antd使用

Antd 式蚂蚁集团 开发的一款企业级的后台pc端 React UI类库。 

官网：https://ant-design.gitee.io/index-cn

大家一定要记住   **文档在手 天下我有**



<img src=".\img\5.png" alt="5" style="zoom:70%;" />

### 1.基本使用

1.下载： yarn add antd 或 npm install --save antd

2.根据文档提示 我们可以使用它的button组件	

```jsx
import React, { Component } from 'react'
// 引用指定内容
import { Button } from 'antd';
export default class Home extends Component {
  render() {
    return (
      <div>
          首页欢迎
          {/* 使用 */}
          <Button type="primary">Button</Button>
      </div>
    )
  }
}

```

3.设置样式antd样式 

**官方式这样说的：**

 修改 `src/App.css`，在文件顶部引入 `antd/dist/antd.css`

**但是我们可以：**

在views文件夹设置一个css 在其中引用antd的样式  

```css
@import '~antd/dist/antd.css';
```

并且把刚设置的css 在views下的index.js中引用

```jsx
import "./index.css";
```



到此antd就已经成功安装到我们的项目中了

### 2.layout布局

在官网中发现下面的布局很符合我们的要求

<img src=".\img\55.png" alt="55" style="zoom: 67%;" />

分析代码我们发现需要改造之前的内容

1.修改整体页面布局NewSandBox.jsx中 把最外层的div 修改成layout 标签 但是不要忘了引用

```jsx
xxxxxx
xxxxx
xxxx
// 引用
import { Layout } from 'antd';

let NewSandBox = () => {
  return (
    // 修改成Layout
    <Layout>
    xxxxxx
    </Layout>
  )
}
export default NewSandBox

```

2.设置左边导航修改Leftlist.jsx中设置

```jsx
// 不要忘了引用
import { Layout, Menu } from 'antd';

import { 
    UserOutlined,
    VideoCameraOutlined,
    UploadOutlined,
  } from '@ant-design/icons';
  
const { Sider } = Layout;


let LeftList = () => {
    return (
        <Sider trigger={null} collapsible >
         <div className="logo" ></div>
            <Menu theme="dark" mode="inline" defaultSelectedKeys={['1']}>
                <Menu.Item key="1" icon={<UserOutlined />}>
                    nav 1
                </Menu.Item>
                <Menu.Item key="2" icon={<VideoCameraOutlined />}>
                    nav 2
                </Menu.Item>
                <Menu.Item key="3" icon={<UploadOutlined />}>
                    nav 3
                </Menu.Item>
            </Menu>
        </Sider>
    )
}
export default LeftList
```

3.设置有测的布局容器 在NewSandBox.jsx设置右侧内容的容器为layout

````jsx

import LeftList from "../components/leftList.jsx"
import RightTop from "../components/rightTop.jsx"
// 引用二级路由页面
import Home from "./home/home.jsx"
import Rlist from "../views/right-manage/list.jsx"
import RoleList from "../views/right-manage/roleList.jsx"
import Ulist from "../views/user-manage/list.jsx"
import No from "../views/no/no.jsx"
// 引用左侧与右侧顶部的组件
import { Route, Switch, Redirect } from "react-router-dom"
// 引用
import "./NewSandBox.css"
import { Layout } from 'antd';
const {Content } = Layout;
let NewSandBox = () => {
  return (
    // 修改成Layout
    <Layout className="site-layout">
     
        {/* 使用 */}
        <LeftList />
		设置有测容器为Layout
        <Layout>
        	xxxxxxxx
        </Layout>
     
    </Layout>
  )
}
export default NewSandBox

````

4.设置右侧顶部在 rightTop.jsx中

```jsx
import React, { Component,useState } from 'react'
import { Layout } from 'antd';
import {
  MenuUnfoldOutlined,
    MenuFoldOutlined
  } from '@ant-design/icons';
  
// 但是Header还需要引用
const { Header } = Layout;
let RightTop=()=>{
    创建变量
  const [collapsed]=useState(false)
  return (
    <Header className="site-layout-background" style={{ padding: "0 16px" }}>
        
    {/* {React.createElement(this.state.collapsed ? MenuUnfoldOutlined : MenuFoldOutlined, {
      className: 'trigger',
      onClick: this.toggle,
    })} */}
    {
      collapsed?<MenuUnfoldOutlined/>:<MenuFoldOutlined/>
    }
  </Header>
  )
}
export default RightTop

```

5.使用content包裹路由设置内容   在NewSandBox中设置

````jsx

import LeftList from "../components/leftList.jsx"
import RightTop from "../components/rightTop.jsx"

// 引用二级路由页面
import Home from "./home/home.jsx"
import Rlist from "../views/right-manage/list.jsx"
import RoleList from "../views/right-manage/roleList.jsx"
import Ulist from "../views/user-manage/list.jsx"
import No from "../views/no/no.jsx"

// 引用左侧与右侧顶部的组件
import { Route, Switch, Redirect } from "react-router-dom"
let NewSandBox = () => {
  return (
    // 修改成Layout
    <Layout>
      <div>
        {/* 使用 */}
        <LeftList />

        <Layout className="site-layout">
          <RightTop />
          {/* 配置二级路由规则 */}
      {/* 使用content组件包裹路由  不要忘了上面引用*/}
          <Content
            className="site-layout-background"
            style={{
              margin: '24px 16px',
              padding: 24,
              minHeight: 280,
            }}
          >
           xxxxxxx

          </Content>
        </Layout>
      </div>
    </Layout>
  )
}
export default NewSandBox

````

6.引用样式在views下新建NewSandBox.css 并且在NewSandBox。.js中引用

````css
#components-layout-demo-custom-trigger .trigger {
    padding: 0 24px;
    font-size: 18px;
    line-height: 64px;
    cursor: pointer;
    transition: color 0.3s;
  }
  
  #components-layout-demo-custom-trigger .trigger:hover {
    color: #1890ff;
  }
  
  #components-layout-demo-custom-trigger .logo {
    height: 32px;
    margin: 16px;
    background: rgba(255, 255, 255, 0.3);
  }
  
  .site-layout .site-layout-background {
    background: #fff;
  }
````

NewSandBox中引用

````js
import "./NewSandBox.css"
````

完成如下效果

<img src=".\img\555.png" alt="555" style="zoom: 67%;" />

## 5.样式优化

1.设置页面高度100%；抓取后发现我们只需要把容器的height设置成100%即可

<img src=".\img\5555.png" alt="555" style="zoom: 50%;" />

在NewSandBox.css中设置

```css
 #root,.ant-layout{
      height: 100%;
  }
```

2.设置右边header部分的图标部分rightTop中设置

<img src=".\img\555.png" alt="555" style="zoom: 67%;" />

```
  设置下padding的位置
  <Header className	="site-layout-background" style={{ padding: "0 16px" }}>
```

2.设置右边header部分的图标点击之后切换显示

```jsx
import React, { useState } from 'react'
import { Layout } from 'antd';
import {
  MenuUnfoldOutlined,
    MenuFoldOutlined
  } from '@ant-design/icons';
  
// 但是Header还需要引用
const { Header } = Layout;
let RightTop=()=>{
  const [collapsed,upcollapsed]=useState(false)
  // 修改下控制icon的变量取反
  let iconup=()=>{
    upcollapsed(!collapsed)
  }
  return (
    <Header className="site-layout-background" style={{ padding: "0 16px" }}>
        
    {/* {React.createElement(this.state.collapsed ? MenuUnfoldOutlined : MenuFoldOutlined, {
      className: 'trigger',
      onClick: this.toggle,
    })} */}
    {
      collapsed?<MenuUnfoldOutlined onClick={iconup}/>:<MenuFoldOutlined onClick={iconup}/>
    }
  </Header>
  )
}
export default RightTop
```

3.完成文字内容

<img src=".\img\6.png" alt="555" style="zoom: 67%;" />

````html
<span style={{float:"right"}}>欢迎xx</span>
````

4.设置鼠标移入下拉框

<img src=".\img\55555.png" alt="555" style="zoom: 67%;" />

```jsx
import React, { useState } from 'react'
import { Layout, Menu, Dropdown, Avatar } from 'antd';
import { DownOutlined } from '@ant-design/icons';

import {
  MenuUnfoldOutlined,
  MenuFoldOutlined,
  UserOutlined
} from '@ant-design/icons';

// 但是Header还需要引用
const { Header } = Layout;
let RightTop = () => {
 xxxxxxxx

  let menu = (
    <Menu>
      <Menu.Item>
        11
      </Menu.Item>
      <Menu.Item>
        22
      </Menu.Item>
      <Menu.Item >
        33
      </Menu.Item>
      <Menu.Item danger>退出登录</Menu.Item>
    </Menu>
  );
  return (
    <Header className="site-layout-background" style={{ padding: "0 16px" }}>

    xxxxxx

      <div style={{ float: "right" }}>
        <span >欢迎xx</span>

        {/* 设置下拉框 不要忘了引用*/}
        <Dropdown overlay={menu}>
          <Avatar size="large" icon={<UserOutlined />} />
        </Dropdown>
      </div>

    </Header>
  )
}
export default RightTop
```

## 6设置左侧导航



<img src=".\img\66.png" alt="66" style="zoom:67%;" />



去文档找到siderhttps://ant-design.gitee.io/components/layout-cn/#Layout.Sider 会发现可以设置

collapsed 当前收起状态

````jsx
// 不要忘了引用
import { Layout, Menu } from 'antd';

import { 
    UserOutlined,
    VideoCameraOutlined,
    UploadOutlined,
  } from '@ant-design/icons';
  
const { Sider } = Layout;


let LeftList = () => {
    return (
        // 设置之后会发现左侧菜单样式
        <Sider trigger={null} collapsible collapsed={true}>
            <div className="logo" ></div>
            <Menu theme="dark" mode="inline" defaultSelectedKeys={['1']}>
                <Menu.Item key="1" icon={<UserOutlined />}>
                    nav 1
                </Menu.Item>
                <Menu.Item key="2" icon={<VideoCameraOutlined />}>
                    nav 2
                </Menu.Item>
                <Menu.Item key="3" icon={<UploadOutlined />}>
                    nav 3
                </Menu.Item>
            </Menu>
        </Sider>
    )
}
export default LeftList
````

设置左侧导航标题文字

```
// 不要忘了引用
import { Layout, Menu } from 'antd';

import { 
    UserOutlined,
    VideoCameraOutlined,
    UploadOutlined,
  } from '@ant-design/icons';
  
const { Sider } = Layout;


let LeftList = () => {
    return (
        // 设置之后会发现左侧菜单样式
        <Sider trigger={null} collapsible collapsed={false}>
            {/* 设置左侧导航标题文字 */}
            <div className="logo" >全球新闻发布系统</div>
          xxxxxxx
          xxxxxx
          xxxxxx
        </Sider>
    )
}
export default LeftList
```

设置文字样式并且不要忘了在组件中引用

在components中新建index.css

```css
.logo{
    line-height: 32px;
    color: white;
    background-color: rgba(255,255,255,.3);
    font-size: 18px;
    margin: 10px;
    text-align: center;

}
```

在组件中引用

```js
import { Layout, Menu } from 'antd';
// 引用样式
import "./index.css"
import { 
    UserOutlined,
    VideoCameraOutlined,
    UploadOutlined,
  } from '@ant-design/icons';
  
const { Sider } = Layout;
```

完成如下效果



<img src=".\img\7.png" alt="7" style="zoom:50%;" />

导航设置伸缩效果 并且引用所需模块

```jsx
// 不要忘了引用
import { Layout, Menu } from 'antd';
// 引用样式
import "./index.css"
import {
    UserOutlined,
    VideoCameraOutlined,
    UploadOutlined,
    MailOutlined
} from '@ant-design/icons';

const { Sider } = Layout;
const { SubMenu } = Menu;



let LeftList = () => {
    return (
        // 设置之后会发现左侧菜单样式
        <Sider trigger={null} collapsible collapsed={false}>
            {/* 设置左侧导航标题文字 */}
            <div className="logo" >全球新闻发布系统</div>
            <Menu theme="dark" mode="inline" defaultSelectedKeys={['1']}>
         		  xxxxxx
				  xxxx
                <SubMenu key="sub1" icon={<MailOutlined />} title="Navigation One">
                    <Menu.Item key="5">Option 5</Menu.Item>
                    <Menu.Item key="6">Option 6</Menu.Item>
                    <Menu.Item key="7">Option 7</Menu.Item>
                    <Menu.Item key="8">Option 8</Menu.Item>
                </SubMenu>
            </Menu>
        </Sider>
    )
}
export default LeftList
```

但是上面的左侧导航是我们写死的 

在工作中侧边导航拦都是后台给我们的数据自动生成的  所以我们改造下侧边导航兰 让她变成动态的

所以我们分析导航发现 这个数据最少要有三个数据  分别是 icon  key是点击的路由路径 和文字

```
let listdata=[
	{
		key:??
		icon:??
		title:??
	}
]
```

但是我们今后导航还有二级的嵌套

```
let listdata=[
	{
		key:??,
		icon:??,
		title:??,
		children:[
			设置嵌套的内容
		]
	}
]
```

所以根据效果我们完成动态导航数据



<img src=".\img\8.png" alt="8" style="zoom:67%;" />

```jsx
// 不要忘了引用
import { Layout, Menu } from 'antd';
// 引用样式
import "./index.css"
import {
    UserOutlined,
    VideoCameraOutlined,
    UploadOutlined,
    MailOutlined
} from '@ant-design/icons';

const { Sider } = Layout;
const { SubMenu } = Menu;

// 设置导航数据
let listdata=[
    {
        icon:<UserOutlined />,
        title:"首页",
        key:"/home"
    },
    {
        icon:<VideoCameraOutlined />,
        title:"用户管理",
        key:"/user-manage",
        children:[
            {
                icon:<UserOutlined />,
                title:"用户列表",
                key:"/user-manage/list"
            },
        ]
    },
    {
        icon:<VideoCameraOutlined />,
        title:"权限管理",
        key:"/right-manage",
        children:[
            {
                icon:<UserOutlined />,
                title:"角色列表",
                key:"/right-manage/list"
            },
            {
                icon:<UserOutlined />,
                title:"权限列表",
                key:"/right-manage/roleList"
            },
        ]
    },
]

let LeftList = () => {
    return (
      xxxxxxx
    )
}
export default LeftList
```

开始动态渲染

```jsx
// 不要忘了引用
import { Layout, Menu } from 'antd';
// 引用样式
import "./index.css"
import {
    UserOutlined,
    VideoCameraOutlined,
    UploadOutlined,
    MailOutlined
} from '@ant-design/icons';

const { Sider } = Layout;
const { SubMenu } = Menu;

// 设置导航数据
let listdata=[
    {
        icon:<UserOutlined />,
        title:"首页",
        key:"/home"
    },
    {
        icon:<VideoCameraOutlined />,
        title:"用户管理",
        key:"/user-manage",
        children:[
            {
                icon:<UserOutlined />,
                title:"用户列表",
                key:"/user-manage/list"
            },
        ]
    },
    {
        icon:<VideoCameraOutlined />,
        title:"权限管理",
        key:"/right-manage",
        children:[
            {
                icon:<UserOutlined />,
                title:"角色列表",
                key:"/right-manage/list"
            },
            {
                icon:<UserOutlined />,
                title:"权限列表",
                key:"/right-manage/roleList"
            },
        ]
    },
]

let LeftList = () => {
    // 创建便利函数
    let showList=(data)=>{
      return  data.map(v=>{
            // 因为数据可能有嵌套的所以我们判断是否有children
            if(v.children){
                return (
                    <SubMenu key="sub1" icon={<MailOutlined />} title="Navigation One">
                   
                    </SubMenu>
                )
            }else{
              return (
                <Menu.Item key="1" icon={<UserOutlined />}>

                </Menu.Item>
                  )
            }
        })
    }
    return (
        // 设置之后会发现左侧菜单样式
        <Sider trigger={null} collapsible collapsed={false}>
            {/* 设置左侧导航标题文字 */}
            <div className="logo" >全球新闻发布系统</div>
            <Menu theme="dark" mode="inline" defaultSelectedKeys={['1']}>
                {/* 调用便利函数把要便利的数据传入 */}
                {showList(listdata)}
             
             
            </Menu>
        </Sider>
    )
}
export default LeftList
```

设置数据 并且使用递归便利二层级内容

````jsx
// 不要忘了引用
import { Layout, Menu } from 'antd';
// 引用样式
import "./index.css"
import {
    UserOutlined,
    VideoCameraOutlined,
    UploadOutlined,
    MailOutlined
} from '@ant-design/icons';

const { Sider } = Layout;
const { SubMenu } = Menu;

// 设置导航数据
let listdata = [
    {
        icon: <UserOutlined />,
        title: "首页",
        key: "/home"
    },
    {
        icon: <VideoCameraOutlined />,
        title: "用户管理",
        key: "/user-manage",
        children: [
            {
                icon: <UserOutlined />,
                title: "用户列表",
                key: "/user-manage/list"
            },
        ]
    },
    {
        icon: <VideoCameraOutlined />,
        title: "权限管理",
        key: "/right-manage",
        children: [
            {
                icon: <UserOutlined />,
                title: "角色列表",
                key: "/right-manage/list"
            },
            {
                icon: <UserOutlined />,
                title: "权限列表",
                key: "/right-manage/roleList"
            },
        ]
    },
]

let LeftList = () => {
    // 创建便利函数
    let showList = (data) => {
       return data.map(v => {
            // 因为数据可能有嵌套的所以我们判断是否有children
            if (v.children) {
                return (
                    <SubMenu key={v.key} icon={v.icon} title={v.title}>
                        {/* 使用递归方式在次调用便利二层级内容 */}
                        {showList(v.children)}
                    </SubMenu>
                )
            } else {
                return (
                    <Menu.Item key={v.key} icon={v.icon}>
                        {v.title}
                    </Menu.Item>
                )

            }
        })
    }
    return (
        // 设置之后会发现左侧菜单样式
        <Sider trigger={null} collapsible collapsed={false}>
            {/* 设置左侧导航标题文字 */}
            <div className="logo" >全球新闻发布系统</div>
            <Menu theme="dark" mode="inline" defaultSelectedKeys={['1']}>
                {/* 调用便利函数把要便利的数据传入 */}
                {showList(listdata)}

             
            </Menu>
        </Sider>
    )
}
export default LeftList
````



设置路由导航点击跳转

```jsx
xxxx
xxxx
// 函数组件设置props
let LeftList = (props) => {
    // 创建便利函数
    let showList = (data) => {
       return data.map(v => {
            // 因为数据可能有嵌套的所以我们判断是否有children
            if (v.children) {
                return (
                    <SubMenu key={v.key} icon={v.icon} title={v.title}>
                        {/* 使用递归方式在次调用便利二层级内容 */}
                        {showList(v.children)}
                    </SubMenu>
                )
            } else {
                return (
                    // 添加点击事件调用编程试导航
                    <Menu.Item key={v.key} icon={v.icon} onClick={
                        ()=>{
                            props.history.push(v.key)
                        }
                    }>
                        {v.title}
                    </Menu.Item>
                )

            }
        })
    }
xxxxx
xxxxx
xxxx
}
export default LeftList
```

但是报错了  所以我们使用withRouter高阶组件完成

```js
import {withRouter} from "react-router-dom"
	xxxxxxx
	xxxxxx
export default withRouter(LeftList)
```

## 7.权限列表

1.使用json-server模拟后台对应接口  启动mock文件夹下提供的json数据

![88](.\img\88.png)

但是大家发现我们两个导航是不同的接口 那么怎么把它们合并起来呢？

<img src=".\img\9.png" alt="9" style="zoom: 50%;" />

所以我们可以使用json-server的**_embed**联查方式得到就是用来获取包含下级资源的数据

在组件中发送请求尝试获取

```jsx
import {withRouter} from "react-router-dom"
import {useEffect,useState} from "react"
import $http from "axios"
// 不要忘了引用
import { Layout, Menu } from 'antd';
// 引用样式
import "./index.css"
import {
    UserOutlined,
    VideoCameraOutlined,
    UploadOutlined,
    MailOutlined
} from '@ant-design/icons';

const { Sider } = Layout;
const { SubMenu } = Menu;

// 设置导航数据
let listdata = [
    {
        icon: <UserOutlined />,
        title: "首页",
        key: "/home"
    },
    {
        icon: <VideoCameraOutlined />,
        title: "用户管理",
        key: "/user-manage",
        children: [
            {
                icon: <UserOutlined />,
                title: "用户列表",
                key: "/user-manage/list"
            },
        ]
    },
    {
        icon: <VideoCameraOutlined />,
        title: "权限管理",
        key: "/right-manage",
        children: [
            {
                icon: <UserOutlined />,
                title: "角色列表",
                key: "/right-manage/list"
            },
            {
                icon: <UserOutlined />,
                title: "权限列表",
                key: "/right-manage/roleList"
            },
        ]
    },
]
let LeftList = (props) => {

    // 发送请求
  useEffect(()=>{ 
    $http("http://localhost:8888/rights?_embed=children").then((ok)=>{
        console.log(ok.data)
    })

    },[])

    let showList = (data) => {
       return data.map(v => {
            if (v.children) {
                return (
                    <SubMenu key={v.key} icon={v.icon} title={v.title}>
                        {showList(v.children)}
                    </SubMenu>
                )
            } else {
                return (
                    <Menu.Item key={v.key} icon={v.icon} onClick={
                        ()=>{
                            props.history.push(v.key)
                        }
                    }>
                        {v.title}
                    </Menu.Item>
                )

            }
        })
    }
    return (
        // 设置之后会发现左侧菜单样式
        <Sider trigger={null} collapsible collapsed={false}>
            {/* 设置左侧导航标题文字 */}
            <div className="logo" >全球新闻发布系统</div>
            <Menu theme="dark" mode="inline" defaultSelectedKeys={['1']}>
                {/* 调用便利函数把要便利的数据传入 */}
                {showList(listdata)}

            
            </Menu>
        </Sider>
    )
}
export default withRouter(LeftList)
```

把请求来得数据动态生成 把请求得数据交给useState  并且传入到便利函数中

````jsx
import {withRouter} from "react-router-dom"
import {useEffect,useState} from "react"
import $http from "axios"
// 不要忘了引用
import { Layout, Menu } from 'antd';
// 引用样式
import "./index.css"
import {
    UserOutlined,
    VideoCameraOutlined,
    UploadOutlined,
    MailOutlined
} from '@ant-design/icons';

const { Sider } = Layout;
const { SubMenu } = Menu;


let LeftList = (props) => {
    // 创建接收变量
    let [listdata,setlistdata]=useState([])

    // 发送请求
  useEffect(()=>{ 
    $http("http://localhost:8888/rights?_embed=children").then((ok)=>{
        console.log(ok.data)
        // 修改
        setlistdata(ok.data)
    })

    },[])

    let showList = (data) => {
       return data.map(v => {
            if (v.children) {
                return (
                    <SubMenu key={v.key} icon={v.icon} title={v.title}>
                        {showList(v.children)}
                    </SubMenu>
                )
            } else {
                return (
                    <Menu.Item key={v.key} icon={v.icon} onClick={
                        ()=>{
                            props.history.push(v.key)
                        }
                    }>
                        {v.title}
                    </Menu.Item>
                )

            }
        })
    }
    return (
        // 设置之后会发现左侧菜单样式
        <Sider trigger={null} collapsible collapsed={false}>
            {/* 设置左侧导航标题文字 */}
            <div className="logo" >全球新闻发布系统</div>
            <Menu theme="dark" mode="inline" defaultSelectedKeys={['1']}>
                {/* 调用便利函数把要便利的数据传入 */}
                {showList(listdata)}

             
            </Menu>
        </Sider>
    )
}
export default withRouter(LeftList)
````

设置指定内容显示



<img src=".\img\10.png" alt="10" style="zoom:50%;" />

在工作中有的时候后台给我们的数据有的时候有些内容是不需要显示的（我们可以在项目开发前期和后台对接好 那么后台就会把这写不需要在页面显示的内容 在数据上进行标识 比我们们现在的数据）

![11](.\img\11.png)

所以我们在渲染的时候可以判断当前这个字段是否为1 如果为1 就渲染当前内容 否则不渲染

```jsx
import {withRouter} from "react-router-dom"
import {useEffect,useState} from "react"
import $http from "axios"
// 不要忘了引用
import { Layout, Menu } from 'antd';
// 引用样式
import "./index.css"
import {
    UserOutlined,
    VideoCameraOutlined,
    UploadOutlined,
    MailOutlined
} from '@ant-design/icons';

const { Sider } = Layout;
const { SubMenu } = Menu;


let LeftList = (props) => {
    // 创建接收变量
    let [listdata,setlistdata]=useState([])

    // 发送请求
  useEffect(()=>{ 
    $http("http://localhost:8888/rights?_embed=children").then((ok)=>{
        console.log(ok.data)
        // 修改
        setlistdata(ok.data)
    })

    },[])

    let showList = (data) => {
       return data.map(v => {
        //    设置判断
            if (v.children&&v.pagepermisson==1) {
                return (
                    <SubMenu key={v.key} icon={v.icon} title={v.title}>
                        {showList(v.children)}
                    </SubMenu>
                )
            } else {
                return (
                    v.pagepermisson==1&&<Menu.Item key={v.key} icon={v.icon} onClick={
                        ()=>{
                            props.history.push(v.key)
                        }
                    }>
                        {v.title}
                    </Menu.Item>
                )

            }
        })
    }
    return (
        // 设置之后会发现左侧菜单样式
        <Sider trigger={null} collapsible collapsed={false}>
            {/* 设置左侧导航标题文字 */}
            <div className="logo" >全球新闻发布系统</div>
            <Menu theme="dark" mode="inline" defaultSelectedKeys={['1']}>
                {/* 调用便利函数把要便利的数据传入 */}
                {showList(listdata)}

             
            </Menu>
        </Sider>
    )
}
export default withRouter(LeftList)
```

设置图标

因为我们不能给后台约束我们具体要什么图标 所以我们可以自定添加显示逻辑

````jsx
import {withRouter} from "react-router-dom"
import {useEffect,useState} from "react"
import $http from "axios"
// 不要忘了引用
import { Layout, Menu } from 'antd';
// 引用样式
import "./index.css"
import {
    UserOutlined,
    VideoCameraOutlined,
    UploadOutlined,
    MailOutlined
} from '@ant-design/icons';

const { Sider } = Layout;
const { SubMenu } = Menu;

// 设置导航数据
let listdata = [
    {
        icon: <UserOutlined />,
        title: "首页",
        key: "/home"
    },
    {
        icon: <VideoCameraOutlined />,
        title: "用户管理",
        key: "/user-manage",
        children: [
            {
                icon: <UserOutlined />,
                title: "用户列表",
                key: "/user-manage/list"
            },
        ]
    },
    {
        icon: <VideoCameraOutlined />,
        title: "权限管理",
        key: "/right-manage",
        children: [
            {
                icon: <UserOutlined />,
                title: "角色列表",
                key: "/right-manage/list"
            },
            {
                icon: <UserOutlined />,
                title: "权限列表",
                key: "/right-manage/roleList"
            },
        ]
    },
]



// 创建图标数组
let dataicon={
    "/home":<UserOutlined />,
    "/user-manage":<VideoCameraOutlined />,
    "/user-manage/list":<UserOutlined />
    // ....

}
let LeftList = (props) => {
    // 创建接收变量
    let [listdata,setlistdata]=useState([])

    // 发送请求
  useEffect(()=>{ 
    $http("http://localhost:8888/rights?_embed=children").then((ok)=>{
        console.log(ok.data)
        // 修改
        setlistdata(ok.data)
    })

    },[])

    let showList = (data) => {
       return data.map(v => {
        //    设置判断
            if (v.children&&v.pagepermisson==1) {
                return (
                    // 插入图标
                    <SubMenu key={v.key} icon={dataicon[v.key]} title={v.title}>
                        {showList(v.children)}
                    </SubMenu>
                )
            } else {
                return (
                      // 插入图标
                    v.pagepermisson==1&&<Menu.Item key={v.key} icon={dataicon[v.key]} onClick={
                        ()=>{
                            props.history.push(v.key)
                        }
                    }>
                        {v.title}
                    </Menu.Item>
                )

            }
        })
    }
    return (
        // 设置之后会发现左侧菜单样式
        <Sider trigger={null} collapsible collapsed={false}>
            {/* 设置左侧导航标题文字 */}
            <div className="logo" >全球新闻发布系统</div>
            <Menu theme="dark" mode="inline" defaultSelectedKeys={['1']}>
                {/* 调用便利函数把要便利的数据传入 */}
                {showList(listdata)}

               
            </Menu>
        </Sider>
    )
}
export default withRouter(LeftList)
````

但是现在大家发现首页本身是没有二级的但是现在有二级箭头我们可以取消他

![12](.\img\12.png)

只需要判断长度即可

```jsx
 //    设置判断长度是否大于0
            if (v.children.length>0&&v.pagepermisson==1) {
                return (
                    // 插入图标
                    <SubMenu key={v.key} icon={dataicon[v.key]} title={v.title}>
                        {showList(v.children)}
                    </SubMenu>
                )
            } else {
                return (
                      // 插入图标
                    v.pagepermisson==1&&<Menu.Item key={v.key} icon={dataicon[v.key]} onClick={
                        ()=>{
                            props.history.push(v.key)
                        }
                    }>
                        {v.title}
                    </Menu.Item>
                )

            }
        })
```

但是报错了

leftList.jsx:83 Uncaught TypeError: Cannot read properties of undefined (reading 'length')

是因为有的里面没有children所以有个判断的小技巧 使用三元运算符 如果?前面是undefined那么就不执行.length

````
v.children?.length>0
````

```jsx
 if (v.children?.length>0&&v.pagepermisson==1) {
                return (
                    // 插入图标
                    <SubMenu key={v.key} icon={dataicon[v.key]} title={v.title}>
                        {showList(v.children)}
                    </SubMenu>
                )
            } else {
                return (
                      // 插入图标
                    v.pagepermisson==1&&<Menu.Item key={v.key} icon={dataicon[v.key]} onClick={
                        ()=>{
                            props.history.push(v.key)
                        }
                    }>
                        {v.title}
                    </Menu.Item>
                )

            }
```



但是现在每次刷新都只显示第一项高亮  我们想选中谁谁高亮 哪怕是刷新之后 我们就要设置Menu的defaultSelectedKeys属性初始选中的菜单项 key 数组 

我们可以通过props.location得到当前页面的路由路径  在传入defaultSelectedKeys即可

````jsx
xxxxx
xxxxx

    console.log(props.location.pathname)//得到信息
    let selectKeys=props.location.pathname
    return (
        <Sider trigger={null} collapsible collapsed={false}>
            <div className="logo" >全球新闻发布系统</div>
            {/* 传入到初始选中的菜单项 key */}
            <Menu theme="dark" mode="inline" defaultSelectedKeys={selectKeys}>
                {showList(listdata)}

             
            </Menu>
        </Sider>
    )
}
export default withRouter(LeftList)
````

但是一刷新二级菜单是折叠的  我们让选中之后打开这个二级菜单

所以我们需要把一级路由路径截取出来  传入到defaultOpenKeys这个属性中初始展开的 SubMenu 菜单项 key 数组

```jsx


    console.log(props.location.pathname)//得到信息
    let selectKeys=props.location.pathname
      // 截取到一级路由路径 注意这是一个数组
    let openKeys=    let openKeys=[ "/"+props.location.pathname.split("/")[1] ]
    return (
        <Sider trigger={null} collapsible collapsed={false}>
            <div className="logo" >全球新闻发布系统</div>
            {/* 传入到初始选中的菜单项 key */}
            <Menu theme="dark" mode="inline" defaultSelectedKeys={selectKeys}
            // 在设置一级导航展开
                defaultOpenKeys={openKeys}
            >
                {showList(listdata)}

               
            </Menu>
        </Sider>
    )
}
export default withRouter(LeftList)
```





