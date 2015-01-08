---
layout: post
title: Mapping over new Array(n)
date: 2014-04-29
categories: code javascript
---

This code acts the same in `node v0.10.26`, `chrome 34.0.1847.116`, and `FF 28.0`:

```javascript
> new Array(3).map(function(e) { return 'dun'; });
// Nodejs [ , , ]
// Chrome [ undefined x3 ]
// FF     [ undefined, undefined, undefined ]
```

I expected it to return `['dun','dun','dun']`.

If I add a value to the end of the array before mapping over it, I get this behavior:

```javascript
> new Array(3).concat(void 0).map(function(e) { return 'dun'; });
// Nodejs [ , , , 'dun' ]
// Chrome [undefined × 3, "dun"]
// FF     [undefined, undefined, undefined, "dun"]
```

It turns out that the callback only gets called when the value in the array is explicitly assigned: [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

An alternative:

```javascript
// Generate the array
(function(number) {
	var arr = new Array(n);
	while(number--) { arr[n] = void 0; }
	return arr;
})(3)
// Map over it
.map(function() { return 'dun'; });
```

Golfed & removing any form of efficiency:

```javascript
// Generate the array
(function(n,a){while(n){a[--n]=0}return a})(3,[])
// Map over it
.map(function(){ return 'dun'; })
```

If using [lodash](http://lodash.com/docs#map), they have already handled this:

```javascript
_.map(new Array(3), function() { return 'dun'; });
```

or drop the `new Array(n)`, and use `_.range`:

```javascript
_.range(3).map(function() { return 'dun'; });
```

## Update

Came across this [answer on SO](http://stackoverflow.com/a/13735425/586621) about padding arrays with values, and this hack seems to work if you don't want to use an external library, while keeping it short:

```javascript
Array.apply(null, new Array(3)).map(function() { return 'dun'; });
```
