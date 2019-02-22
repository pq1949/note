<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Redux入坑进阶-源码解析](#redux%E5%85%A5%E5%9D%91%E8%BF%9B%E9%98%B6-%E6%BA%90%E7%A0%81%E8%A7%A3%E6%9E%90)
  - [预热](#%E9%A2%84%E7%83%AD)
    - [柯里化函数（`curry`）](#%E6%9F%AF%E9%87%8C%E5%8C%96%E5%87%BD%E6%95%B0curry)
    - [代码组合（`compose`）](#%E4%BB%A3%E7%A0%81%E7%BB%84%E5%90%88compose)
  - [`Redux`](#redux)
    - [`combineReducers`](#combinereducers)
    - [`createStore`](#createstore)
    - [`thunkMiddleware`](#thunkmiddleware)
    - [`applyMiddleware`](#applymiddleware)
    - [`bindActionCreator`](#bindactioncreator)
    - [`bindActionCreator`源码解析](#bindactioncreator%E6%BA%90%E7%A0%81%E8%A7%A3%E6%9E%90)
  - [`react-redux`](#react-redux)
    - [`Provider`](#provider)
    - [`connect`](#connect)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Redux入坑进阶-源码解析

> 本文不涉及redux的使用方法，因此可能更适合使用过 redux 的玩家翻阅😃

### 预热

> redux 函数内部包含了大量[柯里化函数](https://llh911001.gitbooks.io/mostly-adequate-guide-chinese/content/ch4.html)以及[代码组合](https://llh911001.gitbooks.io/mostly-adequate-guide-chinese/content/ch5.html)思想

#### 柯里化函数（`curry`）

通俗的来讲，可以用一句话概括柯里化函数：返回函数的函数

```javascript
// example
const funcA = (a) => {
  return const funcB = (b) => {
    return a + b
  }
};
```

上述的`funcA`函数接收一个参数，并返回同样接收一个参数的`funcB`函数。

柯里化函数有什么好处呢？

- 避免了给一个函数传入大量的参数--我们可以通过柯里化来构建类似上例的函数嵌套，将参数的代入分离开，更有利于调试
- 降低耦合度和代码冗余，便于复用

举个栗子：

```javascript
// 已知listA, listB两个Array，都由int组成，需要筛选出两个Array的交集
const listA = [1, 2, 3, 4, 5];
const listB = [2, 3, 4];

const checkIfDataExist = (list) => {
  return (target) => {
    return list.some(value => value === target)
  };
};
// 调用一次checkIfDataExist函数，并将listA作为参数传入，来构建一个新的函数。
// 而新函数的作用则是：检查传入的参数是否存在于listA里
const ifDataExist = checkIfDataExist(listA);

// 使用新函数来对listB里的每一个元素进行筛选
const intersectionList = listB.filter(value => ifDataExist(value));
console.log(intersectionList); // [2, 3, 4]
```

#### 代码组合（`compose`）

代码组合就像是数学中的结合律：

```javascript
const compose = (f, g) => {
  return (x) => {
    return f(g(x));
  };
};
// 还可以再简洁点
const compose = (f, g) => (x) => f(g(x));
```

通过这样函数之间的组合，可以大大增加可读性，效果远大于嵌套一大堆的函数调用，并且我们可以随意更改函数的调用顺序

### `Redux`

#### `combineReducers`

```javascript
// 回顾一下combineReducers的使用格式

// 两个reducer
const todos = (state = INIT.todos, action) => {
  // ....
};
const filterStatus = (state = INIT.filterStatus, action) => {
  // ...
};

const appReducer = combineReducers({
  todos,
  filterStatus
});
```

> 还记得`combineReducers`的黑魔法吗？即：
>
> 1. 传入的Object参数中，对象的`key`与`value`所代表的`reducer function`同名
>
> 2. 各个`reducer function`的名称和需要传入该reducer的`state`参数同名。

源码标注解读（省略部分）：

```javascript
export default function combineReducers(reducers) {
  // 第一次筛选，参数reducers为Object
  // 筛选掉reducers中不是function的键值对
  var reducerKeys = Object.keys(reducers);
  var finalReducers = {}
  for (var i = 0; i < reducerKeys.length; i++) {
    var key = reducerKeys[i];
    if (typeof reducers[key] === 'function') {
      finalReducers[key] = reducers[key]
    }
  }

  var finalReducerKeys = Object.keys(finalReducers)

  // 二次筛选，判断reducer中传入的值是否合法（!== undefined）
  // 获取筛选完之后的所有key
  var sanityError
  try {
    // assertReducerSanity函数用于遍历finalReducers中的reducer，检查传入reducer的state是否合法
    assertReducerSanity(finalReducers)
  } catch (e) {
    sanityError = e
  }

  // 返回一个function。该方法接收state和action作为参数
  return function combination(state = {}, action) {
    // 如果之前的判断reducers中有不法值，则抛出错误
    if (sanityError) {
      throw sanityError
    }
    // 如果不是production环境则抛出warning
    if (process.env.NODE_ENV !== 'production') {
      var warningMessage = getUnexpectedStateShapeWarningMessage(state, finalReducers, action)
      if (warningMessage) {
        warning(warningMessage)
      }
    }

    var hasChanged = false
    var nextState = {}
    // 遍历所有的key和reducer，分别将reducer对应的key所代表的state，代入到reducer中进行函数调用
    for (var i = 0; i < finalReducerKeys.length; i++) {
      var key = finalReducerKeys[i]
      var reducer = finalReducers[key]
      // 这也就是为什么说combineReducers黑魔法--要求传入的Object参数中，reducer function的名称和要和state同名的原因
      var previousStateForKey = state[key]
      var nextStateForKey = reducer(previousStateForKey, action)
      // 如果reducer返回undefined则抛出错误
      if (typeof nextStateForKey === 'undefined') {
        var errorMessage = getUndefinedStateErrorMessage(key, action)
        throw new Error(errorMessage)
      }
      // 将reducer返回的值填入nextState
      nextState[key] = nextStateForKey
      // 如果任一state有更新则hasChanged为true
      hasChanged = hasChanged || nextStateForKey !== previousStateForKey
    }
    return hasChanged ? nextState : state
  }
}

// 检查传入reducer的state是否合法
function assertReducerSanity(reducers) {
  Object.keys(reducers).forEach(key => {
    var reducer = reducers[key]
    // 遍历全部reducer，并给它传入(undefined, action)
    // 当第一个参数传入undefined时，则为各个reducer定义的默认参数
    var initialState = reducer(undefined, { type: ActionTypes.INIT })

    // ActionTypes.INIT几乎不会被定义，所以会通过switch的default返回reducer的默认参数。如果没有指定默认参数，则返回undefined，抛出错误
    if (typeof initialState === 'undefined') {
      throw new Error(
        `Reducer "${key}" returned undefined during initialization. ` +
        `If the state passed to the reducer is undefined, you must ` +
        `explicitly return the initial state. The initial state may ` +
        `not be undefined.`
      )
    }

    var type = '@@redux/PROBE_UNKNOWN_ACTION_' + Math.random().toString(36).substring(7).split('').join('.')
    if (typeof reducer(undefined, { type }) === 'undefined') {
      throw new Error(
        `Reducer "${key}" returned undefined when probed with a random type. ` +
        `Don't try to handle ${ActionTypes.INIT} or other actions in "redux/*" ` +
        `namespace. They are considered private. Instead, you must return the ` +
        `current state for any unknown actions, unless it is undefined, ` +
        `in which case you must return the initial state, regardless of the ` +
        `action type. The initial state may not be undefined.`
      )
    }
  })
}
```

#### `createStore`

```javascript
// 回顾下使用方法
const store = createStore(reducers, state, enhance);
```

源码标注解读（省略部分）：

```javascript
// 对于未知的action.type，reducer必须返回默认的参数state。这个ActionTypes.INIT就可以用来监测当reducer传入未知type的action时，返回的state是否合法
export var ActionTypes = {
  INIT: '@@redux/INIT'
}

export default function createStore(reducer, initialState, enhancer) {
  // 检查你的state和enhance参数有没有传反
  if (typeof initialState === 'function' && typeof enhancer === 'undefined') {
    enhancer = initialState
    initialState = undefined
  }
  // 如果有传入合法的enhance，则通过enhancer再调用一次createStore
  if (typeof enhancer !== 'undefined') {
    if (typeof enhancer !== 'function') {
      throw new Error('Expected the enhancer to be a function.')
    }
    return enhancer(createStore)(reducer, initialState)
  }

  if (typeof reducer !== 'function') {
    throw new Error('Expected the reducer to be a function.')
  }

  var currentReducer = reducer
  var currentState = initialState
  var currentListeners = []
  var nextListeners = currentListeners
  var isDispatching = false // 是否正在分发事件

  function ensureCanMutateNextListeners() {
    if (nextListeners === currentListeners) {
      nextListeners = currentListeners.slice()
    }
  }

  // 我们在action middleware中经常使用的getState()方法，返回当前state
  function getState() {
    return currentState
  }

  // 注册listener，同时返回一个取消事件注册的方法。当调用store.dispatch的时候调用listener
  function subscribe(listener) {
    if (typeof listener !== 'function') {
      throw new Error('Expected listener to be a function.')
    }

    var isSubscribed = true

    ensureCanMutateNextListeners()
    nextListeners.push(listener)

    return function unsubscribe() {
      if (!isSubscribed) {
        return
      }

      isSubscribed = false
      // 从nextListeners中去除掉当前listener
      ensureCanMutateNextListeners()
      var index = nextListeners.indexOf(listener)
      nextListeners.splice(index, 1)
    }
  }

  // dispatch方法接收的action是个对象，而不是方法。
  // 这个对象实际上就是我们自定义action的返回值，因为dispatch的时候，已经调用过我们的自定义action了，比如 dispatch(addTodo())
  function dispatch(action) {
    if (!isPlainObject(action)) {
      throw new Error(
        'Actions must be plain objects. ' +
        'Use custom middleware for async actions.'
      )
    }

    if (typeof action.type === 'undefined') {
      throw new Error(
        'Actions may not have an undefined "type" property. ' +
        'Have you misspelled a constant?'
      )
    }
    // 调用dispatch的时候只能一个个调用，通过dispatch判断调用的状态
    if (isDispatching) {
      throw new Error('Reducers may not dispatch actions.')
    }

    try {
      isDispatching = true
      currentState = currentReducer(currentState, action)
    } finally {
      isDispatching = false
    }
    // 遍历调用各个linster
    var listeners = currentListeners = nextListeners
    for (var i = 0; i < listeners.length; i++) {
      listeners[i]()
    }

    return action
  }
  // Replaces the reducer currently used by the store to calculate the state.
  function replaceReducer(nextReducer) {
    if (typeof nextReducer !== 'function') {
      throw new Error('Expected the nextReducer to be a function.')
    }

    currentReducer = nextReducer
    dispatch({ type: ActionTypes.INIT })
  }
  // 当create store的时候，reducer会接受一个type为ActionTypes.INIT的action，使reducer返回他们默认的state，这样可以快速的形成默认的state的结构
  dispatch({ type: ActionTypes.INIT })

  return {
    dispatch,
    subscribe,
    getState,
    replaceReducer
  }
}
```

#### `thunkMiddleware`

源码及其简单简直给跪...

```javascript
// 返回以 dispatch 和 getState 作为参数的action
export default function thunkMiddleware({ dispatch, getState }) {
  return next => action => {
    if (typeof action === 'function') {
      return action(dispatch, getState);
    }

    return next(action);
  };
}
```

#### `applyMiddleware`

先复习下用法：

```javascript
// usage
import { createStore, applyMiddleware } from 'redux';
import thunkMiddleware from 'redux-thunk';

const store = createStore(
      reducers,
      state,
      applyMiddleware(thunkMiddleware)
);
```

`applyMiddleware`首先接收`thunkMiddleware`作为参数，两者组合成为一个新的函数（`enhance`），之后在`createStore`内部，因为`enhance`的存在，将会变成返回`enhancer(createStore)(reducer, initialState)`

源码标注解读（省略部分）：

```javascript
// 定义一个代码组合的方法
// 传入一些function作为参数，返回其链式调用的形态。例如，
// compose(f, g, h) 最终返回 (...args) => f(g(h(...args)))
export default function compose(...funcs) {
  if (funcs.length === 0) {
    return arg => arg
  } else {
    const last = funcs[funcs.length - 1]
    const rest = funcs.slice(0, -1)
    return (...args) => rest.reduceRight((composed, f) => f(composed), last(...args))
  }
}

export default function applyMiddleware(...middlewares) {
  // 最终返回一个以createStore为参数的匿名函数
  // 这个函数返回另一个以reducer, initialState, enhancer为参数的匿名函数
  return (createStore) => (reducer, initialState, enhancer) => {
    var store = createStore(reducer, initialState, enhancer)
    var dispatch
    var chain = []

    var middlewareAPI = {
      getState: store.getState,
      dispatch: (action) => dispatch(action)
    }
    // 每个 middleware 都以 middlewareAPI 作为参数进行注入，返回一个新的链。此时的返回值相当于调用 thunkMiddleware 返回的函数： (next) => (action) => {} ，接收一个next作为其参数
    chain = middlewares.map(middleware => middleware(middlewareAPI))
    // 并将链代入进 compose 组成一个函数的调用链
    // compose(...chain) 返回形如(...args) => f(g(h(...args)))，f/g/h都是chain中的函数对象。
    // 在目前只有 thunkMiddleware 作为 middlewares 参数的情况下，将返回 (next) => (action) => {}
    // 之后以 store.dispatch 作为参数进行注入
    dispatch = compose(...chain)(store.dispatch)

    return {
      ...store,
      dispatch
    }
  }
}
```

一脸懵逼？没关系，来结合实际使用总结一下：

当我们搭配`redux-thunk`这个库的时候，在`redux`配合`components`时，通常这么写

```javascript
import thunkMiddleware from 'redux-thunk';
import { createStore, applyMiddleware, combineReducer } from 'redux';
import * as reducers from './reducers.js';

const appReducer = combineReducer(reducers);
const store = createStore(appReducer, initialState, applyMiddleware(thunkMiddleware));
```

还记得当`createStore`收到的参数中有`enhance`时会怎么做吗？

```javascript
// createStore.js
if (typeof enhancer !== 'undefined') {
  if (typeof enhancer !== 'function') {
    throw new Error('Expected the enhancer to be a function.')
  }
  return enhancer(createStore)(reducer, initialState)
}
```

也就是说，会变成下面的情况

```javascript
applyMiddleware(thunkMiddleware)(createStore)(reducer, initialState)
```

- `applyMiddleware(thunkMiddleware)`

`applyMiddleware`接收`thunkMiddleware`作为参数，返回形如`(createStore) => (reducer, initialState, enhancer) => {}`的函数。

- `applyMiddleware(thunkMiddleware)(createStore)`

以 createStore 作为参数，调用上一步返回的函数`(reducer, initialState, enhancer) => {}`

- `applyMiddleware(thunkMiddleware)(createStore)(reducer, initialState)`

以（reducer, initialState）为参数进行调用。
在这个函数内部，`thunkMiddleware`被调用，其作用是监测`type`是`function`的`action`

因此，如果`dispatch`的`action`返回的是一个`function`，则证明是中间件，则将`(dispatch, getState)`作为参数代入其中，进行`action` 内部下一步的操作。否则的话，认为只是一个普通的`action`，将通过`next`(也就是`dispatch`)进一步分发

---

也就是说，`applyMiddleware(thunkMiddleware)`作为`enhance`，最终起了这样的作用：

对`dispatch`调用的`action`(例如，`dispatch(addNewTodo(todo)))`进行检查，如果`action`在第一次调用之后返回的是`function`，则将`(dispatch, getState)`作为参数注入到`action`返回的方法中，否则就正常对`action`进行分发，这样一来我们的中间件就完成喽~

因此，当`action`内部需要获取`state`，或者需要进行异步操作，在操作完成之后进行事件调用分发的话，我们就可以让`action` 返回一个以`(dispatch, getState)`为参数的`function`而不是通常的`Object`，`enhance`就会对其进行检测以便正确的处理

#### `bindActionCreator`

> 这个方法感觉比较少见，我个人也很少用到

在传统写法下，当我们要把 state 和 action 注入到子组件中时，一般会这么做：

```javascript
import { connect } from 'react-redux';
import {addTodo, deleteTodo} from './action.js';

class TodoComponect extends Component {
  render() {
    return (
      <ChildComponent
        deleteTodo={this.props.deleteTodo}
        addTodo={this.props.addTodo}
      />
    )
  }
}

function mapStateToProps(state) {
  return {
    state
  }
}
function mapDispatchToProps(dispatch) {
  return {
    deleteTodo: (id) => {
      dispatch(deleteTodo(id));
    },
    addTodo: (todo) => {
      dispatch(addTodo(todo));
    }
  }
}
export default connect(mapStateToProps, mapDispatchToProps)(TodoComponect);
```

使用`bindActionCreators`可以把 action 转为同名 key 的对象，但使用 dispatch 把每个 action 包围起来调用

*惟一使用 bindActionCreators 的场景是当你需要把 action creator 往下传到一个组件上，却不想让这个组件觉察到 Redux 的存在，而且不希望把 Redux store 或 dispatch 传给它*

```javascript
import { bindActionCreators } from 'redux';
import { connect } from 'react-redux';
import {addTodo, deleteTodo} as TodoActions from './action.js';

class TodoComponect extends React.Component {

  // 在本组件内的应用
  addTodo(todo) {
    let action = TodoActions.addTodo(todo);
    this.props.dispatch(action);
  }

  deleteTodo(id) {
    let action = TodoActions.deleteTodo(id);
    this.props.dispatch(action);
  }

  render() {
    let dispatch = this.props.dispatch;
    // 传递给子组件
    let boundActionCreators = bindActionCreators(TodoActions, dispatch);
    return (
      <ChildComponent
        {...boundActionCreators}
      />
    )
  }
}

function mapStateToProps(state) {
  return {
    state
  }
}
export default connect(mapStateToProps)(TodoComponect)
```

#### `bindActionCreator`源码解析

```javascript
function bindActionCreator(actionCreator, dispatch) {
  return (...args) => dispatch(actionCreator(...args))
}

// bindActionCreators期待一个Object作为actionCreators传入，里面是 key: action
export default function bindActionCreators(actionCreators, dispatch) {
  // 如果只是传入一个action，则通过bindActionCreator返回被绑定到dispatch的函数
  if (typeof actionCreators === 'function') {
    return bindActionCreator(actionCreators, dispatch)
  }

  if (typeof actionCreators !== 'object' || actionCreators === null) {
    throw new Error(
      `bindActionCreators expected an object or a function, instead received ${actionCreators === null ? 'null' : typeof actionCreators}. ` +
      `Did you write "import ActionCreators from" instead of "import * as ActionCreators from"?`
    )
  }

  // 遍历并通过bindActionCreator分发绑定至dispatch
  var keys = Object.keys(actionCreators)
  var boundActionCreators = {}
  for (var i = 0; i < keys.length; i++) {
    var key = keys[i]
    var actionCreator = actionCreators[key]
    if (typeof actionCreator === 'function') {
      boundActionCreators[key] = bindActionCreator(actionCreator, dispatch)
    }
  }
  return boundActionCreators
}
```

### `react-redux`

#### `Provider`

```javascript
export default class Provider extends Component {
  getChildContext() {
    // 将其声明为 context 的属性之一
    return { store: this.store }
  }

  constructor(props, context) {
    super(props, context)
    // 接收 redux 的 store 作为 props
    this.store = props.store
  }

  render() {
    return Children.only(this.props.children)
  }
}

if (process.env.NODE_ENV !== 'production') {
  Provider.prototype.componentWillReceiveProps = function (nextProps) {
    const { store } = this
    const { store: nextStore } = nextProps

    if (store !== nextStore) {
      warnAboutReceivingStore()
    }
  }
}

Provider.propTypes = {
  store: storeShape.isRequired,
  children: PropTypes.element.isRequired
}
Provider.childContextTypes = {
  store: storeShape.isRequired
}
```

#### `connect`

传入`mapStateToProps`,`mapDispatchToProps`,`mergeProps`,`options`。
首先获取传入的参数，如果没有则以默认值代替

```javascript
const defaultMapStateToProps = state => ({}) // eslint-disable-line no-unused-vars
const defaultMapDispatchToProps = dispatch => ({ dispatch })
const { pure = true, withRef = false } = options
```

之后，通过

```javascript
const finalMergeProps = mergeProps || defaultMergeProps
```

选择合并`stateProps`,`dispatchProps`,`parentProps`的方式，默认的合并方式 `defaultMergeProps` 为：

```javascript
const defaultMergeProps = (stateProps, dispatchProps, parentProps) => ({
  ...parentProps,
  ...stateProps,
  ...dispatchProps
})
```

返回一个以 Component 作为参数的函数。在这个函数内部，生成了一个叫做`Connect`的 Component

```javascript
// ...
  return function wrapWithConnect(WrappedComponent) {
    const connectDisplayName = `Connect(${getDisplayName(WrappedComponent)})`
    // 检查参数合法性
    function checkStateShape(props, methodName) {}
    // 合并props
    function computeMergedProps(stateProps, dispatchProps, parentProps) {
      const mergedProps = finalMergeProps(stateProps, dispatchProps, parentProps)
      if (process.env.NODE_ENV !== 'production') {
        checkStateShape(mergedProps, 'mergeProps')
      }
      return mergedProps
    }

    // start of Connect
    class Connect extends Component {
      constructor(props, context) {
        super(props, context);
        this.store = props.store || context.store

        const storeState = this.store.getState()
        this.state = { storeState }
        this.clearCache()
      }

      computeStateProps(store, props) {
        // 调用configureFinalMapState，使用传入的mapStateToProps方法（或默认方法），将state map进props
      }
      configureFinalMapState(store, props) {}

      computeDispatchProps(store, props) {
        // 调用configureFinalMapDispatch，使用传入的mapDispatchToProps方法（或默认方法），将action使用dispatch封装map进props
      }
      configureFinalMapDispatch(store, props) {}

      // 判断是否更新props
      updateStatePropsIfNeeded() {}
      updateDispatchPropsIfNeeded() {}
      updateMergedPropsIfNeeded() {}

      componentDidMount() {
        // 内部调用this.store.subscribe(this.handleChange.bind(this))
        this.trySubscribe()
      }
      handleChange() {
        const storeState = this.store.getState()
        const prevStoreState = this.state.storeState
        // 对数据进行监听，发送改变时调用
        this.setState({ storeState })
      }

      // 取消监听，清除缓存
      componentWillUnmount() {
        this.tryUnsubscribe()
        this.clearCache()
      }

      render() {
        this.renderedElement = createElement(WrappedComponent,
            this.mergedProps
        )
        return this.renderedElement
      }
    }
    // end of Connect

    Connect.displayName = connectDisplayName
    Connect.WrappedComponent = WrappedComponent
    Connect.contextTypes = {
      store: storeShape
    }
    Connect.propTypes = {
      store: storeShape
    }

    return hoistStatics(Connect, WrappedComponent)
  }
// ...
```

我们看见，在connect的最后，返回了使用`hoistStatics`包装的`Connect`和`WrappedComponent`

[hoistStatics](https://github.com/mridgway/hoist-non-react-statics)是什么鬼？[为什么使用它?](https://github.com/reactjs/react-redux/issues/276)

> Copies non-react specific statics from a child component to a parent component. Similar to Object.assign, but with React static keywords blacklisted from being overridden.

也就是说，它类似于`Object.assign`，作用是将子组件中的 static 方法复制进父组件，但不会覆盖组件中的关键字方法(如 componentDidMount)

```javascript
import hoistNonReactStatic from 'hoist-non-react-statics';

hoistNonReactStatic(targetComponent, sourceComponent);
```
