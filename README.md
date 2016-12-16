# gulp-jsoncombine-array

> jsoncombine-array plugin for [gulp](https://github.com/gulpjs/gulp)

## Usage

First, install `gulp-jsoncombine-array` as a dependency:

```shell
npm install --save-dev gulp-jsoncombine-array
```

Then, add it to your `gulpfile.js`:

** This plugin will collect all the json files provided to it, parse them, put them in a dictionary where the keys of that dictionary are the filenames (sans the '.json' suffix) and pass that to a processor function. That function decides how that output should look in the resulting file. **

```javascript
var gulp = require('gulp');
var jsoncombinearray = require("gulp-jsoncombine-array");

gulp.task('default', function(callback) {
	return gulp.src("./*.json")
		.pipe(jsoncombinearray("all-things.json",function(dataArray) {
			// do any work on data here
			return new Buffer(JSON.stringify(dataArray));
		}))
		.pipe(gulp.dest("./output"));
});
```

## API

### jsoncombine-array(fileName, processor)

#### fileName
Type: `String`  

The output filename

#### processor
Type: `Function`  

The processor function will be called with two parameters.

The first parameter is json array of the string contents of the file. The second parameter maps to a meta object containing the following keys:

* `cwd` The working directory
* `base` The base path
* `path` The full path to the file

The function should return a new `Buffer` that would be written to the output file.

## License

[MIT License](http://en.wikipedia.org/wiki/MIT_License)
