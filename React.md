# React Manual



React is a JavaScript library for building user interfaces, primarily for building UIs.

React originated as an internal project at Facebook and has high performance and simple code logic.

React 是一个用于构建用户界面的 JavaScript 库， 主要用于构建UI。

React 起源于 Facebook 的内部项目， 拥有较高的性能，代码逻辑简单。

# 1 引入 Import

Staticfile CDN (Chinese developers can use them)

```html
<script src="https://cdn.staticfile.org/react/16.4.0/umd/react.development.js"></script>
<script src="https://cdn.staticfile.org/react-dom/16.4.0/umd/react-dom.development.js"></script>
```

Official

```html
<script src="https://unpkg.com/react@16/umd/react.development.js"></script>
<script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
```

---

# 2 实例 Simple eg.

Hello World

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8" />
<title>Hello React!</title>
<script src="https://cdn.staticfile.org/react/16.4.0/umd/react.development.js"></script>
<script src="https://cdn.staticfile.org/react-dom/16.4.0/umd/react-dom.development.js"></script>
<script src="https://cdn.staticfile.org/babel-standalone/6.26.0/babel.min.js"></script>
</head>
<body>
 
<div id="example"></div>
<script type="text/babel">
ReactDOM.render(
    <h1>Hello, world!</h1>,
    document.getElementById('example')
);
</script>
 
</body>
</html>
```

**实例解析：**

react.min.js 、react-dom.min.js & babel.min.js are needed:

- **React.min.js ** -React core library
- **react-dom.min.js** - Provides DOM-related functionality
- **babel.min.js** - Babel can convert ES6 code to ES5 code so that we can execute React code on browsers that currently do not support ES6. Babel has built-in support for JSX.



实例中我们引入了三个库： react.min.js 、react-dom.min.js 和 babel.min.js：

- **react.min.js** - React 的核心库
- **react-dom.min.js** - 提供与 DOM 相关的功能
- **babel.min.js** - Babel 可以将 ES6 代码转为 ES5 代码，这样我们就能在目前不支持 ES6 浏览器上执行 React 代码。Babel 内嵌了对 JSX 的支持。

```javascript
ReactDOM.render(
    <h1>Hello, world!</h1>,
    document.getElementById('example')
);
```

This code inserts an h1 header into the node id="example".

以上代码将一个 h1 标题，插入 id="example" 节点中。

# 3 元素渲染 Element Render

The element is the smallest unit that makes up the React application and is used to output on the screen.

元素是构成 React 应用的最小单位，它用于描述屏幕上输出的内容。

```javascript
const element = <h1>Hello, world!</h1>;
```



Unlike browser DOM elements, React elements are actually normal objects. The React DOM ensures that the data content of the browser DOM is consistent with the React element.

与浏览器的 DOM 元素不同，React 当中的元素事实上是普通的对象，React DOM 可以确保 浏览器 DOM 的数据内容与 React 元素保持一致。



**渲染 Render elements into the DOM**

First，we add a **<div>** in an HTML page:

首先我们在一个 HTML 页面中添加一个 **id="example"** 的 **<div>**:

```html
<div id="example"></div>
```

Everything in this div will be managed by the React DOM, so we call it the "root" DOM node.

此 div 中的所有内容都将由 React DOM 来管理，所以我们将其称为 "根" DOM 节点。



When we develop applications with React, we typically define only one root node. However, if you are introducing React in an existing project, you may need to define the React root node separately in a different section.

我们用 React 开发应用时一般只会定义一个根节点。但如果你是在一个已有的项目当中引入 React 的话，你可能会需要在不同的部分单独定义 React 根节点。



To render the React element to the root DOM node, we render it to the page by passing them all to **ReactDOM.render ()** :

要将React元素渲染到根DOM节点中，我们通过把它们都传递给 **ReactDOM.render()** 的方法来将其渲染到页面上：

```javascript
const element = <h1>Hello, world!</h1>;
ReactDOM.render(
    element,
    document.getElementById('example')
);
```



**更新元素渲染 Refresh render**

The React elements are immutable. Once an element has been created, you cannot change its content or properties.

React 元素都是不可变的。当元素被创建之后，你是无法改变其内容或属性的。



Currently, the only way to update the interface is to ==create a new element== and pass it to the ReactDOM.render () method:

目前更新界面的唯一办法是==创建一个新的元素==，然后将它传入 ReactDOM.render() 方法：

```javascript
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>现在是 {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(
    element,
    document.getElementById('example')
  );
}
 
setInterval(tick, 1000); // js间歇调用，直到被取消或者卸载
```



**完整实例 Full instance：**

==Wath out for "text/babel" type in script tag==

==注意脚本部分有样式type="text/babel"==

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8" />
<title>Hello React!</title>
<script src="https://cdn.staticfile.org/react/16.4.0/umd/react.development.js"></script>
<script src="https://cdn.staticfile.org/react-dom/16.4.0/umd/react-dom.development.js"></script>
<script src="https://cdn.staticfile.org/babel-standalone/6.26.0/babel.min.js"></script>
</head>
<body>

<div id="example"></div>
<script type="text/babel">
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>现在是 {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(
    element,
    document.getElementById('example')
  );
}
 
setInterval(tick, 1000);
</script>

</body>
</html>
```

![image-20210304174719807](/Users/shaotienlee/Desktop/Study/Notes/React.assets/image-20210304174719807.png)



As you can see, **React only updates the necessary parts**

React **只更新必要部分**



It's worth noting that React Dom first compares the sequence of elements, and only updates the parts that have changed during rendering.

值得注意的是 React DOM 首先会比较元素内容先后的不同，而在渲染过程中只会更新改变了的部分。



**ES 6 Element Declaration**

We can create an ES6 class that encapsulates the elements to be presented. Note that in the render() method, we need to replace **props** with **this.props** :

除了函数外我们还可以创建一个 React.Component 的 ES6 类，该类封装了要展示的元素，需要注意的是在 render() 方法中，需要使用 **this.props** 替换 **props**：

```javascript
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>现在是 {this.props.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
 
function tick() {
  ReactDOM.render(
    <Clock date={new Date()} />,
    document.getElementById('example')
  );
}
 
setInterval(tick, 1000);
```

---

# 4 React JSX

React replaces regular JavaScript with JSX, which is a JavaScript syntax extension that looks a lot like XML. It has the following advantages:

- JSX executes faster because it is optimized after compiling into JavaScript code.
- It is type-safe and detects errors during compilation.
- Using JSX to write templates is easier and faster.

React 使用 JSX 来替代常规的 JavaScript,JSX 是一个看起来很像 XML 的 JavaScript 语法扩展。它有以下优点：

- JSX 执行更快，因为它在编译为 JavaScript 代码后进行了优化。
- 它是类型安全的，在编译过程中就能发现错误。
- 使用 JSX 编写模板更加简单快速。

```javascript
const element2 = <h1>Hello, world!</h1>;
```

This is called JSX, a syntax extension to JavaScript. We recommend using JSX in React to describe the user interface. ==Multiple tags are wrapped in a tag div==

这种看起来可能有些奇怪被称为 JSX， 一种 JavaScript 的语法扩展。 我们推荐在 React 中使用 JSX 来描述用户界面。==多个标签要用一个大div包裹==



JSX is implemented inside JavaScript.

JSX 是在 JavaScript 内部实现的。

Elements are the smallest units that make up the React application, and JSX is used to declare React elements.

元素是构成 React 应用的最小单位，JSX 就是用来声明 React 当中的元素。



Unlike browser DOM elements, React elements are actually normal objects. The React DOM ensures that the data content of the browser DOM is consistent with the React element.

与浏览器的 DOM 元素不同，React 当中的元素事实上是普通的对象，React DOM 可以确保 浏览器 DOM 的数据内容与 React 元素保持一致。



To render the React element to the root DOM node, we render it to the page by passing them all to ReactDOM.render () :

要将 React 元素渲染到根 DOM 节点中，我们通过把它们都传递给 ReactDOM.render() 的方法来将其渲染到页面上：

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8" />
<title>React 实例</title>
<script src="https://cdn.staticfile.org/react/16.4.0/umd/react.development.js"></script>
<script src="https://cdn.staticfile.org/react-dom/16.4.0/umd/react-dom.development.js"></script>
<script src="https://cdn.staticfile.org/babel-standalone/6.26.0/babel.min.js"></script>
<style>
.foo{
	color:red;
}
</style>
</head>
<body>
	<div id="root"></div>
  
	<script type="text/babel">
	const element = <h1 className="foo">Hello, world</h1>;
	ReactDOM.render(element, document.getElementById('root'));
	</script>
</body>
</html>
```

![image-20210304180528615](/Users/shaotienlee/Desktop/Study/Notes/React.assets/image-20210304180528615.png)

## Using JSX

```javascript
ReactDOM.render(
    <h1>Hello, world!</h1>,
    document.getElementById('example')
);
```

To nested multiple HTML tags in the above code, ==a div tag is needed==, the p element in the instance has the custom attribute **data-myAttribute **, and the custom attribute needs to be prefixed with **data-**.

在以上代码中嵌套多个 HTML 标签，==需要使用一个 div 元素包裹它==，实例中的 p 元素添加了自定义属性 **data-myattribute**，添加自定义属性需要使用 **data-** 前缀。

```javascript
ReactDOM.render(
    <div>
    <h1>Learn</h1>
    <h2>React</h2>
    <p data-myattribute = "somevalue">这是一个很不错的 JavaScript 库!</p>
    </div>
    ,
    document.getElementById('example')
);
```

**独立文件 Linking**

The React JSX code can be placed in a separate file. For example, we create a `helloworld_react.js` file with the following code: 

React JSX 代码可以放在一个独立文件上，例如我们创建一个 `helloworld_react.js` 文件，代码如下：

```javascript
ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('example')
);
```

Then link the JS file in the HTML file:

然后在 HTML 文件中引入该 JS 文件：

```html
<body>
  <div id="example"></div>
<script type="text/babel" src="helloworld_react.js"></script>
</body>
```

## JavaScript expression

We can use JavaScript expressions in JSX. The expression is written in  **{}**. Examples are as follows:

我们可以在 JSX 中使用 JavaScript 表达式。表达式写在花括号 **{}** 中。实例如下：

```javascript
ReactDOM.render(
    <div>
      <h1>{1+1}</h1>
    </div>
    ,
    document.getElementById('example')
);
```

### 条件 Condition

You cannot use **if else** statements, but you can use **conditional (ternary operation)** expressions instead. In the following example, the browser will print **true** if the variable **i** is **1**, or **false** if you change the value of **i**.

不能使用 **if else** 语句，但可以使用 **conditional (三元运算)** 表达式来替代。以下实例中如果变量 **i** 等于 **1** 浏览器将输出 **true**, 如果修改 **i** 的值，则会输出 **false**.

```javascript
ReactDOM.render(
    <div>
      <h1>{i == 1 ? 'True!' : 'False'}</h1>
    </div>
    ,
    document.getElementById('example')
);
```

### 样式 Type

React recommends using inline styles. We can use the **camelCase** syntax to set inline styles. React automatically adds **px** after specifying element numbers. The following example demonstrates adding **myStyle** inline to the **h1** element:

React 推荐使用内联样式。我们可以使用 **camelCase** 语法来设置内联样式. React 会在指定元素数字后自动添加 **px** 。以下实例演示了为 **h1** 元素添加 **myStyle** 内联样式：

```javascript
var myStyle = {
    fontSize: 100,
    color: '#FF0000'
};
ReactDOM.render(
    <h1 style = {myStyle}>words</h1>,
    document.getElementById('example')
);
```

### 注释 Comments

```javascript
ReactDOM.render(
    <div>
    <h1>cocococ</h1>
    {/*comments...*/}
     </div>,
    document.getElementById('example')
);
```

### 数组 Arrays

The array automatically expands all the members:

```javascript
var arr = [
  <h1>菜鸟教程</h1>,
  <h2>这个网站不错</h2>,
];
ReactDOM.render(
  <div>{arr}</div>,
  document.getElementById('example')
);
```

# 5 React Component

Wrap a component that outputs "Hello World!", called HelloMessage:

接下来我们封装一个输出 "Hello World！" 的组件，组件名为 HelloMessage：

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8" />
<title>React 组件实例</title>
<script src="https://cdn.staticfile.org/react/16.4.0/umd/react.development.js"></script>
<script src="https://cdn.staticfile.org/react-dom/16.4.0/umd/react-dom.development.js"></script>
<script src="https://cdn.staticfile.org/babel-standalone/6.26.0/babel.min.js"></script>
</head>
<body>

<div id="example"></div>
  
<script type="text/babel">
function HelloMessage(props) {
	return <h1>Hello World!</h1>;
}

const element = <HelloMessage />;

ReactDOM.render(
	element,
	document.getElementById('example')
);
</script>

</body>
</html>
```

*解析*

1. 使用函数定义了一个组件 defined a component：

   ``` javascript
   function HelloMessage(props) {
     return <h1>Hello World </h1>;
   }
   ```

   It is also possible to use ES6 classes to define components. Note that in the render() method, you need to use **this.props** instead of **props**

   也可以用ES6 的Class来定义组件,需要注意的是在 render() 方法中，需要使用 **this.props** 替换 **props**

   ```javascript
   class Welcome extends React.Component {
     render() {
       return <h1>Hello World!</h1>;
     }
   }
   ```

2. **const element = <HelloMessage />**   是 custom component

   *Note that native HTML element names begin with lowercase letters, while custom React class names begin with uppercase letters, such as HelloMessage cannot be written as HelloMessage. Also note that the component class can contain only one top-level tag, otherwise it will report an error.*

   *注意，原生 HTML 元素名以小写字母开头，而自定义的 React 类名以大写字母开头，比如 HelloMessage 不能写成 helloMessage。除此之外还需要注意组件类只能包含一个顶层标签，否则也会报错。*



If you want to pass parameters to a component, you can use the **this.props** object, for example:

如果想要给组件传递参数，可以使用 **this.props** 对象,实例如下：

```javascript
function HelloMessage(props) {
    return <h1>Hello {props.name}!</h1>;
}
 
const element = <HelloMessage name="Dude"/>;
 
ReactDOM.render(
    element,
    document.getElementById('example')
);
```

The **name** attribute in the above example is obtained using **props.name **.

以上实例中 **name** 属性通过 **props.name** 来获取。

> Note: when adding attributes, the *class* attribute needs to be written as *className* , and the *for* attribute needs to be written *htmlFor*, because *class* and *for* are reserved words for JavaScript.

> 注意，在添加属性时， class 属性需要写成 className ，for 属性需要写成 htmlFor ，这是因为 class 和 for 是 JavaScript 的保留字。

---

## 复合组件 composite Components

We can compose a component by creating multiple components, that is, separating the different functional points of the component.

我们可以通过创建多个组件来合成一个组件，即把组件的不同功能点进行分离。



In the following example, we implement a component that outputs the name and address of a website. In the example, the APP component uses the Name, URL, and NICKNAME components to output the corresponding information.

以下实例我们实现了输出网站名字和网址的组件.实例中 App 组件使用了 Name、Url 和 Nickname 组件来输出对应的信息。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>React2</title>
    <script src="https://cdn.staticfile.org/react/16.4.0/umd/react.development.js"></script>
    <script src="https://cdn.staticfile.org/react-dom/16.4.0/umd/react-dom.development.js"></script>
    <script src="https://cdn.staticfile.org/babel-standalone/6.26.0/babel.min.js"></script>
</head>
<body>

<div id="acdc">ERROR</div>

<script type="text/babel">
    class Name extends React.Component {
        render() {
            return <h1>Website Name: {this.props.name}</h1>;
        }
    }

    class Url extends React.Component {
        render() {
            return <h1>Website URL: {this.props.url}</h1>;
        }
    }

    function Nickname(props) {
        return <h1>Website Nickname: {props.nickname}</h1>;
    }

    function App() {
        return (
            <div>
                <Name name="Baidu"/>
                <Url url="www.baidu.com"/>
                <Nickname nickname="百毒"/>
            </div>
        );
    }

    ReactDOM.render(
        <App />,
        document.getElementById('acdc')
    );

</script>

</body>
</html>
```

## 组件生命周期Component Life cycle

As the props or state of a component changes throughout its life cycle, its DOM representation changes as well. A component is a state machine that always returns a consistent output for a particular input.

在组件的整个生命周期中，随着该组件的props或者state发生改变，其DOM表现也会有相应的变化。一个组件就是一个状态机，对于特定地输入，它总返回一致的输出。



The lifecycle of a React component is divided into three parts: **Instance**, **Lifetime**, and **Destruction **.

一个React组件的生命周期分为三个部分：**实例化**、**存在期**和**销毁时**。



### 实例化 Instance

*When the component is instantiated at **client** and is created, the following methods are called in turn:*

*当组件在**客户端**被实例化，第一次被创建时，以下方法依次被调用：*

1、getDefaultProps

> For each component instance, this method is called only once, and for all subsequent applications of the component class, getDefaultPops will not be called again, and the returned object can be used to set the default props(short for properties) values.

> 对于每个组件实例来讲，这个方法只会调用一次，该组件类的所有后续应用，getDefaultPops 将不会再被调用，其返回的对象可以用于设置默认的 props(properties的缩写) 值。

2、getInitialState

> This method **is called once and only once for each instance of the component. ** is used to initialize the state of each instance. In this method, the component props are available. Each React component has its own state, which differs from props in that the state exists only inside the component and props are shared among all instances.

> 对于组件的每个实例来说，这个方法的调用**有且只有一次，**用来初始化每个实例的 state，在这个方法里，可以访问组件的 props。每一个React组件都有自己的 state，其与 props 的区别在于 state只存在组件的内部，props 在所有实例中共享。

3、componentWillMount

> This method is called before the first render and is the last chance to modify the state before the `render` method is called

> 该方法在首次渲染之前调用，也是再 render 方法调用之前修改 state 的最后一次机会

4、render

> This method creates a virtual DOM that represents the output of the component. The render method is the only required method for a component. The result returned by the render method is not a real DOM element, but a virtual representation of an object with a structure similar to that of a DOM Tree. That's why React is efficient.

> 该方法会创建一个虚拟DOM，用来表示组件的输出。对于一个组件来讲，render方法是唯一一个必需的方法。render方法返回的结果并不是真正的DOM元素，而是一个虚拟的表现，类似于一个DOM tree的结构的对象。react之所以效率高，就是这个原因。

5、componentDidMount

> This method will not be called while the server is being rendered. When this method is called, the actual DOM has already been rendered, and you can access the real DOM in this method by using 'this.getDomNode ()' (the recommended use is`reactDom.findDomNode ()`).

> 该方法不会在服务端被渲染的过程中调用。该方法被调用时，已经渲染出真实的 DOM，可以再该方法中通过 `this.getDOMNode()` 访问到真实的 DOM(推荐使用 `ReactDOM.findDOMNode()`)。



When the component is instantiated on **server** and is first created, the following methods are called in turn:

*当组件在**服务端**被实例化，首次被创建时，以下方法依次被调用：*

1、getDefaultProps
2、getInitialState
3、componentWillMount
4、render



ComponentDidMount is not called while the server is being rendered.

componentDidMount 不会在服务端被渲染的过程中调用。



### 存在期 LifeTime

Now, the component is rendered and the user can interact with it, such as a mouse click, or some other event that causes the application state to change, you will see the following methods called in turn

此时组件已经渲染好并且用户可以与它进行交互，比如鼠标点击，手指点按，或者其它的一些事件，导致应用状态的改变，你将会看到下面的方法依次被调用

1、componentWillReceiveProps

> Components of `props` attribute can be changed by the parent component, then `componentWillReceiveProps` is invoked in the future. State can be updated in this method to trigger the render method to re-render the component.

>组件的 props 属性可以通过父组件来更改，这时，componentWillReceiveProps 将来被调用。可以在这个方法里更新 state,以触发 render 方法重新渲染组件。

2、shouldComponentUpdate

> If you're sure that a component's `props` or `state` changes don't require a re-render, you can prevent it from happening in this method by returning `false`, which will not execute render and the subsequent componentWillUpdate, ComponentDidUpdate methods.

>如果你确定组件的 props 或者 state 的改变不需要重新渲染，可以通过在这个方法里通过返回 `false` 来阻止组件的重新渲染，返回 `false 则不会执行 render 以及后面的 componentWillUpdate，componentDidUpdate 方法。

3、componentWillUpdate

> This method is similar to `ComponentWillMount`. `ComponentWillUpdate` (object nextState, object nextState) is called before a component receives props or states that are about to be re-rendered. **Be sure not to update props or states in this method. **

>这个方法和 componentWillMount 类似，在组件接收到了新的 props 或者 state 即将进行重新渲染前，componentWillUpdate(object nextProps, object nextState) 会被调用，**注意不要在此方法里再去更新 props 或者 state。**

4、render

> same

5、componentDidUpdate

> This method is similar to `ComponentDidMount` in that after the component is re-rendered, ComponentDidUpdate (Object prevState, Object prevState) will be called. You can access and modify the DOM here.

>这个方法和 componentDidMount 类似，在组件重新被渲染之后，componentDidUpdate(object prevProps, object prevState) 会被调用。可以在这里访问并修改 DOM。

### 销毁时 Destruction

Whenever React finishes using a component, the component must be unmounted from the DOM and then destroyed. The ==componentWillUnmount== hook function is executed to do all the cleanup and destruction. Any tasks added to `ComponentDidMount`, such as the created timer or event listener, need to be unmounted in this method.

每当React使用完一个组件，这个组件必须从 DOM 中卸载后被销毁，此时 ==componentWillUnmount== 钩子函数会被执行，完成所有的清理和销毁工作，在 componentDidMount 中添加的任务都需要在该方法中撤销，如创建的定时器或事件监听器。

当再次装载组件时，以下方法会被依次调用：

1、getInitialState
2、componentWillMount
3、render
4、componentDidMount

![image-20210307121747905](/Users/shaotienlee/Desktop/Study/Notes/React.assets/image-20210307121747905.png)

---

# 6 React State

React treats components as State Machines. By interacting with the user, achieving different states, and then rendering the UI to keep the user interface and data consistent.

React 把组件看成是一个状态机（State Machines）。通过与用户的交互，实现不同状态，然后渲染 UI，让用户界面和数据保持一致。



In React, just update the component's state and then re-render the user interface based on the new state (without manipulating the DOM).

React 里，只需更新组件的 state，然后根据新的 state 重新渲染用户界面（不要操作 DOM）。



The following example creates an ES6 class with the name extended to `React.Component` and uses `this.state` in the `render()` method to modify the current time. Add a class constructor to initialize the `this.state` state. The class component should always call the base constructor using props.

以下实例创建一个名称扩展为 React.Component 的 ES6 类，在 render() 方法中使用 this.state 来修改当前的时间。添加一个类构造函数来初始化状态 this.state，类组件应始终使用 props 调用基础构造函数。

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8" />
<title>Hello React!</title>
<script src="https://cdn.staticfile.org/react/16.4.0/umd/react.development.js"></script>
<script src="https://cdn.staticfile.org/react-dom/16.4.0/umd/react-dom.development.js"></script>
<script src="https://cdn.staticfile.org/babel-standalone/6.26.0/babel.min.js"></script>
</head>
<body>

<div id="example"></div>
<script type="text/babel">
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>现在是 {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('example')
);
</script>

</body>
</html>
```



Next, we'll make Clock set its own timer and update it every second.

接下来，我们将使Clock设置自己的计时器并每秒更新一次。

## 将生命周期方法添加到类中 Using LifeCycle Hook 

In applications with many components, it is important to release the resources that the components occupy during destruction.

在具有许多组件的应用程序中，在销毁时释放组件所占用的资源非常重要。



We want to generate timers every time a `Clock` component is first loaded into the DOM, which in React is called **mount **. Similarly, whenever the `Clock` generated DOM is removed, we also want to clear the timer, which in React is called **Unimount**.

每当 Clock 组件第一次加载到 DOM 中的时候，我们都想生成定时器，这在 React 中被称为**挂载**。同样，每当 Clock 生成的这个 DOM 被移除的时候，我们也会想要清除定时器，这在 React 中被称为**卸载**。



We can declare special methods on our component classes to run some code when the component is mounted or unmounted:

我们可以在组件类上声明特殊的方法，当组件挂载或卸载时，来运行一些代码：

```javascript
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
 
  componentDidMount() {
    this.timerID = setInterval(
      // Arrow func，equals function() {return this.tick();}
      () => this.tick(),
      1000
    );
  }
 
  componentWillUnmount() {
    clearInterval(this.timerID);
  }
 
  tick() {
    this.setState({
      date: new Date()
    });
  }
 
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>Now is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
 
ReactDOM.render(
  <Clock />,
  document.getElementById('example')
);
```

**实例解析：**

**ComponentDidMount ()** and **ComponentWillUnMount ()** methods are called lifecycle hooks.

**componentDidMount()** 与 **componentWillUnmount()** 方法被称作生命周期钩子。



The **ComponentDidMount ()** hook is executed after the component outputs to the DOM, and we can set a timer on this hook. `this.TimerID` is the ID of the timer. We can unmount the timer in **ComponentWillUnmount ()** hook.

在组件输出到 DOM 后会执行 **componentDidMount()** 钩子，我们就可以在这个钩子上设置一个定时器。this.timerID 为定时器的 ID，我们可以在 **componentWillUnmount()** 钩子中卸载定时器。



**代码执行顺序 Execution Sequence：**

1. When `<Clock />` is passed to `ReactDOM.render ()`, React calls the constructor of the `Clock` component. Since `Clock` needs to display the current time, `this.state` is initialized using an object that contains the current time. We will update this status later.
2. React then calls the `Clock` component's `render()` method. This is for knowing what should be displayed on the screen, and then React updating the DOM to match the `Clock` rendering output.
3. React calls the `ComponentDidMount ()` lifecycle hook when the output of `Clock` is inserted into the DOM. The `Clock` component asks the browser to set a timer that calls `tick()` once a second.
4. The browser calls the `tick()` method every second. The `Clock` component schedules UI updates by calling `setState()` with an object containing the current time. By calling `setState()`, React knows that the state has changed and calls the `render()` method again to determine what should be displayed on the screen. This time, `this.state.date` in the `render()` method will be different, so the render output will contain the updated time and update the DOM accordingly.
5. Once the `Clock` component is removed from the DOM, React calls the `componentWillunmount ()` hook function and the timer is cleared.

1. 当 `<Clock />` 被传递给 `ReactDOM.render()` 时，React 调用 `Clock` 组件的构造函数。 由于 `Clock` 需要显示当前时间，所以使用包含当前时间的对象来初始化 `this.state` 。 我们稍后会更新此状态。
2. React 然后调用 `Clock` 组件的 `render()` 方法。这是 React 了解屏幕上应该显示什么内容，然后 React 更新 DOM 以匹配 `Clock` 的渲染输出。
3. 当 `Clock` 的输出插入到 DOM 中时，React 调用 `componentDidMount()` 生命周期钩子。 在其中，`Clock` 组件要求浏览器设置一个定时器，每秒钟调用一次 `tick()`。
4. 浏览器每秒钟调用 `tick()` 方法。 在其中，`Clock` 组件通过使用包含当前时间的对象调用 `setState()` 来调度UI更新。 通过调用 `setState()` ，React 知道状态已经改变，并再次调用 `render()` 方法来确定屏幕上应当显示什么。 这一次，`render()` 方法中的 `this.state.date` 将不同，所以渲染输出将包含更新的时间，并相应地更新 DOM。
5. 一旦 `Clock` 组件被从 DOM 中移除，React 会调用 `componentWillUnmount()` 这个钩子函数，定时器也就会被清除。



## 数据自顶向下流动 Top-Down

Neither the parent nor the child can know whether a component is stateful or stateless, and they should not care whether a component is defined as a function or a class.

父组件或子组件都不能知道某个组件是有状态还是无状态，并且它们不应该关心某组件是被定义为一个函数还是一个类。



This is why states are often referred to as local or encapsulated. Components are not accessible except for the component that owns and sets it. Any state is always owned by some specific component, and any data or UI exported from that state can only affect components lower in the tree.

这就是为什么状态通常被称为局部或封装。 除了拥有并设置它的组件外，其它组件不可访问。（任何状态始终由某些特定组件所有，并且从该状态导出的任何数据或 UI 只能影响树中下方的组件）



Each Clock component in the following example sets up its own timer and updates it independently.

以下实例中每个 Clock 组件都建立了自己的定时器，并且独立更新。

```javascript
function FormattedDate(props) {
  return <h2>现在是 {props.date.toLocaleTimeString()}.</h2>;
}
 
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
 
  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }
 
  componentWillUnmount() {
    clearInterval(this.timerID);
  }
 
  tick() {
    this.setState({
      date: new Date()
    });
  }
 
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <FormattedDate date={this.state.date} />
      </div>
    );
  }
}
 
function App() {
  return (
    <div>
      <Clock />
      <Clock />
      <Clock />
    </div>
  );
}
 
ReactDOM.render(<App />, document.getElementById('example'));
```

---

# 7 React Props

The main difference between state and props is that **props** is immutable, whereas **state** can be changed depending on interaction with the user. This is why some container components need to define a state to update and modify data. Child components can only pass data through props.

state 和 props 主要的区别在于 **props** 是不可变的，而 **state** 可以根据与用户交互来改变。这就是为什么有些容器组件需要定义 state 来更新和修改数据。 而子组件只能通过 props 来传递数据。

## using props

```javascript
function HelloMessage(props) {
    return <h1>Hello {props.name}!</h1>;
}
 
const element = <HelloMessage name="Dude"/>;
 
ReactDOM.render(
    element,
    document.getElementById('example')
);
```

## 默认 default props

```javascript
class HelloMessage extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}
 
HelloMessage.defaultProps = {
  name: 'dude'
};
 
const element = <HelloMessage/>;
 
ReactDOM.render(
  element,
  document.getElementById('example')
);
```

## State & Props

 Try to combine the two above, the following example sets *state* in the parent component and passes it to the child component by using *props* on the child component. In the *render* function, we set the name and site to get the data passed by the parent component.

我试一试组合这两个，下面例子在父组件中设置 state， 并通过在子组件上使用 props 将其传递到子组件上。在 render 函数中, 我们设置 name 和 site 来获取父组件传递过来的数据。

```javascript
class WebSite extends React.Component {
  constructor() {
      super();
 
      this.state = {
        name: "baidu",
        site: "https://www.baidu.com"
      }
    }
  render() {
    return (
      <div>
        <Name name={this.state.name} />
        <Link site={this.state.site} />
      </div>
    );
  }
}
 
 
 
class Name extends React.Component {
  render() {
    return (
      <h1>{this.props.name}</h1>
    );
  }
}
 
class Link extends React.Component {
  render() {
    return (
      <a href={this.props.site}>
        {this.props.site}
      </a>
    );
  }
}
 
ReactDOM.render(
  <WebSite />,
  document.getElementById('example')
);
```

## 验证 Props validator

==Need import==

```html
<script src="https://cdn.bootcss.com/prop-types/15.6.1/prop-types.js"></script>
```

Props validation uses **propTypes**, which ensure that our application components are being used correctly. *React.Proptypes* provide many validators to verify that the incoming data is valid. When invalid data is passed to props, the JavaScript console throws a warning.

The following example creates a *Testing* component. The property title is required and is a string. Non-string types are automatically converted to strings:

Props 验证使用 **propTypes**，它可以保证我们的应用组件被正确使用，React.PropTypes 提供很多验证器 (validator) 来验证传入数据是否有效。当向 props 传入无效数据时，JavaScript 控制台会抛出警告。

以下实例创建一个 Mytitle 组件，属性 title 是必须的且是字符串，非字符串类型会自动转换为字符串 ：

```javascript
var title = "Testing";
class MyTitle extends React.Component {
  render() {
    return (
    	<h1>hello, {this.props.title} </h1>
    );
  }
}

MyTitle.propTypes = {
  title: PropTypes.string
};

ReactDOM.render(
	<Testing title={title} />,
	document.getElementById('example')
);
```



**More validators**

```javascript
MyComponent.propTypes = {
    // 可以声明 prop 为指定的 JS 基本数据类型，默认情况，这些数据是可选的
    // You can declare prop as the specified JS primitive data type. 				// by default, this is optional
    optionalArray: React.PropTypes.array,
    optionalBool: React.PropTypes.bool,
    optionalFunc: React.PropTypes.func,
    optionalNumber: React.PropTypes.number,
    optionalObject: React.PropTypes.object,
    optionalString: React.PropTypes.string,
 
    // Objects that can be rendered: numbers, strings, elements or array
    optionalNode: React.PropTypes.node,
 
    //  React elements
    optionalElement: React.PropTypes.element,
 
    // 用 JS 的 instanceof 操作符声明 prop 为类的实例。
    // Declare prop using instanceof operator in JS.
    optionalMessage: React.PropTypes.instanceOf(Message),
 
    // enum restriction
    optionalEnum: React.PropTypes.oneOf(['News', 'Photos']),
 
    // Can be one of multiple object types
    optionalUnion: React.PropTypes.oneOfType([
      React.PropTypes.string,
      React.PropTypes.number,
      React.PropTypes.instanceOf(Message)
    ]),
 
    // Specifies type of the array
    optionalArrayOf: React.PropTypes.arrayOf(React.PropTypes.number),
 
    // 指定类型的属性构成的对象
    // Specifies the type of properties
    optionalObjectOf: React.PropTypes.objectOf(React.PropTypes.number),
 
    // 特定 shape 参数的对象
    // Specifies the shape params
    optionalObjectWithShape: React.PropTypes.shape({
      color: React.PropTypes.string,
      fontSize: React.PropTypes.number
    }),
 
    // add `isRequired` to make prop NOT NULL.
    requiredFunc: React.PropTypes.func.isRequired,
 
    // NOT NULL for every types
    requiredAny: React.PropTypes.any.isRequired,
 
    // 自定义验证器。如果验证失败需要返回一个 Error 对象。不要直接使用 `console.warn` 或抛异常，因为这样 `oneOfType` 会失效。
    // Cumstom validator. If match failure occurs, it will return an error object.
    customProp: function(props, propName, componentName) {
      if (!/matchme/.test(props[propName])) {
        return new Error('Validation failed!');
      }
    }
  }
}
```

---

# 8 事件处理 Event Handler

The React element handles events similar to the DOM element. But there is a slight grammatical difference:

- The React event binding property is named humped instead of lowercase.
- If you use JSX syntax, you need to pass in a function as an event handler, rather than a string.



React 元素的事件处理和 DOM 元素类似。但是有一点语法上的不同:

- React 事件绑定属性的命名采用驼峰式写法，而不是小写。
- 如果采用 JSX 的语法你需要传入一个函数作为事件处理函数，而不是一个字符串(DOM 元素的写法)

```html
<!-- HTML -->
<button onclick="activateLasers()">
  button activited
</button>

<!--React-->
<button onClick={activateLasers}>
  button activited
</button>
```



Another difference in React is that you can't block the default behavior by returning **false**. You must explicitly use **preventDefault**. For example, we normally block links in HTML from opening a new page by default. We could write something like this:

在 React 中另一个不同是你不能使用返回 **false** 的方式阻止默认行为， 你必须明确使用 **preventDefault**。例如，通常我们在 HTML 中阻止链接默认打开一个新页面，可以这样写：

```html
<!-- HTML -->
<a href="#" onclick="console.log('click'); return false">
  hit me
</a>

```

In React, `e` in the example is a composite event.

```javascript
function ActionLink() {
  function handleClick(e) {
    e.preventDefault();
    console.log('clicked');
  }
 
  return (
    <a href="#" onClick={handleClick}>
      hit me
    </a>
  );
}
```



When using React you usually don't need to use an `addEventListener` to add a listener to a DOM element that has been created. You only need to provide a listener when the element is initially rendered.

When you define a component using ES6 Class syntax, the event handler becomes a method of the class. For example, the following Toggle component renders a button that lets the user Toggle between switch states:

使用 React 的时候通常你不需要使用 `addEventListener` 为一个已创建的 DOM 元素添加监听器。你仅仅需要在这个元素初始渲染的时候提供一个监听器。

当你使用 ES6 class 语法来定义一个组件的时候，事件处理器会成为类的一个方法。例如，下面的 Toggle 组件渲染一个让用户切换开关状态的按钮：

```javascript
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};
 
    // 这边绑定是必要的，这样 `this` 才能在回调函数中使用
    // the binding over here is necessary，so that `this` can be used in call-back function
    this.handleClick = this.handleClick.bind(this);
  }
 
  handleClick() {
    this.setState(prevState => ({
      isToggleOn: !prevState.isToggleOn
    }));
  }
 
  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}
 
ReactDOM.render(
  <Toggle />,
  document.getElementById('example')
);
```

You have to be careful with 'this' in JSX callbacks. Class methods do not bind' this' by default. If you forget to bind 'this.handleClick' and pass it to 'onClick', the value of 'this' will be' undefined 'when you call this function.

你必须谨慎对待 JSX 回调函数中的 `this`，类的方法默认是不会绑定 `this` 的。如果你忘记绑定 `this.handleClick` 并把它传入 `onClick`, 当你调用这个函数的时候 `this` 的值会是 `undefined`。



To solve the problem above, we can:

```javascript
class LoggingButton extends React.Component {
  handleClick() {
    console.log('this is:', this);
  }
 
  render() {
    //  这个语法确保了 `this` 绑定在  handleClick 中
    // Ensure that 'this' is bound to handleClick
    return (
      <button onClick={(e) => this.handleClick(e)}>
        Click me
      </button>
    );
  }
}
```



**向事件处理程序传递参数** 

Usually we pass extra parameters to the event handler. For example, if the id is the id of the row you want to delete, you can pass arguments to the event handler either way:

通常我们会为事件处理程序传递额外的参数。例如，若是 id 是你要删除那一行的 id，以下两种方式都可以向事件处理程序传递参数：

```javascript
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```

In both examples, the parameter e as the React event object will be passed as the second parameter. Event objects must be passed explicitly through arrow functions, but with bind, event objects and more arguments are passed implicitly.

上面两个例子中，参数 e 作为 React 事件对象将会被作为第二个参数进行传递。通过箭头函数的方式，事件对象必须显式的进行传递，但是通过 bind 的方式，事件对象以及更多的参数将会被隐式的进行传递。



Note that the arguments to the listener are passed via bind. For listeners defined in class components, the event object e is passed after the arguments, for example:

值得注意的是，通过 bind 方式向监听函数传参，在类组件中定义的监听函数，事件对象 e 要排在所传递参数的后面，例如:

```javascript
class Popper extends React.Component{
    constructor(){
        super();
        this.state = {name:'Hello world!'};
    }
    
    preventPop(name, e){    
        e.preventDefault();
        alert(name);
    }
    
    render(){
        return (
            <div>
                <p>hello</p>
                {/* The parameters are passed through the bind() method */}
                <a href="https://reactjs.org" onClick={this.preventPop.bind(this,this.state.name)}>Click</a>
            </div>
        );
    }
}
```

