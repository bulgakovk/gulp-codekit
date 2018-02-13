#gulp-codekit [![NPM version][npm-image]][npm-url] ![Travis build][travis-image]
>Makes inclusion of files a breeze.  
Supports CodeKit and Prepros include directives.
Heavily based on [gulp-include](http://github.com/wiledal/gulp-include) by [Hugo Wiledal](http://github.com/wiledal)

## Features
* Concatenate files with full control
* Respects indentation whitespace
* Uses [globs](https://www.npmjs.com/package/glob) for simple path control
* Works recursively (files can include files that can include files, and so on)

## Installation
```shell
npm i gulp-codekit-extended
```
## Usage
Example `gulpfile.js`:
```javascript
var gulp          = require("gulp"),
    include       = require("gulp-include");

gulp.task("scripts", function() {
  console.log("-- gulp is running task 'scripts'");

  gulp.src("src/js/main.js")
    .pipe(include())
      .on('error', console.log)
    .pipe(gulp.dest("dist/js"));
});

gulp.task("default", ["scripts"]);

```

## Options
* `extensions` (optional)
	* Takes a `String` or an `Array` of extensions, eg: `"js"` or `["js", "coffee"]`
	* If set, all directives that does not match the extension(s) will be ignored

## Include directives
`gulp-include` uses directives similar to `sprockets` or `snockets`. A _directive_ is a comment in your files that `gulp-include` recognizes as a command.
  
Example directives:
```javascript
//=require vendor/jquery.js
//=require vendor/**/*.js
//=include relative/path/to/file.js
// @codekit-append relative/path/to/file.js
// @codekit-prepend relative/path/to/file.js

> **Note:** Currently codekit-prepend does the same as codekit-append, and works like an include

```
```css
/*=include relative/path/to/file.css */
```
```coffee
#=include relative/path/to/file.coffee
```
```html
<!--=include relative/path/to/file.html -->
```

The contents of the referenced file will replace the file.
  
### `require` vs. `include`
A file that is included with `require` will only be included if it has not been included  before. Files included with `include` will _always_ be included.  
For instance, let's say you want to include `jquery.js` only once, and before any of your other scripts in the same folder.
```javascript
//=require vendor/jquery.js
//=require vendor/*.js
```
Note: This also works recursively. If for instance, for the example above, if another file in the folder `vendor` is also including `jquery.js` with the `require`-directive it will be ignored.

## Release log

#### 0.1.0
* Basic codekit-append

## Licence
(MIT License)

Copyright (c) 2014 Hugo Wiledal

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.


[travis-image]: https://travis-ci.org/designbyadrian/gulp-codekit.svg?branch=master

[npm-url]: https://npmjs.org/package/gulp-codekit
[npm-image]: https://badge.fury.io/js/gulp-codekit.svg
