---
title: 'JS number and rounding'
date: 2019-04-13T21:40:00+02:00
lastmod: 2019-04-28T17:48:00+02:00
draft: false
tags: ['number']
categories: ['js']
---

## Summary

(1.2345).toFixed(3) === '1.234', no rounding?

IEEE Standard for Floating-Point Arithmetic (IEEE 754)

<!--more-->

## IEEE 754

Format (64 bit): seee eeee eeee mmmm mmmm mmmm mmmm mmmm mmmm mmmm mmmm mmmm mmmm mmmm mmmm mmmm

s: sign
e: exponent
m: mantissa

`decimal number = -1^S * 2^(E - 1023) * (1 + sum(i = 1, 52, (m_i * 2^(-1))))`

## Number examples

```javascript
0.1 + 0.2 === 0.30000000000000004;
0.3 * 2 === 0.6;
0.3 * 3 === 0.8999999999999999;
0.3 * 5 === 1.5;
```

| number | IEEE 754                                                           |
| ------ | ------------------------------------------------------------------ |
| 1.5    | 0 01111111111 1000000000000000000000000000000000000000000000000000 |
| 1.75   | 0 01111111111 1100000000000000000000000000000000000000000000000000 |
| 3.75   | 0 10000000000 1110000000000000000000000000000000000000000000000000 |

Reason why (1.2345).toFixed(3) === '1.234':

`1.2345 -> 0 01111111111 0011110000001000001100010010011011101001011110001101 -> 1.2344999999999999307220832`

## Better round function for fractions

```javascript
function roundTo(n, digits = 0) {
  const multiplicator = Math.pow(10, digits);
  n = parseFloat((n * multiplicator).toFixed(11)); // some use 11, some use (digits + 1)
  return Math.round(n) / multiplicator;
}
```

## Resources

- [MDN - JS Nuber](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)
- [Dezimalzahl ↔ IEEE 754](https://www.ultimatesolver.com/de/ieee-754)
- [Stackoverflow - Javascript toFixed Not Rounding](https://stackoverflow.com/questions/10015027/javascript-tofixed-not-rounding)
- [YouTube - 32 bit floating point conversion example](https://www.youtube.com/watch?v=8afbTaA-gOQ)
