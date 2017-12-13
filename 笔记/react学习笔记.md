## React

[TOC]

### React的特点

1. 只作为 UI（Just the UI）：React 不是一个完整的 MVC 框架，最多是作为视图（View）在 MVC 中使用。（甚至 React 并不非常认可 MVC 开发模式。它提出的是一个新的开发模式和理念，强调的是“用户界面”。React 希望将功能分解化，让开发变得像搭积木一样，快速且可维护。）
2. 虚拟 DOM 机制（Virtual DOM）：这是 React 的一个亮点，可以很好地优化视图的渲染和刷新。过去我们更新视图是，需要先清空 DOM 容器里的内容，然后将最新的 DOM 和数据追加到容器中。而 React 将这一操作放进了内存。通过将视图变化放进内存进行比较（虚拟 DOM 比较），计算出最小更新的视图，然后将差异部分进行更新以完成整个组件的渲染。这正是React 如此高效的原因。
3. 数据流（Data Flow）：React 实现了单向的数据流，并且对于传统的数据绑定而言，React 更加灵活、便捷。

### React安装和准备

`npm install -g create-react-app`   **全局安装**

`create-react-app 项目名称`  **创建项目**

`npm start`  **运行**

在使用 ReactJS 进行开发前，我们需要准备好这三个 js 文件：react.js、react-dom.js、browser.js。下面分别对它们进行介绍

**1.react.js 和 react-dom.js**

前者是 React 主要核心，后者负责 React DOM 操作

**2.browser.js **

实现浏览器端对 JSX 的编译。（在 react 0.14 前，使用 jsxtransformer.js，后改为 browser.js）

### JSX简介及语法

1. JSX 即 JavaScript XML，是一种在 React 组件内部构建标签的类 XML 语法
2. JSX 并不是一门新的语言，仅仅是个语法糖（syntactic sugar），允许开发者在 JavaScript 中书写 HTML 语法。最后，每个 HTML 标签都转化为 JavaScript 代码来运行
3. 这样对于使用 JavaScript 来构建组件以及组件之间关系的应用，在代码层面显得更加清晰。而不再像过于一样用JavsScript 操作 DOM 来创建组件以及组件之间的嵌套关系

####运行环境

`JSX 必须借助 ReactJS 环境才能运行，所以使用前要先加载 ReactJS 文件（react.js、react-dom.js）`

`除了 ReactJS 环境，还需要加载 JSX 的解析器（browser.js）`

#### 载入方式

**JSX目前有两种方法载入**

- 内联方式载入

  ```javascript
  <script type="text/babel">
    //注意：type类型必须为 text/babel
      ReactDOM.render(
        <h1>hello hangge.com</h1>,
        document.getElementById('example')
      );
  </script>
  ```

- 外联方式

  ```javascript
  <script type="text/babel" src="hello.jsx"></script>
  ```

#### 标签的使用

我们除了可以在 JavaScript 中书写 HTML 标签外（不需要像以前那样做为字符串用引号引起来）。还可以使用那些由 ReactJS 创建的组件类标签

```javascript
var Hello = React.createClass({
    render: function() {
        return <div>Hello Word</div>;
    }
});
ReactDOM.render(
     <Hello />,
     document.getElementById('example')
);
```

上面的代码中，创建了一个叫 Hello 的组件，此时我们就可以像使用 HTML 标签一样，通过 <Hello/> 的方式把它引入进来

**注意：ReactJS中自定义的组件首字母一定要大写,HTML标签用小写**

#### 执行JavaScript表达式

在 JSX 中运行 JavaScript 表达式，需要将表达式用 {} 括起来

#### 样式的使用

- JSX 中的样式是通过 style 属性定义的。和传统 Web 定义不同的是，它不再是一个字符串而是一个 JavaScript 对象。

  比如下面样例，第一个大括号表示是 JSX 语法，第二个大括号是 JavaScript 对象

  ```javascript
  <div style={{color:'#ff00ff', fontSize: '20px'}}>Hello React</div>
  ```

- 对于属性名要转为驼峰命名格式，如果不想转的话，则需要加引号括起来。比如：**'font-size':'20px'**

- 也可以通过 className='xxx' 的方式引入样式。（切记是 className 而不是 class）

#### 事件绑定

JSX 支持所有的 HTML 元素的事件。但要注意的是，事件名称一定要用驼峰命名方式，如果将 onClick 改成 onclick 就不起作用了

```javascript
<div id="example"></div>
<script type="text/babel">
  function testClick() {
    alert("点击了按钮!");
  }
  var app = <button onClick={testClick.bind(this)} style={{fontSize: '28px'}}>按钮</button>

  ReactDOM.render(
       app,
       document.getElementById('example')
  );
</script>
```

### 组件的生命周期

组件在整个 ReactJS 的生命周期中，主要会经历这4个阶段：创建阶段、实例化阶段、更新阶段、销毁阶段

#### 创建阶段

- 该阶段主要发生在创建组件类的时候，即调用 React.createClass 时触发
- 这个阶段只会触发一个 getDefaultProps 方法，该方法返回一个对象并缓存起来。然后与父组件指定的 props 对象合并，最后赋值给 this.props 作为该组件的默认属性

```
props属性介绍：
1.props 是一个对象，是组件用来接收外面传来的参数的
2.组件内部是不允许修改自己的 props 属性，只能通过父组件来修改。上面的 getDefaultProps 方法便是处理 props 的默认值的

```

#### 实例化阶段

该阶段主要发生在实例化组件类的时候，也就是该组件类被调用的时候触发。这个阶段会触发一系列的流程，按执行顺序如下：

1. getInitialState：初始化组件的 state 的值。其返回值会赋值给组件的 this.state 属性
2. componentWillMount：根据业务逻辑来对 state 进行相应的操作
3. render：根据 state 的值，生成页面需要的虚拟 DOM 结构，并返回该结构
4. componentDidMount：对根据虚拟 DOM 结构而生的真实 DOM 进行相应的处理。组件内部可以通过 ReactDOM.findDOMNode(this) 来获取当前组件的节点，然后就可以像 Web 开发中那样操作里面的 DOM 元素了

```
state属性介绍：
它是用来存储组件自身需要的数据。它是可以改变的，它的每次改变都会引发组件的更新。这也是 ReactJS 中的关键点之一。
即每次数据的更新都是通过修改 state 属性的值，然后 ReactJS 内部会监听 state 属性的变化，一旦发生变化，就会触发组件的 render 方法来更新 DOM 结构
```

#### 更新阶段

这主要发生在用户操作之后或者父组件有更新的时候，此时会根据用户的操作行为进行相应得页面结构的调整。这个阶段也会触发一系列的流程，按执行顺序如下：

1. componentWillReceiveProps：当组件接收到新的 props 时，会触发该函数。在改函数中，通常可以调用 this.setState方法来完成对 state 的修改
2. shouldComponentUpdate：该方法用来拦截新的 props 或 state，然后根据事先设定好的判断逻辑，做出最后要不要更新组件的决定
3. componentWillUpdate：当上面的方法拦截返回 true 的时候，就可以在该方法中做一些更新之前的操作
4. render：根据一系列的 diff 算法，生成需要更新的虚拟 DOM 数据。（注意：在 render 中最好只做数据和模板的组合，不应进行 state 等逻辑的修改，这样组件结构更加清晰）
5. componentDidUpdate：该方法在组件的更新已经同步到 DOM 中去后触发，我们常在该方法中做一 DOM 操作

#### 销毁阶段

- 这个阶段只会触发一个叫 componentWillUnmount 的方法
- 当组件需要从 DOM 中移除的时候，我们通常会做一些取消事件绑定、移除虚拟 DOM 中对应的组件数据结构、销毁一些无效的定时器等工作。这些事情都可以在这个方法中处理

#### 案例

```javascript
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title>hangge</title>
    <script type="text/javascript" src="react.js"></script>
    <script type="text/javascript" src="react-dom.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.24/browser.min.js"></script>
</head>
<body>
  <div id="example"></div>
  <script type="text/babel">
      var Welcome = React.createClass({
          /* 1.创建阶段 */
          //在创建类的时候被调用
          getDefaultProps: function() {
              console.log("getDefaultProps");
              return {};
          },
 
          /* 2.实例化阶段 */
          //获取this.state的默认值
          getInitialState: function() {
              console.log("getInitialState");
              return {name: "hangge.com"};
          },
          //组件将要加载，在render之前调用此方法
          componentWillMount: function() {
              //业务逻辑的处理都应该放在这里，比如对state的操作等
              console.log("componentWillMount");
          },
          //渲染并返回一个虚拟DOM
          render: function() {
              console.log("render");
              return (
                      <div>欢迎访问: {this.state.name}</div>
              );
          },
          //组件完成加载，在render之后调用此方法
          componentDidMount: function() {
              //在该方法中，ReactJS会使用render方法返回的虚拟DOM对象来创建真实的DOM结构
              console.log("componentDidMount");
              var node = ReactDOM.findDOMNode(this);
              console.log(node);
          },
 
          /* 3.更新阶段 */
          //该方法发生在this.props被修改或父组件调用setProps()方法之后
          componentWillReceiveProps: function() {
              console.log("componentWillRecieveProps");
          },
          //是否需要更新
          shouldComponentUpdate: function() {
              console.log("shouldComponentUpdate");
              return true;
          },
          //将要更新
          componentWillUpdate: function() {
              console.log("componentWillUpdate");
          },
          //更新完毕
          componentDidUpdate: function() {
              console.log("componentDidUpdate");
          },
 
          /* 4.销毁阶段 */
          //销毁时会被调用
          componentWillUnmount: function() {
              console.log("componentWillUnmount");
          },
      });
      ReactDOM.render(<Welcome />, document.getElementById('example'));
  </script>
</body>
</html>
```

### 组件通信

####子组件调用父组件的方法

- 子组件要拿到父组件的属性，需要通过 this.props 方法。子组件通过 this.props.属性名 从父组件获取属性。以后每次父组件修改了传入的 属性，子组件便会得到通知，然后会自动获取新的属性
- 同样地，如果子组件想要调用父组件的方法，只需父组件把要被调用的方法以属性的方式放在子组件上，子组件内部便可以通过“this.props.被调用的方法”这样的方式来获取父组件传过来的方法

```javascript
<script type="text/babel">
      //创建子类组件
      var Child = React.createClass({
        render: function() {
            return (
                    <span>{this.props.name}</span>
            );
        },
      });
 
      //创建父类组件
      var Parent = React.createClass({
          render: function() {
              return (
                      <div onClick={this.click}>
                        父组件是：<Child name={this.props.name} ref="child"></Child>
                      </div>
              );
          },
          click: function() {
            ReactDOM.findDOMNode(this.refs.child).style.color = "red";
          },
      });
      ReactDOM.render(<Parent name="hangge.com" />, document.getElementById('example'));
  </script>
```

#### 父组件调用子组件的方法

在 ReactJS 中有个叫 ref 的属性。这个属性就像给组件起个引用名字一样，子组件被设置为 ref 之后（比如 ref="xxx"）。父组件便可以通过 this.refs.xxx 来获取到子组件了

