---
title: 'JS arrow function'
date: 2019-04-25T11:36:00+02:00
lastmod: 2019-04-25T14:06:00+02:00
draft: false
tags: ['basics']
categories: ['js']
---

## Summary

1. 箭头函数没有 prototype(原型)，所以箭头函数本身没有 this
2. 箭头函数的 this 在定义的时候继承自外层第一个普通函数的 this（`this` comes from the enclosing lexical scope）。
3. 如果箭头函数外层没有普通函数，严格模式和非严格模式下它的 this 都会指向 window(全局对象)
4. 箭头函数本身的 this 指向不能改变，但可以修改它要继承的对象的 this。
5. 箭头函数的 this 指向全局，使用 arguments 会报未声明的错误。
6. 箭头函数的 this 指向普通函数时,它的 argumens 继承于该普通函数
7. 使用 new 调用箭头函数会报错，因为箭头函数没有 constructor
8. 箭头函数不支持 new.target
9. 箭头函数不支持重命名函数参数,普通函数的函数参数支持重命名
10. 箭头函数相对于普通函数语法更简洁优雅

<!--more-->

## JS `this`

1. 箭头函数没有 prototype(原型)，所以箭头函数本身没有 this
2. 箭头函数的 this 指向在定义的时候继承自外层第一个普通函数的 this
3. 不能直接修改箭头函数的 this 指向（call, apply, bind）。Since arrow functions do not have their own this, the methods call() or apply() can only pass in parameters.
4. 箭头函数外层没有普通函数，严格模式和非严格模式下它的 this 都会指向 window(全局对象)

Until arrow functions, every new function defined its own this value based on how the function was called:

- A new object in the case of a constructor.
- undefined in strict mode function calls.
- The base object if the function is called as an "object method".
- etc.

### Example 1:

```javascript
let a;
const barObj = {
  msg: 'from barObj',
};
const fooObj = {
  msg: 'from fooObj',
};

bar(); // 将bar的this指向barObj // (1)
foo.call(fooObj); // 将foo的this指向fooObj

function foo() {
  a(); // 结果：{ msg: 'from barObj' }
}

function bar() {
  a = () => {
    console.log(this, 'this指向定义的时候外层第一个普通函数');
  }; // 在bar中定义 this继承于bar函数的this指向
}
```

这时候`foo()`就会`log()` `window`。

如果把（1）改成`bar.call(barObj)`，那么`foo()`就会`log()` `barObj`。

### Example 2

```javascript
function Person() {
  // The Person() constructor defines `this` as an instance of itself.
  this.age = 0;

  setInterval(function() {
    // In non-strict mode, the function defines `this`
    // as the global object (because it's where the function is executed.),
    // which is different from the `this`
    // defined by the Person() constructor.
    this.age++;
  }, 1000);
}

var p = new Person();
```

This problem can be fixed by (old):

```javascript
function Person() {
  var that = this; // trick
  that.age = 0;

  setInterval(function() {
    // The callback refers to the `that` variable of which
    // the value is the expected object.
    that.age++;
  }, 1000);
}
```

or in the new ES6 arrow function way:

```javascript
function Person() {
  this.age = 0;

  setInterval(() => {
    this.age++; // |this| properly refers to the Person object
  }, 1000);
}
```

### Example 3, arrow function are best suited for non-method function

```javascript
const obj = {
  i: 10,
  b: () => console.log(this.i, this),
  c: function() {
    console.log(this.i, this);
  },
};

obj.b(); // prints undefined, Window {...} (or the global object)
obj.c(); // prints 10, Object {...}
```

## Function `arguments`

Arrow functions do not have their own `arguments` object. Thus, in this example, arguments is simply a reference to the arguments of the enclosing scope. Use rest parameters (`...`) as an alternative.

## `new` operator

Not to be used as constructors.

```javascript
const Foo = () => {};
const foo = new Foo(); // Uncaught TypeError: Foo is not a constructor
```

## `prototype` property

Arrow functions do not have a `prototype` property.

```javascript
const foo = () => {};
console.log(foo.prototype); // undefined
```

## `yield` keyword

The `yield` keyword may not be used in an arrow function's body (except when permitted within functions further nested within it). As a consequence, arrow functions cannot be used as generators.

## `new.target`

`new.target`是 ES6 新引入的属性，普通函数如果通过`new`调用，`new.target`会返回该函数的引用。
箭头函数不支持`new.target`：

1. 箭头函数的 this 指向全局对象，在箭头函数中使用箭头函数会报错

```javascript
const a = () => {
  console.log(new.target); // Uncaught SyntaxError: new.target expression is not allowed here
};

a();
```

2. 箭头函数的 this 指向普通函数，它的 new.target 就是指向该普通函数的引用。

```javascript
function B() {
  let a = () => {
    console.log(new.target); // 指向函数B：function B(){...}
  };
  a();
}
new B();
```

## Duplicated param name

```javascript
function func1(a, a) {
  console.log(a, arguments);
}
func1(1, 2); // 2 Arguments(2) [1, 2, callee: ƒ, Symbol(Symbol.iterator): ƒ]

const func2 = (a,a) => {
  console.log(a); // Uncaught SyntaxError: Duplicate parameter name not allowed in this context
};
```

## Function body

### Return object literal

```javascript
const func = () => {
  foo: 1;
};
func(); // returns undefined
```

```javascript
const func = () => ({
  foo: 1,
});
func(); // returns the object. Thus prefer having explicit `return`

// preferred
const func1 = () => {
  return {
    foo: 1,
  };
};
```

### No line break between its parameters and its arrow

```javascript
const func = (a, b, c)
           => 1; // Uncaught SyntaxError: Unexpected token =>
```

<!-- prettier-ignore-start -->
```javascript
const func = (
  a,
  b,
  c
) => {
  return 1; // return as expected
};
```
<!-- prettier-ignore-end -->

## Parsing Order

Although the arrow in an arrow function is not an operator, arrow functions have special parsing rules that interact differently with [operator precedence](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence) compared to regular functions.

```javascript
let callback;

callback = callback || function() {}; // ok

callback = callback || () => {}; // Uncaught SyntaxError: Malformed arrow function parameter list

callback = callback || (() => {}); // ok
```

## Resources

- https://mp.weixin.qq.com/s/N0ahVkwVhDpnzGdZyC8jQg
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions
