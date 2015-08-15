express-busboy
--------------

A simple `body-parser` like module for express that 
uses [`connect-busboy`](https://github.com/mscdex/connect-busboy) under the hood.

It's designed to be more of a "drop in" replacement for `body-parser`.
With it populating `req.body`, there is very minimal code change needed to use it.

usage
-----

```js
var bb = require('express-busboy');
var app = express();

bb.extend(app);
```

The module will populate `req.body` and `req.files` like the `body-parser` module does.

configuration
-------------

```js
bb.extend(app, {
    //busboy options can go here
});
```

If you want to use the `body-parser` middleware for requests that aren't
multipart file uploads, use the `json: false` option:

```js
var bodyParser = require('body-parser');
app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json({ type: ['application/json', 'application/*json'] }));
bb.extend(app, {
    json: false,
    //busboy options can go here
});
```

file uploads
------------

By default file uploads are disabled, the `req.files` object will always be empty. You can activate them with:

```js
bb.extend(app, {
    upload: true,
    path: '/path/to/save/files'
});
```

`path` will default to: `os.tmpdir()/express-busboy/<uuid>/<the field name>/<filename>`.

If needed, we could potentially add a filter for which url's have the ability to upload files.

build
-----

[![Build Status](https://travis-ci.org/yahoo/express-busboy.svg?branch=master)](https://travis-ci.org/yahoo/express-busboy)
