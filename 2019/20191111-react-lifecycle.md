## 组件的生命周期
每个组件都包含“生命周期方法”，你可以重写这些方法，以便于在运行过程中特定的阶段执行这些方法。你可以使用此[生命周期图谱](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)作为速查表。在下述列表中，常用的生命周期方法会被加粗。其余生命周期函数的使用则相对罕见。

### 挂载
当组件第一次被渲染到 DOM 中的时候，这在 React 中被称为“挂载（mount）”。
当组件实例被创建并插入 DOM 中时，其生命周期调用顺序如下：

- constructor()
- static getDerivedStateFromProps()
- render()
- componentDidMount()

### 更新
当组件的 props 或 state 发生变化时会触发更新。组件更新的生命周期调用顺序如下：

- static getDerivedStateFromProps()
- shouldComponentUpdate()
- render()
- getSnapshotBeforeUpdate()
- componentDidUpdate()

### 卸载
同时当 DOM中的组件被删除的时候，这在 React 中被称为“卸载（unmount）”。
当组件从 DOM 中移除时会调用如下方法：
- componentWillUnmount()

### 错误处理
当渲染过程，生命周期，或子组件的构造函数中抛出错误时，会调用如下方法：

- static getDerivedStateFromError()
- componentDidCatch()

#### 注意:
下述方法即将过时，在新代码中应该避免使用它们：

- UNSAFE_componentWillMount()
- UNSAFE_componentWillUpdate()
- UNSAFE_componentWillReceiveProps()
- UNSAFE_componentWillUpdate()
- UNSAFE_componentWillReceiveProps()




### Reference
- https://react.docschina.org/docs/state-and-lifecycle.html
- https://react.docschina.org/docs/react-component.html
