# gulp-codception
> PHPSpec plugin for gulp 3

## Usage

First, install `gulp-phpspec` as a development dependency:

```shell
npm install --save-dev gulp-phpspec
```

Then, add it to your `gulpfile.js`:

```javascript
var phpspec = require('gulp-phpspec');

// option 1: default format
gulp.task('phpspec', function() {
	gulp.src('./spec/**/*.php').pipe(phpspec());
});

// option 2: with defined bin and options
gulp.task('phpspec', function() {
	var options = {debug: false};
	gulp.src('./spec/**/*.php').pipe(phpspec('./vendor/bin/phpspec run',options));
});

// option 3: supply callback to integrate something like notification (using gulp-notify)

var gulp    = require('gulp'),
    notify  = require('gulp-notify'),
    phpspec = require('gulp-phpspec');

gulp.task('phpspec', function() {
	var options = {notify: false};
	gulp.src('app/spec/**/*.php')
		.pipe(phpspec('', options))
		.on('error', notify.onError({
			title: "Testing Failed",
			message: "Error(s) occurred during test..."
		}))
		.pipe(notify({
			title: "Testing Passed",
			message: "All tests have passed..."
		}));
});


```

## API

### (codeceptpath,options,cb)

#### codeceptpath

Type: `String`

The path to the desired Codeception binary
- If not supplied, the defeault path will be ./vendor/bin/codecept

#### options.debug
Type: `Boolean (Default: false)`

Emit error details and shows command used in console

#### options.clear
Type: `Boolean (Default: false)`

Clear console before executing command

#### options.testClass
Type: `String`

Define a specific class for testing (supply full path to test class)

#### options.testSuite
Type: `String (Default all suites)`

Define a specific test suite to execute (acceptance, unit, functional)
Note: You can also supply any custom suites you may have created

#### options.flags
Type: `String (Default no flags)`

Define any custom flags you may wish to use during testing

```
var opts = {flags: '--silent --report'}
```

#### options.notify
Type: `Boolean (Default: false)`

Call user supplied callback to handle notification (use gulp-notify)

#### options.skipSuite
Type: `Array (Default: [])`

List of suite(s) to skip during test run

## Changelog

- 0.4.0: Expanded API
    - Added new option opts.skipSuite
    - Expanded plugin tests
    - Updated dependencies for jsHint and Mocha

- 0.3.0: Updated package.json to include test dependencies and scripts
    - Added updated test script (calls mocha and jshint)

- 0.2.0: Update Default Command - Windows Fix
    - Fixed default command when using windows

- 0.1.2: Code Refactoring and Cleanup
    - Added test/test.js
    - Updated documentation

- 0.0.1: Initial Release

## Credits

gulp-codeception written by Mike Erickson

E-Mail: [codedungeon@gmail.com](mailto:codedungeon@gmail.com)

Twitter: [@codedungeon](http://twitter.com/codedungeon)

Webiste: [codedungeon.org](http://codedungeon.org)