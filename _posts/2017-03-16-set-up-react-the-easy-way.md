---
layout: post
title: Set up React for an existing project the easy way with Babel and serve through Restify
date:   2017-03-16 21:00:01 -0600
excerpt: Setting up React takes a long time for someone who doesn't have any experience. Following the official installation guide is not very helpful either, as it's not very clear about what we need to do exactly. Babel? Webpack? Browsify? Just tell me how to say hello world in the shortest time!
---

# Set up React for an existing project the easy way with Babel and serve through Restify

{{ page.date | date: "%B %-d, %Y"}}

Setting up `React` takes a long time for someone who doesn't have any experience. Following the [official installation guide](https://facebook.github.io/react/docs/installation.html) is not very helpful either, as it's not very clear about what we need to do exactly. Babel? Webpack? Browsify? Just tell me how to say hello world in the shortest time!

This set up guide can be helpful, and you can do this when you:

- Already have a project
- [Don't want to use npm to manage client packages](https://facebook.github.io/react/docs/installation.html#using-a-cdn) —> just want to print hello world without too much overhead

## Required Dependencies

As `React` uses `JSX` `JavaScript` syntax, and it will not work if we just link a `JSX` `JavaScript` file to an `HTML` file, we need to use `Babel` to transform `JavaScript` files in  `JSX` to non-`JSX` regular `JavaScript` files, and just link the compiled `JavaScript` files to `HTML` files.

### Babel Packages

```
"babel-cli": "^6.24.0"
`"babel-preset-env": "^1.2.2"
`"babel-preset-react": "^6.23.0"
```

### Update Dependencies

If you have a `package.json` file, just write these three lines to `"devDependencies"`, so your `package.json` file will look something like this:

```json
{
  "name": "yourproject",
  "description": "Your Project",
  "license": "GPL-3.0",
  "devDependencies": {
    "babel-cli": "^6.24.0",
    "babel-preset-env": "^1.2.2",
    "babel-preset-react": "^6.23.0"
  },
  "scripts": {
    //...
  },
  "dependencies": {
    //...
  }
}
```

After that, you should run either `npm install` or `yarn configure` get the babel packages installed.

### Add `.babelrc`

Since `Babel` is needed, we are going to need a `.babelrc` file under root folder (your project folder, where `package.json` is). It should be as simple as:

```javascript
{ "presets": ["react"] }
```

### Project Structure

```
|-- .babelrc
|-- package.json
```

## Add Main Pages

Create a folder (I will just call it public), and an `index.html` file and `index.js`inside of it. Now the project structure looks like this:

```
|-- public
     |-- index.html
     |-- index.js
|-- .babelrc
|-- package.json
```

In `index.html`, put:

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title></title>
    <script src="https://unpkg.com/react@15/dist/react.js"></script>
    <script src="https://unpkg.com/react-dom@15/dist/react-dom.js"></script>
</head>
<body>
  	<div id="root"></div>
</body>
</html>
```

[Using the two scripts](https://facebook.github.io/react/docs/installation.html#using-a-cdn) linked is an easy way to use `React` without actually installing the whole pacakge.

Notice in `<body></body>`, we have `<div id="root"></div>`, so where does that come from? It's actually how we link our `React` file to `HTML` file.

In `index.js`, write:

```jsx
ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('root')
);
```

This is in `JSX` syntax.

## Transform JSX file

We need to transform `JSX` file into regular `JavaScript` file, remember? Time to call `Babel` for help.

So far our project structure looks like:

```
|-- public
     |-- index.html
     |-- index.js
|-- .babelrc
|-- package.json
```

Let's put the transformed/compiled under public as well. Make sure you're at project root directory, run this command on Mac/Linux:

```
./node_modules/.bin/babel -o public/compiled.js public/index.js
```

On Windows:

```
.\\node_modules\\.bin\\babel.cmd -o public/compiled.js public/index.js
```

The `node_modules` part is calling `babel`, `-o` means to overwrite so that we have a fully transformed `JavaScript` file everytime. The first path is the destination directory for compiled `JavaScript` file, and the second `JSX` file to transform.

As you can see, this command depends on your preferred project structure. If you need to, just change the file directories and you're good.

## Hello, world!

Now open `index.html` in any browser and just enjoy your first hello-world using `React`!

If you want to make changes to your `React` file (`index.js`), remember to run the command to re-compile it, and refresh the page. Compared with the extra overhead you would have if you ever need to set up `React` the hard way, it is really not too bad.

## Extra: serve page through Restify

If the above works perfect for you, you should be able to see your page locally. However, if you want to host this on a server, there's some extra work on connecting to the server. For me, I want to serve the page through [`Restify`](https://github.com/restify/node-restify).

The general way to do it is to read `index.html`, and send it to the server. In `Restify`, we can take advantage of [`restify.serveStatic`](http://restify.com/#serve-static):

```javascript
server.get(/.*/, restify.serveStatic({
  directory: __dirname + '/public',
  default: 'index.html'
}));
```

The first argument in `get` is a regular expression that specifies the `URI`. In this case, the `URI` is just `/`. Suppose we are on localhost port 8888, the full `URL` will be `localhost:8888/`. Remember to use a regular expression for the first argument, and do ***not*** use string as that will fail!

In `serveStatic`, `directory` is just the directory to the file you want to serve. In our case, it's just the `index.html` under `public`.

Now if you start the server, and go to `localhost:8888` (or replace 8888 with your port number), you should be able to see your page up!
