# markdown-it-emoji

[![Build Status](https://img.shields.io/travis/markdown-it/markdown-it-emoji/master.svg?style=flat)](https://travis-ci.org/markdown-it/markdown-it-emoji)
[![NPM version](https://img.shields.io/npm/v/markdown-it-emoji.svg?style=flat)](https://www.npmjs.org/package/markdown-it-emoji)
[![Coverage Status](https://img.shields.io/coveralls/markdown-it/markdown-it-emoji/master.svg?style=flat)](https://coveralls.io/r/markdown-it/markdown-it-emoji?branch=dev)

> Emoji syntax plugin for [markdown-it](https://github.com/markdown-it/markdown-it)
markdown parser.

Two versions:

- __Full__ (default), with all github supported emojies.
- [Light](https://github.com/markdown-it/markdown-it-emoji/blob/master/lib/data/light.json), with only well supported unicode emojies and reduced size.

Also supports [shortcuts](https://github.com/markdown-it/markdown-it-emoji/blob/master/lib/data/shortcuts.json) like `:)`, `:-(`, ...


## Install

node.js, browser:

```bash
npm install markdown-it-emoji --save
bower install markdown-it-emoji --save
```

## Use

### init

```js
var md = require('markdown-it')();
var emoji = require('markdown-it-emoji');
// Or for light version
// var emoji = require('markdown-it-emoji/light');

md.use(emoji [, options]);
```

Options are not mantatory:

- __defs__ (Object) - rewrite available emojies definitions
  - example: `{ name1: char1, name2: char2, ... }`
- __enabled__ (Array) - disable all emojies except whitelisted
- __shortcuts__ (Object) - rewrite default shortcuts
  - emample: `{ "smile": [ ":)", ":-)" ], "laughing": ":D" }`

Differences in browser. If you load script directly into the page, without
package system, module will add itself globally with name `markdownitEmoji`.
Then, init will look a bit different:

```js
var md = window.markdownit().use(window.markdownitEmoji);
```


### change output

By default, emojies are rendered as appropriate unicode chars. But you can change
renderer function as you wish.

Render as span blocks (for example, to use custom iconic font):

```js
// ...
// initialize

md.renderer.emoji = function(token, idx) {
  return '<span class="emoji emoji_' + token[idx].name + '></span>';
}
```

Or use [twemoji](https://github.com/twitter/twemoji):

```js
// ...
// initialize

var twemoji = require('twemoji')

md.renderer.emoji = function(token, idx) {
  return twemoji.parse(token[idx].to);
}
```


## License

[MIT](https://github.com/markdown-it/markdown-it-emoji/blob/master/LICENSE)
