# 扩展

# -Reactd的设计思路

## 转换式系统与响应式系统

转换式系统：输入求解输出的过程。////编译器----数值计算

响应式系统：监听事件，消息驱动。重点是UI与用户的交互。////UI系统

![image-20220318144903134](/Users/wyt/Library/Application Support/typora-user-images/image-20220318144903134.png)

## 响应式编程

- 状态更新，UI自动更新。

- 前端代码组件化，可复用，可封装。

- 状态之间相互依赖，只需要声明。

  ### 组件化

  - 组件是 组件的组合/原子的组合
  - 组件内部拥有状态，外部不可见
  - 父组件可以将状态传入子组件内部

  ### 组件设计

  - 组件声明了状态和UI的映射

    就是数学上的函数关系

  - 组建由Props/State两种状态

    - State是私有的，内部的，外部不可见
    - Props是外部传入的。来自于父组件

  - 组件可以由其他组件拼装而成

    - 组件内部有私有状态state
    - 组价接受外部的Props状态提供复用性
    - 根据当前的Props/State,返回一个UI

####  纯函数

# -typescript

## 什么是typescript

**静态类型弱类型语言**

- 静态类型语言，基于语法解析TSDoc，ide增强
- 可维护性的增强：在编译阶段会暴露大部分错误=》多人合作项目中，获得更好的稳定性和开发效率

**JS的超集**

- 包含于兼容所有JS特性，支持共存
- 支持渐进式引入与升级

## 基本语法

### 变量的数据类型定义

#### 基本数据类型

在变量后使用 冒号+数据类型进行声明

```
const q:string = 'string'
const w:number = 1
const e:boolean = true
const r:null = null
```

#### 对象数据类型

冒号后添加自定义类型 ；**（一般情况下用大写I开头，以表示这是一个类型）**

通过interface关键字进行定义。

```tsx
interface IMan {
	readonly name : string;
	sex :'man' | 'woman' | 'other';
	age: number;
	hobby?:string;
	[key:string]:any
}

```

注意：

- 关键字readonly，不可在对象初始化外进行赋值。
- 关键字 ？：代表可选属性
- 关键字key [key:string]: any; 代表我们未知定义的属性为string，值为any；

#### 函数类型

##### **在函数参数上直接进行定义**

```tsx
function add (x:number,y:number):number{
	return x+y;
}
```

##### 或返回值的定义用=>进行定义

```tsx
const mult : (x:number,y:number)=>number = (x,y)=>x*y;
```

##### 同时函数也支持用interface进行定义

```
interface IMult {
	(x:number,y:number):number;
}
const mult:IMult = (x,y)=>x*y;
```

##### 函数的重载

```
function getDate(type:"string",timestamp?:string):string;
function getDate(type:"date",timestamp?:string):date;
function getDate(type:"string"|"date",timestamp?:string):string|date{
	const date = new Date(timestamp);
	return type === 'string'?date.toLocaleString():date;
};
const x = getDate('date');/////x:Date
const y = getDate('string'.'2020-01-01');//y:string
```

上面代码用 interface进行书写---它会出问题

```
interface IGetDate {
	(type:'string',timestamp?:string):String;
	(type:"date",timestamp?:string):Date;
	(type:"string"|"date",timestamp?:string):string|date;
}
```



#### 数组类型

多用1，2两种方式 

```
type IArr1 = number[];
type IArr2 = Array<string | number | Record<string,number>>;
type IArr3 = [number,number,string,string];
interface IArr4 {
	[key:number]:any
}
```

### 泛型

```ts
function getRepeatArr(target){
	return new Array(100).fill(target)
}

//简单粗暴 不做推荐，且失去 定义的意义
type IGetRepeatArr = (target:any)=>any[];


//不预先指定类型，但在使用的时候会指定类型的一种新的特性
type IGetRepeatArr = <T>(traget:T)=>T[];

```

在函数中使用时，泛型写在圆括号前，其他时间均写在泛型名的后面用尖括号。

#### 泛型可使用extends进行约束

![image-20220319113221209](/Users/wyt/Library/Application Support/typora-user-images/image-20220319113221209.png)

#### 泛型可以添加默认类型

![image-20220319113243239](/Users/wyt/Library/Application Support/typora-user-images/image-20220319113243239.png)

### type---类型别名

```
type IObjArr = Array<{
	key:string;
	[objkey:string]:any;
}>

function keyBy <T extends IObjArr>(objArr:Array<t>){
	//未定义类型是，result类型是{}
	const result = objArr.reduce((res,val,key)=>{
	res[key] = val;
	return =res;
	},{});
	//我们可以通过as关键字，断言result类型为正确类型
	return result as Record<string,T>;
}
```

### 字符串 字面量

```tsx
type IDomTag = 'html' | 'body' | 'div' ;
表明 IDomTag 必须是上述其中之一。
```

### 联合||交叉类型

传统方法：将两个interface使用 | 分割符分隔开

```jsx
interface IHistoryBook {
	author:string;
	type:string;
	range:string
}

interface IStoryBook {
	author:String;
	type:Srting;
	theme:String
} 
 
type IBookList = Array< IHistoryBook | IStoryBook>

```

联合交叉类型写法如下

```
 type IBookList = Array<{
 	author:striong;
 }&({
 	type:'history';
 	range:string;
 }|{
 	type:'story';
 	theme:string
 })>
```



# React

- 单向数据流
-  

## 基础

### （概念的理解）

### Virtual Dom

Virtual Dom 是一种用于和真是DOM同步，而在JS内存中维护的一个对象，它具有和DOM类似的树状结构，并和DOM建立一一对应的关系。

它赋予了React声明式的API:您告诉React希望让UI是什么状态，React就确保DOM匹配该状态。这是您可以从属性操作、事件处理和手动DOM更新在构建程序时必要的操作中解放出来。



![image-20220318155744516](/Users/wyt/Library/Application Support/typora-user-images/image-20220318155744516.png)

### diff

- 权衡![image-20220318155949300](/Users/wyt/Library/Application Support/typora-user-images/image-20220318155949300.png)

- ![image-20220318160121575](/Users/wyt/Library/Application Support/typora-user-images/image-20220318160121575.png)

- #### 三条规则

  - 不同的元素：替换
  - 同类新的DOM：更新
  - 同类型的组件：递归更新 

### 声明周期

#### 状态上升

状态属于两个节点向上寻找到最近的祖宗节点

#### **请简述你对react的理解**

React是一个简单的JavaScript UI库，用于构建高效、快速的用户界面。它是一个轻量级库，因此很受欢迎。它遵循组件设计模式、声明式编程范式和函数式编程概念，以使前端应用程序更高效。它使用虚拟DOM来有效地操作DOM。它遵循从高阶组件到低阶组件的单向数据流。

#### state与props的区别

两者都是普通的JS对象，用于保存数据：

- **props是传递给组件的（类似于函数的形参），而state是在组件内被组件自己管理的**。
- props不可被修改，但是state可以通过setState被修改，setstate是异步的
- 一般state在constructor中初始化

#### 组件之间的数据传递

- 正传：props，子接受，父传递。使用TS时，需要添加接口验证数据类型。

- 逆传：通过正传一个带形参的函数过来，在子组件中使用时间通过`this.props.fuFun.bind(this,'对形参赋值‘）`，然后再父组件中读取形参的值。使用TS时，需要在子组件中使用接口验证约束的fuFun`()=>void`,父组件中需要验证形参数据类型。

- 同胞传值：通过pubsub-js进行组件间传值，通过pubsub.publish（’事件名‘，数据）进行抛出，可以通过 pubsub.subscribe('监听的事件名',('事件名',数据)=>{    可以得到数据})

- 跨组件传值---context：上下文对象，无需为每一层添加props，就可以组件间进行数据传递的方法，使用createContext()方法提供了两个对象，Provider--》生产者对象--用于生产数据；Consumer---》消费者对象----用来使用数据.

  ```jsx
  //需要先引入一个context对象
   let context = React.createContext()
  
  <context.Provider value={{name:"xixi",age:18}}>  <context.Provider/>
  //抛出数据
  <context.Consumer>{
                          (value)=>{
                              return (
                                  <h1>{value.name}----{value.age}</h1>
                              )
                          }
                      }
  <context.Consumer>                    
                   
  ```

- redux 第三方数据管理工具

- 三大原则：

  - 单一数据源：所有数据都保存在一个store中
  - state是只读的，只能使用action里的方法进行修改
  - 使用纯函数进行修改，reducer

- 使用方法

  - 构造store

   ```
    //1引入对象  
    import {createStore} from "redux"
    
    let data ={
    	//以对象的形式写入你要存的数据
    }
    //5创建reducer
    let reducuer =(state=data,action)=>{
    	return state
    })
    
    //2创建对象 4 把reducer传入实例化的对象
    let store = createStore()
    //3暴露redux对象
    export default store 
   ```

  - 使用 redux
  
    - store.getState() 获取redux中所存的数据
    - 通过dispatch()来调用action的修改 store.dispatch({type:"你要执行的操作名"}),
    - 构造action方法
  
    ```js
    let reducer = (state=data,action)=>{
    	//通过switch判断传进来的操作名
    	switch （action.type){
    		case 'plus':
    			//此处进行修改函数的编写 一定要返回 state
    			
    			return {....state,name:'我修改了name'}
    			break；
    		case  '   ':
    			return {...state,age:"我修改了age"}
    			break;
    		default :
    		return state
    		break;
    	}
    
    ```

### vue与React的区别

- 共同点
  - 都是基于JavaScript的框架，两者只有框架的骨架，其他的功能（路由，状态管理）都是框架分离的组件。
  - 都使用了虚拟DOM，用于映射真实的DOM树，当变化产生时，一个新的虚拟DOM会被创建，并同事比较与旧的之间的区别，通过diff算法计算出相对最迅速的方法去实现更新。
  - 两者均推崇组件化
  - props,两者均有props概念，单项数据流允许数据从上向下传输。
- 不同点
  - vue有双向绑定机制，他的单项数据流中子组件可以读取数据，但是不能更改。
  - react单向数据流依赖state，改变state并不会改变DOM，只有setState触发的时候才能触发render()方法进行重新渲染。但是如果父组件的props改变了，会重新渲染子组件。
  - vue会计算出虚拟DOM的差异，在渲染中跟踪每个组件的依赖关系，不会重新渲染dom树。
  - react当状态改变的时候会重新渲染全部子组件，可以通过shouldComponentUpdate()声明周期进行优化 （return FALSE）就不会被重新渲染。
  - vue有单文件组件
  - react依赖于jsx在 JavaScript中写dom

### 虚拟dom与diff算法

- 虚拟dom：可以看似在js与真实dom之间增加了一层缓存，在每次状态更新的时候，react都会先更新虚拟dom树，然后通过diff算法算出近似最优解去更新真是dom树；
  - **Virtual Dom 是一种用于和真实DOM同步，而在JS内存中维护的一个对象，它具有和DOM类似的树状结构，并和DOM建立一一对应的关系。**
- **diff算法**：是**调和过程(Reconciliation)**的具体体现。就是通过计算更新后的虚拟dom树与旧的虚拟dom树进行比较，得到更新的地方，然后通过一下三种原则计算出近似最优解更新dom树，已达到视图的更改。
  - 原理：
    - 按照组件进行分层，只比较统计元素
    - 给列表的每个单元添加唯一key以便比较
    - 合并操作，调用 component 的 setstate 方法的时候, React 将其标记为 dirty，到每一个事件循环结束, React 检查所有标记 dirty 的 component 重新绘制
    - 选择性子树渲染。开发人员可以重写 shouldComponentUpdate 提高 diff 的性能。
  - 原则：
    - 不同的元素：替换
    - 同类新的DOM：更新
    - 同类型的组件：递归更新 
- **关于v-dom提高性能**：利用diff算法避免了不必要的更新和加载以及dom操作。
- **shouldComponentUpdate**:可以使用shouldComponentUpdate 中 return FALSE来组织组件更新。

### setState:会触发调和过程(Reconciliation)。



## 组件

### 你对组件的理解

提高代码的复用性、可读性以及可维护性。

- 复用性：组件将数据和逻辑进行封装。
- 可读性与可维护性：语法直观，提高可读性，高聚合低耦合。

### 类组件

#### 不足：-----

- 状态逻辑难以复用：如果要复用，可能要用到render或者HOC，都会增加组件的层级。造成代码冗余。

- 趋向复杂难以维护：

  - 在生命周期函数中混杂不相干的逻辑
  - 类组件中到处都是对状态的访问和处理，导致组件难以拆分成更小的组件

- this指向问题：父组件给子组件传递函数时，必须绑定this

  - react中绑定this的四种方法：

  ```js
  import React, { Component } from 'react'
  
  export default class App extends Component {
      handleClick2;
  
      constructor(props) {
          super(props);
          this.state = {
              num: 1,
              title: ' react study'
          };
          this.handleClick2 = this.handleClick1.bind(this);
      }
  
      handleClick1() {
          this.setState({
              num: this.state.num + 1,
          })
      }
  
      handleClick3 = () => {
          this.setState({
              num: this.state.num + 1,
          })
      };
  
      render() {
          return (<div>
              <h2>Ann, {this.state.num}</h2>
              <button onClick={this.handleClick2}>btn1</button>
              {/* 第一种是在构造函数中绑定 this：那么每次父组件刷新的时候，如果传递给子组件其他的 props 值不变，那么子组件就不会刷新； */}
              <button onClick={this.handleClick1.bind(this)}>btn2</button>
              {/* 第二种是在 render() 函数里面绑定 this：因为 bind 函数会返回一个新的函数，所以每次父组件刷新时，都会重新生成一个函数，即使父组件传递给子组件其他的 props 值不变，子组件每次都会刷新； */}
              <button onClick={() => this.handleClick1()}>btn3</button>
              {/* 第三种是使用箭头函数：父组件刷新的时候，即使两个箭头函数的函数体是一样的，都会生成一个新的箭头函数，所以子组件每次都会刷新； */}
              <button onClick={this.handleClick3}>btn4</button>
              {/* 第四种是使用类的静态属性：原理和第一种方法差不多，比第一种更简洁 */}
          </div>)
      }
  
  }
  ```

### 无状态组件

- 组件不会被实例化，提高了性能
- 无this指向
- 无法访问声明周期函数

## Hook

### 注意

- 不要在循环，条件或嵌套函数中调用Hook.

- 只能在函数组件中调用。

### Hooks的解决的问题

- 解决上述的三个类组件的显著问题

- 可以在不修改组件结构状态的情况下复用状态逻辑（自定义hooks）

- 可以将组件中相互关联的部分拆成更小的函数部分（比如设置订阅和请求）

- **副作用的关注点分离：**副作用值得是那些没有发生在数据向视图转换中的逻辑，比如 请求，获取dom，本地缓存的处理，绑定事件，添加定时器等等。再类组件中，都是写在生命周期函数中的。而 `useEffect` 在全部渲染完毕后才会执行，`useLayoutEffect` 会在浏览器 `layout` 之后，`painting` 之前执行。

### 常用Hook

#### useState

- **useState**： 传入一个惟一的参数就是state的初始值

- **useState 会返回一个数组**：**一个 state，一个更新 state 的函数**

  ```
  const [state, setState] = useState(initialState);
  ```

  - 在初始化渲染期间，返回的状态 (state) 与传入的第一个参数 (initialState) 值相同
  - 你可以在事件处理函数中或其他一些地方调用这个函数。它类似 class 组件的 this.setState，但是它**不会把新的 state 和旧的 state 进行合并，而是直接替换**

- **每次渲染都是独立的闭包**

  - 每一次渲染都有它自己的 Props 和 State
  - 每一次渲染都有它自己的事件处理函数
  - 当点击更新状态的时候，函数组件都会重新被调用，那么每次渲染都是独立的，取到的值不会受后面操作的影响,

  **如下，在先点击alert事件再调用`setNumber(+1)`时，3秒后也只会弹出点击事件时的number的状态。**

  ```
  function Counter2(){
    let [number,setNumber] = useState(0);
    function alertNumber(){
      setTimeout(()=>{
        // alert 只能获取到点击按钮时的那个状态
        alert(number);
      },3000);
    }
    return (
        <>
            <p>{number}</p>
            <button onClick={()=>setNumber(number+1)}>+</button>
            <button onClick={alertNumber}>alertNumber</button>
        </>
    )
  }
  ```

- **函数式更新**

  - **如果新的 state 需要通过使用先前的 state 计算得出，那么可以将回调函数当做参数传递给 setState。该回调函数将接收先前的 state，并返回一个更新后的值。**

  **如下，在先点击lazy事件再调用`setNumber(+1)`时，如果修改中不使用回调函数，则不会去重新获取number的值，只会返回1，如果采用回调函数，则会3秒后计算时使用当下number的值，就是说在者三秒钟之内的+1效果可以生效。**

  ```
  function Counter(){
      let [number,setNumber] = useState(0);
      function lazy(){
          setTimeout(() => {
              // setNumber(number+1);
              // 这样每次执行时都会去获取一遍 state，而不是使用点击触发时的那个 state
              setNumber(number=>number+1);
          }, 3000);
      }
      return (
          <>
             <p>{number}</p>
             <button onClick={()=>setNumber(number+1)}>+</button>
             <button onClick={lazy}>lazy</button>
          </>
      )
  }
  
  ```

- **惰性初始化 state**

  - **initialState 参数只会在组件的初始化渲染中起作用，后续渲染时会被忽略**
  - **如果初始 state 需要通过复杂计算获得，则可以传入一个函数，在函数中计算并返回初始的 state，此函数只在初始渲染时被调用**

  如下,在父组件更新props.number的状态时和在子组件本身更新counter.number时，`console.log('Counter5 render')`都会被执行，而`console.log('initState');`只会在页面首次渲染的时候执行一次，手动调用的话，conter的状态也会改变。(经测试，此处不能执行异步函数)

  ```
  function Counter5(props){
      console.log('Counter5 render');
      // 这个函数只在初始渲染时执行一次，后续更新状态重新渲染组件时，该函数就不会再被调用
      function getInitState(){
      	console.log('initState');
          return {number:props.number};
      }
      let [counter,setCounter] = useState(getInitState);
      return (
          <>
             <p>{counter.number}</p>
             <button onClick={()=>setCounter({number:counter.number+1})}>+</button>
             <button onClick={()=>setCounter(counter)}>setCounter</button>
          </>
      )
  }
  ```

- 关于useState的性能优化

  **Object.is**

  - **Object.is** ：hook内会使用Object.is进行浅比较新旧state是否相等。与类组件的setState不同的是如果修改的数据与原数据相同，不会重新渲染。
  - **与 class 组件中的 setState 方法不同，useState 不会自动合并更新对象。你可以用函数式的 setState 结合展开运算符来达到合并更新对象的效果**

  **减少渲染次数**

  - **默认情况，只要父组件状态变了（不管子组件依不依赖该状态），子组件也会重新渲染**
  - **一般的优化**：
    - **类组件**：可以使用 `pureComponent` ；
    - **函数组件**：使用 `React.memo` ，将函数组件传递给 `memo` 之后，就会返回一个新的组件，新组件的功能：**如果接受到的属性不变，则不重新渲染函数**；
  - 深度优化此处会用到 useCallback/useMemo

#### useCallback:

接收一个内联回调函数参数和一个依赖项数组（子组件依赖父组件的状态，即子组件会使用到父组件的值） ，useCallback 会返回该回调函数的 memoized 版本，该回调函数仅在某个依赖项改变时才会更新

#### useMemo:

把创建函数和依赖项数组作为参数传入 `useMemo`，它仅会在某个依赖项改变时才重新计算 memoized 值。这种优化有助于避免在每次渲染时都进行高开销的计算。

```
import React,{useState,memo,useMemo,useCallback} from 'react';

function SubCounter({onClick,data}){
    console.log('SubCounter render');
    return (
        <button onClick={onClick}>{data.number}</button>
    )
}
SubCounter = memo(SubCounter);

let oldData,oldAddClick;
export  default  function Counter2(){
    console.log('Counter render');
    const [name,setName]= useState('计数器');
    const [number,setNumber] = useState(0);
    // 父组件更新时，这里的变量和函数每次都会重新创建，那么子组件接受到的属性每次都会认为是新的
    // 所以子组件也会随之更新，这时候可以用到 useMemo
    // 有没有后面的依赖项数组很重要，否则还是会重新渲染
    // 如果后面的依赖项数组没有值的话，即使父组件的 number 值改变了，子组件也不会去更新
    //const data = useMemo(()=>({number}),[]);
    const data = useMemo(()=>({number}),[number]);
    console.log('data===oldData ',data===oldData);
    oldData = data;
    
    // 有没有后面的依赖项数组很重要，否则还是会重新渲染
    const addClick = useCallback(()=>{
        setNumber(number+1);
    },[number]);
    console.log('addClick===oldAddClick ',addClick===oldAddClick);
    oldAddClick=addClick;
    return (
        <>
            <input type="text" value={name} onChange={(e)=>setName(e.target.value)}/>
            <SubCounter data={data} onClick={addClick}/>
        </>
    )
}
```

#### useReducer:

##### 什么时候用useReducer

- 如果你的`state`是一个数组或者对象

- 如果你的`state`变化很复杂，经常一个操作需要修改很多state

- 如果你希望构建自动化测试用例来保证程序的稳定性

- 如果你需要在深层子组件里面去修改一些状态（关于这点我们下篇文章会详细介绍）

- 如果你用应用程序比较大，希望UI和业务能够分开维护

##### 基本知识

const [state, dispatch] = useReducer(reducer, initialState,init);

- useReducer 和 redux 中 reducer 很像

- useState 内部就是靠 useReducer 来实现的

- useState 的替代方案，它接收一个形如 (state, action) => newState 的 reducer，并返回当前的 state 以及与其配套的 dispatch 方法

- 在某些场景下，useReducer 会比 useState 更适用，例如 state 逻辑较复杂且包含多个子值，或者下一个 state 依赖于之前的 state 等

```
let initialState = 0;
// 如果你希望初始状态是一个{number:0}
// 可以在第三个参数中传递一个这样的函数 ()=>({number:initialState})
// 这个函数是一个惰性初始化函数，可以用来进行复杂的计算，然后返回最终的 initialState
const [state, dispatch] = useReducer(reducer, initialState, init);
-------------------------------------
const initialState = 0;
function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {number: state.number + 1};
    case 'decrement':
      return {number: state.number - 1};
    default:
      throw new Error();
  }
}
function init(initialState){
    return {number:initialState};
}
function Counter(){
    const [state, dispatch] = useReducer(reducer, initialState,init);
    return (
        <>
          Count: {state.number}
          <button onClick={() => dispatch({type: 'increment'})}>+</button>
          <button onClick={() => dispatch({type: 'decrement'})}>-</button>
        </>
    )
}

```

#### useContext

主要为了简化在函数组件中使用上下文环境的复杂度，存入一个context。可以返回一个context（上下文环境）的对象，包含传入的context对象的数据。

- 接收一个 context 对象（React.createContext 的返回值）并返回该 context 的当前值

- 当前的 context 值由上层组件中距离当前组件最近的 <MyContext.Provider> 的 value prop 决定

- 当组件上层最近的 <MyContext.Provider> 更新时，该 Hook 会触发重渲染，并使用最新传递给 MyContext provider 的 context value 值

- **useContext(MyContext) 相当于 class 组件中的** `static contextType = MyContext` 或者 `<MyContext.Consumer>`

- **useContext(MyContext) 只是让你能够读取 context 的值以及订阅 context 的变化。你仍然需要在上层组件树中使用 <MyContext.Provider> 来为下层组件提供 context**。

```jsx
import React, { useReducer, createContext, useContext } from 'react';
import ReactDOM from 'react-dom';

const initialState = 0;
function reducer(state = initialState, action) {
    switch (action.type) {
        case 'ADD':
            return { number: state.number + 1 };
        default:
            break;
    }
}

const CounterContext = createContext();
// 第一种获取 CounterContext 方法：不使用 hook
function SubCounter_one() {
    return (
        <CounterContext.Consumer>
            {
                value => (
                    <>
                        <p>{value.state.number}</p>
                        <button onClick={() => value.dispatch({ type: 'ADD' })}>+</button>
                    </>
                )
            }

        </CounterContext.Consumer>
    )
}
// 第二种获取 CounterContext 方法：使用 hook ，更简洁
function SubCounter() {
    const { state, dispatch } = useContext(CounterContext);
    return (
        <>
            <p>{state.number}</p>
            <button onClick={() => dispatch({ type: 'ADD' })}>+</button>
        </>
    )
}
/* class SubCounter extends React.Component{
    static contextTypes = CounterContext
    this.context =  {state, dispatch}
} */

 function UseContext() {
    const [state, dispatch] = useReducer((reducer), initialState, () => ({ number: initialState }));
    return (
        <>
            <CounterContext.Provider value={{ state, dispatch }}>
            <h1>第一种获取 CounterContext 方法：不使用 hook</h1>
                <SubCounter />
                <h1>第二种获取 CounterContext 方法：使用 hook ，更简洁</h1>
                <SubCounter_one/>
            </CounterContext.Provider>
        </>

    )
}

export default UseContext
```

#### **useEffect**：

默认情况它在三组生命周期（挂载，更新，销毁）都会调用，但是通过对第二个参数的设置可以分别模拟。

##### 模拟componentDidMount

- **useEffect(()=>{},[])**

##### 模拟componentDidUpdate

- 不传递第二个数组参数可以模拟，但是有区别就是 生命周期函数并不会在渲染时执行，但是模拟的会。

- **useEffect(()=>{})**

##### 模拟componentWillUnmount

- **useEffect(()=>{ return ()=>{console.log ('此时模拟了销毁前')}})

- **effect（副作用）：指那些没有发生在数据向视图转换过程中的逻辑，如 `ajax` 请求、访问原生`dom` 元素、本地持久化缓存、绑定/解绑事件、添加订阅、设置定时器、记录日志等。**

- useEffect 就是一个 Effect Hook，给函数组件增加了操作副作用的能力。它跟 class 组件中的 `componentDidMount`、`componentDidUpdate` 和 `componentWillUnmount` 具有相同的用途，只不过被合并成了一个 API

- **useEffect 接收一个函数，该函数会在组件渲染到屏幕之后才执行，该函数有要求：要么返回一个能清除副作用的函数，要么就不返回任何内容**

- 与 `componentDidMount` 或 `componentDidUpdate` 不同，使用 useEffect 调度的 effect 不会阻塞浏览器更新屏幕，这让你的应用看起来响应更快。大多数情况下，effect 不需要同步地执行。在个别情况下（例如测量布局），有单独的 useLayoutEffect Hook 供你使用，其 API 与 useEffect 相同。

- 当数组参数不存在时，可近似模拟componentDidUpdate，但是初始化时会执行

- useEffect(()=>{},[]),如果数组为空，则可以模拟componentDidMount 

##### **业务上的使用**

- **需要在不同生命周期执行同样的函数内容，如修改标题等等。类组件需要在两个生命周期钩子中调用两次，而useEffcet不需要。**
- **副作用函数还可以通过返回一个函数来指定如何清除副作用，为防止内存泄漏，清除函数会在\**\*\*组件卸载前\*\**\*执行。如果组件多次渲染，则在执行下一个 effect 之前，上一个 effect 就已被清除。**此处需要传入一个空的数组作为依赖项，这样就只会在函数挂载时执行，如果返回一个函数，会在卸载时执行返回的函数。
  - useEffect 如果返回一个函数的话，该函数会在组件卸载和更新时调用       
  -  useEffect 在执行副作用函数之前，会先调用上一次返回的函数        
  - 如果要清除副作用，要么返回一个清除副作用的函数
- **跳过 effect 进行性能优化：**使用传入的数组对于useEffect进行优化，当依赖某一个状态时，只有状态发生了改变，effect才会被调用。
- **使用多个 Effect 实现关注点分离：**使用 Hook 其中一个目的就是要解决 class 中生命周期函数经常包含不相关的逻辑，但又把相关逻辑分离到了几个不同方法中的问题。



#### useLayoutEffcet:

- **useEffect 在全部渲染完毕后才会执行**

- **useLayoutEffect 会在 浏览器 layout 之后，painting 之前执行**

- 其函数签名与 useEffect 相同，但它会在所有的 DOM 变更之后**同步**调用 effect

- **可以使用它来读取 DOM 布局并同步触发重渲染**

- 在浏览器执行绘制之前 useLayoutEffect 内部的更新计划将被**同步**刷新

- **尽可能使用标准的 useEffect 以避免阻塞视图更新**

#### **useRef**：



## Fetch与axios和ajax的区别

​	传统 Ajax 指的是 XMLHttpRequest（XHR），最早出现的发送后端请求技术，隶属于原始 js 中，核心使用 XMLHttpRequest 对象，多个请求之间如果有先后关系的话，就会出现回调地狱。JQuery ajax 是对原生 XHR 的封装

- axios 是一个基于 Promise ，本质上也是对原生 XHR 的封装，只不过它是Promise 的实现版本，符合最新的 ES 规范，

- fetch 不是 ajax 的进一步封装，而是原生 js，没有使用 XMLHttpRequest 对象。

##  HOC高阶组件：

- 参数是组件，且返回值也是组件，（习惯命名以with开始）

- 作用：

  - 封装可以在组件中高度复用的代码

  - 高阶组件 HOC 接收 props：如果组件是被高阶组件导出的那么在正向传值的时候需要在高阶组件中进行

    传递

  - 反向继承：作用：渲染劫持，按照条件选择性的给用户输出想要的内容;super.render()是调用父类的 render()渲染

