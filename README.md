# get-html

![Last version](https://img.shields.io/github/tag/Kikobeats/get-html.svg?style=flat-square)
[![Build Status](https://img.shields.io/travis/Kikobeats/get-html/master.svg?style=flat-square)](https://travis-ci.org/Kikobeats/get-html)
[![Coverage Status](https://img.shields.io/coveralls/Kikobeats/get-html.svg?style=flat-square)](https://coveralls.io/github/Kikobeats/get-html)
[![Dependency status](https://img.shields.io/david/Kikobeats/get-html.svg?style=flat-square)](https://david-dm.org/Kikobeats/get-html)
[![Dev Dependencies Status](https://img.shields.io/david/dev/Kikobeats/get-html.svg?style=flat-square)](https://david-dm.org/Kikobeats/get-html#info=devDependencies)
[![NPM Status](https://img.shields.io/npm/dm/get-html.svg?style=flat-square)](https://www.npmjs.org/package/get-html)
[![Donate](https://img.shields.io/badge/donate-paypal-blue.svg?style=flat-square)](https://paypal.me/Kikobeats)

> Get the HTML from any website, using prerendering when is necessary.

## Features

- Get HTML markup from any website (client side apps as well)
- Prerendering detection based on domains whitelist.
- Speed up process blocking ads trackers.
- Encoding body response properly.

## Install

```bash
$ npm install get-html --save
```

## Usage

```js
'use strict'

const getHtml = require('get-html')
;(async () => {
  const url = 'https://kikobeats.com'
  const { html, stats } = await getHTML(url)
  console.log(html)
})()
```

## API

### getHTML(url, [options])

#### url

*Required*<br>
Type: `string`

The target URL for getting the HTML markup.

#### options

##### prerender

Type: `boolean|string`<br>
Default: `'auto'`

Enable or disable prerendering as mechanism for getting the HTML markup explicitly.

The value `auto` means that that internally use a list of whitelist website that don't need to use prerendering by default. This list is used for speedup the process, using `fetch` mode for these websites.

See [fetchMode parameter](#fetchMode) for know more.

##### browserless

Type: `object`<br>

A [browserless](https://browserless.js.org/) instance to be used for interact with puppeteer. If you don't provide one, a browser instance will be created in each library call.

##### encoding

Type: `string`<br>
Default: `'utf-8'`

Encoding the HTML markup properly from the body response.

It determines the encode to use A Node.js library for converting HTML documents of arbitrary encoding into a target encoding (utf8, utf16, etc).

##### fetchMode

Type: `function`<br>

A function evaluation that will be invoked to determinate the resolutive `mode` for getting the HTML markup from the target URL.

The default `fetchMode` is:

```js
const getFetchMode = (url, { prerender }) => {
  if (prerender === false) return 'fetch'
  if (prerender !== 'auto') return 'prerender'
  return autoDomains.includes(parseDomain(url).domain) ? 'fetch' : 'prerender'
}
```

##### gotOptions

Type: `object`<br>

Under `mode=fetch`, pass configuration object to [got](https://www.npmjs.com/package/got).

##### puppeteerOpts

Type: `object`

Under non `mode=fetch`, pass configuration object to [puppeteer](https://www.npmjs.com/package/puppeteer).

## License

**get-html** © [Kiko Beats](https://kikobeats.com), released under the [MIT](https://github.com/Kikobeats/get-html/blob/master/LICENSE.md) License.<br>
Authored and maintained by Kiko Beats with help from [contributors](https://github.com/Kikobeats/get-html/contributors).

> [kikobeats.com](https://kikobeats.com) · GitHub [Kiko Beats](https://github.com/Kikobeats) · Twitter [@Kikobeats](https://twitter.com/Kikobeats)