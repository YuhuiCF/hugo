---
title: "JS for statements and enumerability"
date: 2018-04-08T12:34:00+02:00
lastmod: 2018-04-08T13:01:00+02:00
draft: false
tags: []
categories: ["js"]
---


## Summary

* `forEach()` is a method for Arrays, `[1, 2].forEach((i) => {console.log(i);})`
* `for in` loops over enumerable property names of an object, `for (let i in {a: '1', b: '2'}) {console.log(i);}`
* `for of` is new in ES6, and loops over an iterable object (`[Symbol.iterator]`), returning a list of the values (different version of `forEach`)

## Enumerability

Enumerable properties are those which can be iterated by a for..in loop.

<!--more-->

How to make a property non-enumerable:

```javascript
const a = {};
Object.defineProperty(a, 'myMethod', {// or add to `Object.prototype` instead of `a`
  newValue: function () {
    alert('j');
  },
  enumerable: false,
});
```
