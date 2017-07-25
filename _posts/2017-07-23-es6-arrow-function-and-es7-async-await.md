---
layout: post
title: ES6 Arrow Function and ES7 Async Await
date:   2017-07-23 19:00:01 -0600
excerpt: I've always wanted to set up Jekyll for my website. The powerful liquid templating makes building and maintaining a static website so much easier. In addition, the ability to easily customize page and post URL's for SEO (Search Engine Optimization), and to use plain markdown files as page content are very nice.
---

# ES6 Arrow Function and ES7 Async Await

Recently in [my project](https://github.com/42mandychen/giveawaypicker) I played around with ES6 arrow function and ES7 Async Await. I realize how

## Expression vs Statement

An expression produces a value, while a statement performs an action.

> Wherever JavaScript expects a statement, you can also write an expression. Such a statement is called an *expression statement*. The reverse does not hold: you cannot write a statement where JavaScript expects an expression.

Source: [Expressions versus statements in JavaScript](http://2ality.com/2012/09/expressions-vs-statements.html)

## `var`, `let`, `const`

To declare a variable, we have `var`, we have `let`, and we have `const`… Which one to use?

Well, the easiest one is `const` — when you use `const`, you are saying that the variable will not be reassigned.

What about `let` and `var`?

## `==` vs. `===`

`==` does type conversion silently when the types of both sides are not the same, `===` doesn't do type conversion. In other words, `==` checks equality, while `===` checks identity.

> The rules for converting strings and numbers to Boolean values state that `0`, `NaN`, and the empty string (`""`) count as `false`, while all the other values count as `true`.

Source: [Eloquent JavaScript](http://eloquentjavascript.net/01_values.html#p_vNLaRBSip6)

The take-home message is, if you want to check if two things have the same type and have the same value, use `===`, as `==` may have unexpected behaviours.

However, one thing probably needs to be brought up: you can't use `==` or `===` to check if two objects are equal.  For example:

```javascript
let a = [1,2,3];
let b = [1,2,3];
console.log(a == b);  // -> false
console.log(a === b); // -> false
```

To see more detailed documentations regarding `==` and `===`, check [The Abstract Equality Comparison Algorithm](http://es5.github.io/#x11.9.3).

## `undefined` vs. `null`

>  The difference in meaning between `undefined` and `null` is an accident of JavaScript’s design, and it doesn’t matter most of the time. In the cases where you actually have to concern yourself with these values, I recommend treating them as interchangeable (more on that in a moment).

Source: [Eloquent JavaScript](http://eloquentjavascript.net/01_values.html#p_vNLaRBSip6)

## Lexical Scoping



## ES6 Arrow Functions

Why do we need arrow functions?

An arrow function is basically a lambda function [1], and a lambda function does ***not*** create a scope [2].

Remember the annoying thing to keep in mind — `let that = this`? You do not need to do it if you use an arrow function.

Let's look at some code in React [3] (modified from my project .

```javascript
function someFunction () {
    jsonp(requestURL, null, (error, data) => {
        if (error) {
            console.log('error!');
            console.error(error.message);
            this.setState({error: error.message});
        } else {
            console.log('success!');
            console.log(data);
            this.setState({media_id: data.media_id});
        }
    });
}
```

The above code interacts with Intagram API to get the `media_id` of an Instagram post (photo or video). In this version, we can see the callback function is an arrow function. Inside the arrow function, `this.setState({error: error.message});` can be called because `this` inside the arrow function is the same as outside the `jsonp` call.

What if we don't use this arrow function, i.e., let's say we are using ES5 [4] instead of ES6 [5]?

```javascript
function someFunction () {
  let that = this;
  jsonp(requestURL, null, function (error, data) {
        if (error) {
          console.log('error!');
          console.error(error.message);
          that.setState({error: error.message});
        } else {
          console.log('success!');
          console.log(data);
          that.setState({media_id: data.media_id});
        }
      });
}
```

In this case, we have to set `that` to be `this` so that inside the callback function — which creates a scope of its own — we still have access to `this` — the function scope of `someFunction`.
