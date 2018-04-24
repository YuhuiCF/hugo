---
title: "Webpack Upgrade"
date: 2018-03-07T16:00:00+01:00
lastmod: 2018-04-24T11:43:00+02:00
draft: false
tags: ["webpack"]
categories: ["js"]
---


## Upgrade of webpack to 4.x.x

A new major version of webpack has been released, 4.x.x.

Here are the listed changes from an existing repository having webpack@2.2.1 and needed to be upgraded to webpack@4.1.0.

<!--more-->

### Updated npm modules

```javascript
{
  "webpack": {
    "from": "2.2.1",
    "to":   "4.1.0",
  },
  "webpack-dev-server": {
    "from": "2.4.2",
    "to":   "3.1.0",
  },
  "karma-webpack": {
    "from": "2.0.3",
    "to":   "2.0.13",
  },
  "babel-loader": {
    "from": "7.0.0",
    "to":   "7.1.4",
  },
  "uglifyjs-webpack-plugin@1.2.2": {
    "new": "replace config.plugins.push(new webpack.optimize.UglifyJsPlugin({...}))"
  },
  "webpack-cli@2.0.10": {
    "new": "The CLI moved into a separate package: webpack-cli. Please install 'webpack-cli' in addition to webpack itself to use the CLI."
  }
}
```

### Updated webpack configs

```javascript
// mode is needed
config.mode = isTest || isDev ? 'development' : 'production';

// config.plugins.push(new webpack.optimize.UglifyJsPlugin({...})) is to be replaced by:
const UglifyJSPlugin = require('uglifyjs-webpack-plugin');

config.optimization = {
  minimizer: [
    new UglifyJSPlugin({
      uglifyOptions: {
        mangle: false,
      },
      // exclude: [/\.min\.js$/gi],
      sourceMap: true,
    }),
  ],
};
```

### Some other very nice tutorials

[A tale of Webpack 4 and how to finally configure it in the right way
Spoiler: there is no right way. #justwebpackthings](https://hackernoon.com/a-tale-of-webpack-4-and-how-to-finally-configure-it-in-the-right-way-4e94c8e7e5c1)
