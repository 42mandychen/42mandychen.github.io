---
layout: post
title: Set up React for an existing project the hard way with Babel, Webpack and serve through Webpack server
date:   2017-03-16 23:00:01 -0600
excerpt: In this guide, I put down the steps I followed to set up React with Babel and Webpack.
---

# Set up React for an existing project the hard way with Babel, Webpack and serve through Webpack server

If you want to set up `React` quickly, check out my note on [setting up `React` the easy way](https://gist.github.com/42mandychen/0aa124fda880689dc2c4308f3d9628d0). In this guide, I put down the steps I followed to set up `React` with `Babel` and `Webpack`.

A few tutorials I found:

[official installation guide](https://facebook.github.io/react/docs/installation.html)

- It doesn't really explain what we need to do, and how we link files
- `init` commands are used only when you need to create a new project from scratch

[Codecademy Tutorial](https://www.codecademy.com/articles/react-setup-i)

- It has some nice explanations on `React`, `Babel`, `Webpack`, and how things work in general
- It is a complete walkthrough starting from getting `npm` installed
- Their syntax for `.babelrc` is not correct —> `.babelrc` is a JSON file
- As a computer science tutorial that involves actual code, the fact that they don't have code boxes but rather pictures is very inconvenient

[Setup React using Babel and Webpack](https://scotch.io/tutorials/setup-a-react-environment-using-webpack-and-babel)

- Explains things step by step as well
- Their file paths in `webpack.config.js` are relative paths, which are no longer supported in the newest `Webpack` —> change to absolute paths using `__dirname`

This set up guide can be helpful, and you can do this when you:

- Already have a project
- [Don't want to use npm to manage client packages](https://facebook.github.io/react/docs/installation.html#using-a-cdn) —> just want to print hello world without too much overhead

This guide is aimed to give steps with specific code, not to explain every step as I cannot do a better job than all the other tutorials. If you want to understand why, make sure to check out the above tutorials.

## Required Dependencies

### Update Dependencies

If you have a `package.json` file, just write these three lines to `"devDependencies"`, so your `package.json` file will look something like this:

```json
{
  "name": "yourproject",
  "description": "Your Project",
  "license": "GPL-3.0",
  "devDependencies": {
    "babel-cli": "^6.24.0",
    "babel-core": "^6.24.0",
    "babel-loader": "^6.4.0",
    "babel-preset-env": "^1.2.2",
    "babel-preset-es2015": "^6.24.0",
    "babel-preset-react": "^6.23.0",
    "html-webpack-plugin": "^2.28.0",
    "webpack": "^2.2.1",
    "webpack-dev-server": "^2.4.2"
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

Since `Babel` is needed, we are going to need a `.babelrc` file under root folder (your project folder, where `package.json` is):

```javascript
{ "presets": ["react", "es2015"] }
```

### Add `webpack.config.js`

Since `Webpack` is used, we need this configuration file. Here we use `HTMLWebpackPlugin` as well. Place it under root folder:

```json
var HTMLWebpackPlugin = require('html-webpack-plugin');
var HTMLWebpackPluginConfig = new
    HTMLWebpackPlugin({
        template: __dirname + "/public/index.html",
        filename: "index.html",
        inject: "body"
});

module.exports = {
    entry: __dirname + "/public/index.js",
    module: {
        loaders: [
            { test: /\.js$/, loader: 'babel-loader', exclude: /node_modules/ },
            { test: /\.jsx$/, loader: 'babel-loader', exclude: /node_modules/ }
        ]
    },
    output: {
        filename: 'index_bundle.js',
        path: __dirname + '/public'
    },
    plugins: [HTMLWebpackPluginConfig]
};
```

Notice how `__dirname` is used to have absolute paths.

This will load the `index.html` file under `public` folder, transform the `JSX` `index.js` file to a regular `JavaScript` file called `index_bundle.js`, and put this transformed/compiled file under `public`.

Therefore, our ideal project structure looks like this after everything (**but not yet** as we haven't created all the files):

```
|-- public
	|-- index.html
	|-- index.js
	|-- index_bundle.js
|-- .babelrc
|-- package.json
|-- webpack.config.js
```



## Add Main Pages

Create the `public` under root directory, and an `index.html` file and `index.js`inside of it. Now the project structure looks like this:

```
|-- public
	|-- index.html
	|-- index.js
|-- .babelrc
|-- package.json
|-- webpack.config.js
```

In `index.html`, put:

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title></title>
</head>
<body>
  	<div id="root"></div>
</body>
</html>
```

Notice in `<body></body>`, we have `<div id="root"></div>`, so where does that come from? It's actually how we link our `React` file to `HTML` file.

In `index.js`, write:

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('root')
);
```

This is in `JSX` syntax.



## Run on Webpack server

We will use the `Webpack` server to do the work.

An easy way to do this is to add a command to the `scripts` section in `package.json`:

```json
{
  "name": "yourproject",
  "description": "Your Project",
  "license": "GPL-3.0",
  "devDependencies": {
    "babel-cli": "^6.24.0",
    "babel-core": "^6.24.0",
    "babel-loader": "^6.4.0",
    "babel-preset-env": "^1.2.2",
    "babel-preset-es2015": "^6.24.0",
    "babel-preset-react": "^6.23.0",
    "html-webpack-plugin": "^2.28.0",
    "webpack": "^2.2.1",
    "webpack-dev-server": "^2.4.2"
  },
  "scripts": {
    //...
    "start": "webpack-dev-server"
  },
  "dependencies": {
    //...
  }
}
```

Then, run `yarn start` or `npm start`, and you should be given a `URL` on command line as `Webpack` server runs. Go to that `URL` on any browser and you should be able to see your hello world!

If you make any change to your `React`, just save the file and your web page will be updated in real time. Neat!
