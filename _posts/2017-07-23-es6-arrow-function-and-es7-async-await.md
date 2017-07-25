---
layout: post
title: ES6 Arrow Function and ES7 Async Await
date:   2017-07-23 19:00:01 -0600
excerpt: Recently in my project I played around with ES6 arrow function and ES7 Async Await. I realize how nice arrow function is not just because of its cleaner syntax, but also its scoping. I also got my hand dirty on turning Promises into ES7 Async Await.

---

# ES6 Arrow Function and ES7 Async Await

Recently in [my project](https://github.com/42mandychen/giveawaypicker) I played around with ES6 arrow function and ES7 Async Await. I realize how nice arrow function is not just because of its cleaner syntax, but also its scoping. I also [got my hand dirty](https://github.com/42mandychen/giveawaypicker/blob/master/src/components/InstagramForm/index.js#L134-L152) on turning Promises into ES7 Async Await.

## ES6 Arrow Function

Why do we need arrow functions?

An arrow function is basically a [lambda function](https://en.wikipedia.org/wiki/Anonymous_function), and a lambda function does ***not*** create [scope](https://developer.mozilla.org/en/docs/Web/JavaScript/Closures).

Remember the annoying thing to keep in mind when function scope changes — `let that = this`? You do not need to do it if you use an arrow function.

Let's look at some code in `React` (modified from [my project]((https://github.com/42mandychen/giveawaypicker))).

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

The above code interacts with Intagram API to get the `media_id` of an Instagram post (photo or video) by sending a `jsonp` request inside a `React` component. In this version, we can see the callback function is an arrow function. Inside the arrow function, `this.setState({error: error.message});` can be called because `this` inside the arrow function is the same as outside the `jsonp` call.

What if we don't use this arrow function, i.e., let's say we are using ES5 instead of ES6?

```javascript
function someFunction () {
  let that = this;  // <----
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

Now you see why arrow functions are so nice? In addition, it's super easy to convert a regular function to an arrow function.

```javascript
function myCallBackFunction () {
  // something
}
```

is the same as

```javascript
myCallBackFunction () => {
  // something
}
```

What we do is we remove the `function` keyword, and add a fat big arrow between the right bracket and left curly bracket. Easy!