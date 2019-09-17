# React & Redux

[TOC]

## React

### react与vue的区别

1. react兼容性更好，vue不兼容ie8
2. react采用jsx语法，而vue使用html模版语法。
3. 一般大项目用react,小项目用vue。
4. 维护团队不同，react是社区维护，维护的更加全面一些。

### react特点及优势

**优点：**

1. 对虚拟dom操作，而不是真实dom，减少了不必要的渲染。
2. 组件化，模块化。每个模块是组件，组件化开发，可维护性高。
3. 单向数据流。对于数据的传递更容易控制，比较有序，有便于管理。
4. 跨浏览器兼容。

**缺点：**

1. 当父组件重新渲染时，子组件即便props和state没有变化也必须重新渲染。
2. 需要依赖很多的其他模块。

**特点：**

1. 声明式渲染。React采用声明范式，可以轻松描述应用。
2. 高效。React通过对DOM的模拟，最大限度地减少与DOM的交互。
3. 灵活。React可以与已知的库或框架很好地配合。

### react原理

React使用虚拟DOM机制，对于每一个组件，React会在内存中构建一个相对应的DOM树，基于React开发时所有的DOM操作都基于虚拟DOM进行，每一次数据变化后，React都会先更新内存中的虚拟DOM，然后通过Diff算法，对比真实的DOM元素，获取DOM结构变化的部分（Pathchs），然后将这些Pathchs更新到真实的DOM中。

由于所有的过程都是在内存中进行，因此非常高效。

### setstate原理

React对于this.setState，并不是一触发this.setState就将state的值变化，而是采用批量更新（**batch update**机制）。在setState后，将需要更新的state合并之后放入状态队列。在一定时候，才会对state进行更新，这样可以减少组件的渲染次数，提高性能。

> React的batch update是采用Transaction（事物）来实现的。Transaction对函数进行包装，让React有机会在函数执行前和执行后运行特定的逻辑。

Transaction的执行机制：

1. 在事件initiallize阶段，创建update queue。
2. 调用setState时，状态不会自理调用，而是被push进update queue。
3. 函数执行结束调用事件close阶段，update queue会被flush。

想比于React，Vue是采用Event Loop。

> React基于Transaition实现的Batch Query是一个不以来语言特性的通用模式，因此有更稳定可控的表现。但缺点是无法覆盖所有情况。

比如setTimeout的回调函数不受React控制。 由于setTimeout等要离开主线程进行异步操作时会脱离当前的UI事物，在进入此次处理时batchUpdate=false。所以setState几次就render几次。

```javascript
// setState的另外一种方式
// 传入一个function 第一个参数为上一次更新后的state 第二个参数为应用更新时的props
this.setState((prevState,props) => {
	return { index : prevState.index + 1 + props.index };
})
```

### 组件生命周期

分为三个部分： 实例化，存在期和销毁期。

**实例化：**

- getDefaultProps 用来设置默认的props对于每个组件实例，该方法只调用一次
- getInitialState 初始化每个实例的state，此时props可以被访问到
- componentWillMount 组件即将挂载，组件渲染之前
- render 创建一个虚拟dom 必须方法
- componentDidMount 组件挂载，已渲染出真实的DOM 可以通过this.getDOMNode() 或者 ReactDOM.findDOMNode()获取真实DOM节点

**存在期：**

- componentWillReceiveProps 当父组件传入的props发生变化时触发
- shouldComponentUpdate 决定组件是否需要更新 false则不会更新
- componentWillUpdate 在组件接受到新的props或者state即将重新渲染 （别用this.setState）
- render
- componentDidUpdate 组件重新渲染之后

**销毁时：**

- componentWillUnmount 组件销毁前 完成所有的清理工作和销毁工作，包括定时器，事件监听器



![img](img/1000.png)

#### React v16.3新引入两个生命周期函数getDerivedStateFromProps、getSnapshotBeforeUpdate

**static getDerivedStateFromProps(nextProps, prevState):** 组件接受新的props时，它应该返回一个对象来更新状态，或者返回null来不更新任何内容，而不会做其他的会影响state的值的操作。

```javascript
// before
componentWillReceiveProps(nextProps) {
  if (nextProps.isLogin !== this.props.isLogin) {
    this.setState({ 
      isLogin: nextProps.isLogin,   
    });
  }
  if (nextProps.isLogin) {
    this.handleClose();
  }
}

// after
static getDerivedStateFromProps(nextProps, prevState) {
  if (nextProps.isLogin !== prevState.isLogin) {
    return {
      isLogin: nextProps.isLogin,
    };
  }
  return null;
}

componentDidUpdate(prevProps, prevState) {
  if (!prevState.isLogin && this.props.isLogin) {
    this.handleClose();
  }
}
```

getDerivedStateFromProps还禁止组件去访问this.props，强制让开发者去比较nextProps与prevState的值，以确定在使用时，是根据当前的props去更新组件的state，而不是做一些奇怪的事让组件的状态变的难以预测。

componentWillUpdate 可以读取当前某个DOM元素的状态，componentDidUpdate 中使用 componentWillUpdate 中读取到的 DOM 元素状态是不安全的。

 此时就需要**getSnapshotBeforeUpdate(prevProps, prevState)**

```jsx
class ScrollingList extends React.Component {
  constructor(props) {
    super(props);
    this.listRef = React.createRef();
  }

  getSnapshotBeforeUpdate(prevProps, prevState) {
    // 我们是否要添加新的 items 到列表?
    // 捕捉滚动位置，以便我们可以稍后调整滚动.
    if (prevProps.list.length < this.props.list.length) {
      const list = this.listRef.current;
      return list.scrollHeight - list.scrollTop;
    }
    return null;
  }

  componentDidUpdate(prevProps, prevState, snapshot) {
    // 如果我们有snapshot值, 我们已经添加了新的items.
    // 调整滚动以至于这些新的items 不会将旧items推出视图。
    // (这边的snapshot是 getSnapshotBeforeUpdate方法的返回值)
    if (snapshot !== null) {
      const list = this.listRef.current;
      list.scrollTop = list.scrollHeight - snapshot;
    }
  }

  render() {
    return (
      <div ref={this.listRef}>{/* ...contents... */}</div>
    );
  }
}
```



![img](img/1000-20190820202806846.png)

