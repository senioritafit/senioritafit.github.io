---
layout: post
title: Pipelining with Async.js, Q.js, and When.js
date: 2014-01-08
updated: 2014-04-16
categories: code javascript promise
---

## Background

I heavily used [Async](https://github.com/caolan/async) for my projects in the past, but I wanted to give promises a go using the [Q library](https://github.com/kriskowal/q) and the [when.js library](https://github.com/cujojs/when).

## Explanation

I am attempting to pass the result of one asynchronous function to the next and end up with a final result. The goal is to handle this with promises. I have included async in here to compare the promise libraries to something familiar.

 - In Async, there is a [`waterfall`](https://github.com/caolan/async#waterfall) function to handle this situation.
 - In When, there is a [`pipeline`](https://github.com/cujojs/when/blob/master/docs/api.md#whenpipeline) function that seems to do the same thing as waterfall in Async.
 - In Q, there doesn't seem to be a mechanism to do such a thing, but we will see that it isn't needed.

## Examples

Here are three complete and working examples implemented in three different libraries that result in the same string `'foobarbazqux'`. The raw code can be found here: [pipeline.js](https://gist.github.com/trevorsenior/0695e2fd02ef9e52ee59)

### Lib: *Async* (callback based)

This example will be used as a base for the promise based implementations.

```javascript
var async = require('async'); // version 0.7.0

// Given a string & what to append, return a callback
// with the new string
function appendString(string, toAppend, callback) {
  callback(null, string + toAppend);
}

function fooBarBazQuxWaterfall(callback) {
  async.waterfall([
    function(callback) {
      appendString('', 'foo', callback);
    },
    function(foo, callback) {
      appendString(foo, 'bar', callback);
    },
    function(fooBar, callback) {
      appendString(fooBar, 'baz', callback);
    },
    function(fooBarBaz, callback) {
      appendString(fooBarBaz, 'qux', callback);
    }
  ], callback);
}
```

### Lib: *When* (promise based)

The when.js library provides a `pipeline` function that functions in a similar way to async's waterfall function. It takes an array, and passes the result of one function to the next:

```javascript
var when = require('when') // version 3.1.0
, pipeline = require('when/pipeline');


// Given a string & what to append, return
// a promise with the new string
function appendString(string, toAppend) {
  return when(string + toAppend).delay(100);
}

// Using pipeline
function fooBarBazQuxPipeline() {
  return pipeline([
    function() { return appendString('', 'foo'); },
    function(string) {
      return appendString(string, 'bar');
    },
    function(string) {
      return appendString(string, 'baz');
    },
    function(string) {
      return appendString(string, 'qux');
    }
  ]);
}
```

We can also chain together things using `then`:

```javascript
// Using then statements
function fooBarBazQuxThen() {
  return appendString('', 'foo').then(function(foo) {
    return appendString(foo, 'bar');
  }).then(function(fooBar) {
    return appendString(fooBar, 'baz');
  }).then(function(fooBarBaz) {
    return appendString(fooBarBaz, 'qux');
  });
}
```

If we have access to the function, we can have it accept a string, or a promise for a string to simplify the code even further:


```javascript
// Given a promise for a string & what to append,
// promise with the new string
function appendStringAlt(stringOrPromise, toAppend) {
  return when(stringOrPromise).then(function(string) {
    return string + toAppend;
  }).delay(100);
}

// By handling the promise in the `appendStringAlt`
// function, we can remove the use of then statements
// all together
function fooBarBazQuxAlt() {
  var foo = 'foo';
  var foobar = appendStringAlt(foo, 'bar');
  var foobarbaz = appendStringAlt(foobar, 'baz');
  return appendStringAlt(foobarbaz, 'qux');
}
```


### Lib: *Q* (promise based)

The Q library does not add as much utility functions as when.js and async and therefore does not have a waterfall clone. However as demonstrated with the when.js library, it isn't needed. The exact same promise chains can be constructed in the Q library as they were in the when.js library. [View the raw code](https://gist.github.com/trevorsenior/0695e2fd02ef9e52ee59) for the Q implementation.
