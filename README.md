# Acorn-JSX

[![Build Status](https://travis-ci.org/acornjs/acorn-jsx.svg?branch=master)](https://travis-ci.org/acornjs/acorn-jsx)
[![NPM version](https://img.shields.io/npm/v/acorn-jsx.svg)](https://www.npmjs.org/package/acorn-jsx)

<a href="https://stand-with-ukraine.pp.ua/"><img src="https://raw.githubusercontent.com/vshymanskyy/StandWithUkraine/main/banner-direct.svg" width="800"></a>

This is plugin for [Acorn](http://marijnhaverbeke.nl/acorn/) - a tiny, fast JavaScript parser, written completely in JavaScript.

It was created as an experimental alternative, faster [React.js JSX](http://facebook.github.io/react/docs/jsx-in-depth.html) parser. Later, it replaced the [official parser](https://github.com/facebookarchive/esprima) and these days is used by many prominent development tools.

> This is a fork intended to satisfy a specific use case while awaiting the migration of the original package to ESM - https://github.com/acornjs/acorn-jsx/issues/112

## Transpiler

Please note that this tool only parses source code to JSX AST, which is useful for various language tools and services. If you want to transpile your code to regular ES5-compliant JavaScript with source map, check out [Babel](https://babeljs.io/) and [Buble](https://buble.surge.sh/) transpilers which use `acorn-jsx` under the hood.

## Usage

Requiring this module provides you with an Acorn plugin that you can use like this:

```javascript
var acorn = require("acorn");
var jsx = require("@projectevergreen/acorn-jsx-esm");
acorn.Parser.extend(jsx()).parse("my(<jsx/>, 'code');");
```

Note that official spec doesn't support mix of XML namespaces and object-style access in tag names (#27) like in `<namespace:Object.Property />`, so it was deprecated in `acorn-jsx@3.0`. If you still want to opt-in to support of such constructions, you can pass the following option:

```javascript
acorn.Parser.extend(jsx({ allowNamespacedObjects: true }))
```

Also, since most apps use pure React transformer, a new option was introduced that allows to prohibit namespaces completely:

```javascript
acorn.Parser.extend(jsx({ allowNamespaces: false }))
```

Note that by default `allowNamespaces` is enabled for spec compliancy.

## License

This plugin is issued under the [MIT license](./LICENSE).
