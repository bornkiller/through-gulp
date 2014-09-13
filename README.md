# through-gulp
[![Build Status](https://travis-ci.org/bornkiller/through-gulp.svg?branch=master)](https://travis-ci.org/bornkiller/through-gulp)

A tiny wrapper around Node streams. To make gulp plugin write easier.
Inspired by through2, (https://github.com/rvagg/through2/), but much simplify
for gulp-plugin only.

## API
only one API provided to use.
```javascript
var through = require('through-gulp');
through(transformFunction, flushFunction);
```
Both argument has default value to pipe data next without processing.

## Usage
A simple demonstrate to write a gulp-plugin with through-gulp.
If you know nothing about gulp plugin, check this
(https://github.com/gulpjs/gulp/blob/master/docs/writing-a-plugin/guidelines.md)


```javascript
// PLUGIN_NAME: sample
var through = require('through-gulp');

function sample() {
  // creating a stream through which each file will pass
  var stream = through(function(file, encoding,callback) {
  	  // do whatever necessary to process the file 
      if (file.isNull()) {

      }
      if (file.isBuffer()) {

      }
      if (file.isStream()) {

      }
      // just pipe data next, or just do nothing to process file later in flushFunction
      // never forget callback to indicate that the file has been processed.
      this.push(file);
      callback();
    },function(callback) {
      // just pipe data next, just callback to indicate that the stream's over
      this.push(something);
      callback();
    });

  // returning the file stream
  return stream;
};

// exporting the plugin 
module.exports = sample;
```

then use the plugin with gulp
```javascript
var gulp = require('gulp');
var sample = require('sample');
gulp.task('sample', function() {
	return gulp.src(['source file'])
	    .pipe(sample())
	    .pipe(gulp.dest('file destiny'))
});
```
## Contact
*Email: hjj491229492@hotmail.com*.
