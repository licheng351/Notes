### React中创建组件的方式有3种
1. ES 5写法：React.createClass()（老版本用法，不建议使用）；
2. ES 6写法：React.Component；
3. 无状态函数式组件，无状态的函数式写法，又称为纯组件SFC。


### 组件之间的通信
React 中数据流是单向的，从父节点到字节点，自上而下。
1. 父组件向子组件通信
2. 子组件向父组件通信
3. 跨级组件通信
       a. props层级嵌套传递
       b. context传递 
4. 非嵌套组件通信
a. 事件的发布订阅模式
b. context实现


### 事件绑定
React的合成事件系统是属于原生浏览器事件的子集。
1. 在构造函数中使用bind()绑定this
    在构造函数constructor()内使用bind()绑定this，等之后调用这个方法的时候，无须再次绑定。这是官方推荐的具有最佳性能的绑定方式。
2. 使用箭头函数绑定this
    每次调用函数时去绑定this，会生成一个新的方法实例，因此对性能会有一定影响。同时当这个函数传入低阶组件时，这些组件可能会再次re-render。
3. 使用bind()方法绑定this
    同方法2一样，每次调用函数的时候再去绑定this，会对性能有一定影响。
4. 使用属性初始化器语法绑定this
    因为使用属性初始化器语法绑定this的方法在创建时使用了箭头函数，所以一创建就绑定了this，因此在调用的时候无须再次绑定。

受控组件和非受控组件对比
受控组件： 在React中强调的是对状态的可控管理，也就是对组件状态的可预知性和可测试性。表单状态是会随用户在表单中的输入、选择或勾选等操作不断发生变化的，每当发生变化时，将它们的状态都写入组件的state中，这种组件就被称为受控组件（Controlled Component）。

非受控组件：非受控组件即无约束组件，React强调的是对状态的可控管理，非受控组件是它的一种反模式。在大多数情况下，推荐使用受控组件来处理表单，当然这并不表明就不能使用非受控组件。比如有一个非常长的表单，希望用户先填写上面的表单域，填完了再去处理所有内容。

非受控组件本身有自己的状态缓存，而受控组件由React的state状态进行缓存。在用户输入内容时，input框中数值的每次改变都对应着调用一次onChange事件，调用的结果就是去触发一次setState()。

受控组件的优点是在用户输入和页面显示之间做了一道可控层，可以在用户输入之后和页面显示之前对输入值进行处理。上述案例中，用户输入的字母在显示前被转为大写字母，同时也在图3.2表单输入实时绑定到页面其他元素下面p标签内同步展示。

受控组件的缺点是需要为每个表单组件都绑定一个change事件，并且定义一个事件处理器去绑定表单值和组件的状态，而且每次表单值的改变都必定会调用一次onChange事件，带来了一些性能上的损耗。即使如此，利大于弊，还是提倡在React中使用受控组件。

注意：Model层数据改变，View层随之同步更新就是单向绑定；有了单向绑定的基础，反过来用户让View层代码改变，Model层随之被更新就是双向数据绑定。

### React高阶组件
高阶组件(Higher Order Component，HOC)是React的一种模式，用于增强现有组件的功能。 简单来说，一个高阶组件就是一个函数，这个函数接受一个组件作为输入，并返回一个新组件作为输出。返回的新组件拥有输入组件不具有的功能。

高阶组件的意义：
重用代码。利用高阶组件提取公共逻辑，减少重复代码。
修改现有React组件的行为。对于某些第三方组件，我们不想触碰其内部逻辑，可以通过独立于原有组件的函数，产生新的组件并且对原组件没有侵害。

根据返回的新组件和传入组件参数的关系，高阶组件的实现方式可以分为两大类：代理方式的高阶组件，继承方式的高阶组件。

### state
正确地使用 State, 不要直接修改 State,应该使用 setState()。State 的更新可能是异步的,出于性能考虑，React 可能会把多个 setState() 调用合并成一个调用。State 的更新会被合并。

### 数据是向下流动的
不管是父组件或是子组件都无法知道某个组件是有状态的还是无状态的，并且它们也并不关心它是函数组件还是 class 组件。

这就是为什么称 state 为局部的或是封装的的原因。除了拥有并设置了它的组件，其他组件都无法访问。

组件可以选择把它的 state 作为 props 向下传递到它的子组件中。

### 节流 & 防抖
如果你有一个 `onClick` 或者 `onScroll` 这样的事件处理器，想要阻止回调被触发的太快，那么可以限制执行回调的速度，可以通过以下几种方式做到这点：

- **节流**：基于时间的频率来进行抽样更改 (例如 [`_.throttle`](https://lodash.com/docs#throttle))
- **防抖**：一段时间的不活动之后发布更改 (例如 [`_.debounce`](https://lodash.com/docs#debounce))
- **`requestAnimationFrame` 节流**：基于 requestAnimationFrame 的抽样更改 (例如 [raf-schd]([`raf-schd`](https://github.com/alexreardon/raf-schd)))

可以看这个比较 throttle 和 debounce 的[可视化页面](http://demo.nimius.net/debounce_throttle/)

> **注意：**
> `_.debounce`、`_.throttle` 和 `raf-schd` 都提供了一个 `cancel` 方法来取消延迟回调。你需要在 `componentWillUnmount` 中调用该方法，或者对代码进行检查来保证在延迟函数有效期间内组件始终挂载。

### References
- [Airbnb React/JSX 编码规范](https://github.com/JasonBoy/javascript/blob/master/react/README.md)
- https://www.cnblogs.com/wonyun/p/5930333.html
- https://github.com/Marco2333/react-demo
- https://zh-hans.reactjs.org/docs/rendering-elements.html
- http://huziketang.mangojuice.top/books/react/lesson1 
- https://react.docschina.org/docs/state-and-lifecycle.html
- https://react.docschina.org/docs/faq-functions.html
- https://css-tricks.com/debouncing-throttling-explained-examples/
