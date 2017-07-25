---
layout: post
title: "Have fun with JavaScript: ES6 Arrow Function and ES2017 Async Await"
date:   2017-07-23 19:00:01 -0600
excerpt: Recently in my project I played around with ES6 arrow function and ES2017 Async Await. I realize how nice arrow function is not just because of its cleaner syntax, but also its scoping. I also got my hand dirty on turning Promises into ES2017 Async Await.
---

# Have fun with JavaScript: ES6 Arrow Function and ES2017 Async Await

{{ page.date | date: "%B %-d, %Y"}}

Recently in [my project](https://github.com/42mandychen/giveawaypicker) I played around with ES6 arrow function and ES2017 Async Await. I realize how nice arrow function is not just because of its cleaner syntax, but also its scoping. I also [got my hand dirty](https://github.com/42mandychen/giveawaypicker/blob/master/src/components/InstagramForm/index.js) on turning Promises into ES2017 Async Await.

## ES6 Arrow Function

Why do we need arrow functions?

An arrow function is basically a [lambda function](https://en.wikipedia.org/wiki/Anonymous_function), and a lambda function does ***not*** create [scope](https://developer.mozilla.org/en/docs/Web/JavaScript/Closures).

Remember the annoying thing to keep in mind when function scope changes — `let that = this`? You do not need to do it if you use an arrow function.

Let's look at some code in `React` (modified from [my project]((https://github.com/42mandychen/giveawaypicker))).

{% gist 42mandychen/be9e4b409b0ee7424923549e315c3308 arrow-function.js %}

The above code interacts with Intagram API to get the `media_id` of an Instagram post (photo or video) by sending a `jsonp` request inside a `React` component. In this version, we can see the callback function is an arrow function. Inside the arrow function, `this.setState({error: error.message});` can be called because `this` inside the arrow function is the same as outside the `jsonp` call.

What if we don't use this arrow function, i.e., let's say we are using ES5 instead of ES6 (ES2015)?

{% gist 42mandychen/be9e4b409b0ee7424923549e315c3308 without-arrow-function.js %}

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

## ES2017 Async Await vs. Promise

Async await is a new feature in ES2017 (ES8). Recently, [documentations](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function) were up too on Mozilla. As my project requires sending requests to interact with Instagram API, I inevitably needs to use Promise, and chaining Promises. If you don't know about Promise, there's [a nice tutorial](https://developers.google.com/web/fundamentals/getting-started/primers/promises) on Google.

Here is an example of the chaining promises I used.

{% gist 42mandychen/be9e4b409b0ee7424923549e315c3308 chaining-promises.js %}

The first call that returns a promise is `fetchJsonp` on line 3. If the request is successful, it then returns a `response` and we call`response.json()` to get the actual response body on line 4. This `response.json()` returns a new promise and if this promise is successful, I then parse `mediaId` from the response body and use this `mediaId` to make a new request by calling `fetchJsonp` on line 9. After that, it's the same as previously — I call `response.json()` if there's no error. In the end there's a catch block that will get the error message if there's any error in any of the above steps.

And that's it. That's how you would chain promises. Now what will the code look like if we use `async` and `await`?

First, `handleSubmit` is an asynchronous function, so we need the `async` keyword before `handleSubmit` now.

```javascript
async handleSubmit(event) {
  // some code
}
```

Then, we re-write the asynchronous calls. Let's just take the first `fetchJsonp` call on line 3 and change it with `await`.

```javascript
async handleSubmit(event) {
  let response = await fetchJsonp(requestURLForMediaId);
}
```

Here is the magic syntax of  `await`. As you might see, it now looks like a synchronous line of code, doesn't it? Let's do the same for the other calls.

```javascript
async handleSubmit(event) {
  let response = await fetchJsonp(requestURLForMediaId);
  let json = await response.json();
  const mediaId = json.media_id;
  const requestURLForLikes = 'https://api.instagram.com/v1/media/'
    + mediaId + '/likes?access_token=' + token;
  let response2 = await fetchJsonp(requestURLForLikes);
  let json2 = await response2.json();
  let users = json2.data;
}
```

Now that we've dealt with all the success cases, what about the  `catch` block?

If any error occurs, an error will be thrown out and we can use a `try/catch` block to deal with it. So our final version looks like this:

{% gist 42mandychen/be9e4b409b0ee7424923549e315c3308 async-await.js %}

Compared to the chaining-promises version, the async-await version looks much more like, maybe, another language. If you think about the two versions, they are actually doing the same thing quite differently. So far I'm not sure if there's any performance difference, but it'll definitely be interesting to look into this further.

Anyways, the above is what I did with JavaScript recently. It was a lot of fun to me.
