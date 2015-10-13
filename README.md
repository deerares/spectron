# spectron

[![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg?style=flat)](http://standardjs.com/)
[![Build Status](https://travis-ci.org/kevinsawicki/spectron.svg?branch=master)](https://travis-ci.org/kevinsawicki/spectron)

Easily test your [Electron](http://electron.atom.io) apps using [ChromeDriver](https://code.google.com/p/selenium/wiki/ChromeDriver)
and [webdriverio](http://webdriver.io)

## Using

```sh
npm --save-dev spectron
```

Spectron works with any testing framework but the following example uses
[mocha](https://mochajs.org).

```js
var Application = require('spectron').Application
var assert = require('assert')
var path = require('path')

describe('application loading', function () {
  this.timeout(10000)

  var app = null

  beforeEach(function (done) {
    app = new Application({
      path: '/Applications/MyApp.app/Contents/MacOS/MyApp'
    })
    app.start(done)
  })

  afterEach(function (done) {
    if (app) {
      app.stop(done)
    }
    app = null
  })

  it('launches the application and shows an initial window', function (done) {
    app.client.windowHandles().then(function (response) {
      assert.equal(response.value.length, 1)
    }).then(done, done)
  })
})
```
