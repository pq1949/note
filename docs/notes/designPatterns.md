### 图说设计模式

https://github.com/me115/design_patterns

http://design-patterns.readthedocs.org/zh_CN/latest/index.html

### 使用 Swift 实现的常用设计模式示例

https://github.com/lizelu/DesignPatterns-Swift

### js 版本的实现

#### 单例模式

```js
// https://www.30secondsofcode.org/blog/s/javascript-singleton-proxy
const singletonify = className => {
  return new Proxy(className.prototype.constructor, {
    instance: null,
    construct: (target, argumentsList) => {
      if (!this.instance) this.instance = new target(...argumentsList);
      return this.instance;
    }
  });
};

/**
const singletonify = (className) => {
  return new Proxy(className.prototype.constructor, {
    instance: null,
    construct: (target, argumentsList) => {
      if (!this.instance)
        this.instance = Reflect.construct(target, argumentsList);
      return this.instance;
    }
  });
}
**/

class MyClass {
  constructor(msg) {
    this.msg = msg;
  }

  printMsg() {
    console.log(this.msg);
  }
}

MySingletonClass = singletonify(MyClass);

const myObj = new MySingletonClass("first");
myObj.printMsg(); // 'first'
const myObj2 = new MySingletonClass("second");
myObj2.printMsg(); // 'first'
```

#### 观察者模式

```js
// https://es6.ruanyifeng.com/#docs/reflect
const queuedObservers = new Set();

const observe = fn => queuedObservers.add(fn);
const observable = obj => new Proxy(obj, {set});

function set(target, key, value, receiver) {
  const result = Reflect.set(target, key, value, receiver);
  queuedObservers.forEach(observer => observer());
  return result;
}


const person = observable({
  name: '张三',
  age: 20
});

function print() {
  console.log(`${person.name}, ${person.age}`)
}

observe(print);
person.name = '李四';
```
