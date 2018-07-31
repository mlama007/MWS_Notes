# Gulp

## Most basic Gulp file:

```js
var gulp = require('gulp');

gulp.task('default', defaultTask);

function defaultTask(done) {
  // place code for your default task here
  done();
}
```

## Convert SASS into CSS

```js
var gulp = require('gulp');
var sass = require('gulp-sass');

gulp.task('default', function() {
	console.log('hello world!');
});

gulp.task('styles', function() {
	gulp.src('sass/**/*.scss')
		.pipe(sass().on('error', sass.logError))
		.pipe(gulp.dest('./css'));
});
```

### With autoprefixer (generates right prefixes for CSS files!)

```js
var gulp = require('gulp');
var sass = require('gulp-sass');
var autoprefixer = require('gulp-autoprefixer');

gulp.task('default', function() {
	console.log('hello world!');
});

gulp.task('styles', function() {
	gulp.src('sass/**/*.scss')
		.pipe(sass().on('error', sass.logError))
		.pipe(autoprefixer({
			browsers: ['last 2 versions']
		}))
		.pipe(gulp.dest('./css'));
});
```


### Add watcher to instantly see changes made to code

```js
var gulp = require('gulp');
var sass = require('gulp-sass');
var autoprefixer = require('gulp-autoprefixer');

gulp.task('default', function() {
	gulp.watch('sass/**/*.scss',['styles']);
});

gulp.task('styles', function() {
	gulp.src('sass/**/*.scss')
		.pipe(sass().on('error', sass.logError))
		.pipe(autoprefixer({
			browsers: ['last 2 versions']
		}))
		.pipe(gulp.dest('./css'));
});
```

# Tools:

Start local 3000
[Broswer Sync](https://www.browsersync.io/)
`npm install -g browser-sync`
Static Sites:
`browser-sync start --server --files "css/*.css`
Dynamic Sites:
`browser-sync start --proxy "myproject.dev" --files "css/*.css`

## Gulp

`npm install gulp@3.9.0`

Create a watch task in gulpfile.js
`gulp _task_`

```js
var gulp = require('gulp');
var sass = require('gulp-sass');
var autoprefixer = require('gulp-autoprefixer');

gulp.task('default', function() {
	gulp.watch('sass/**/*.scss',['styles']);
});

gulp.task('styles', function() {
	gulp.src('sass/**/*.scss')
		.pipe(sass().on('error', sass.logError))
		.pipe(autoprefixer({
			browsers: ['last 2 versions']
		}))
		.pipe(gulp.dest('./css'));
});
```

If you install `Broswer Sync` in project file, you can include it in you `gruntfile.js` and just run grunt to open it.

```js
var gulp = require('gulp');
var sass = require('gulp-sass');
var autoprefixer = require('gulp-autoprefixer');
var browserSync = require('browser-sync').create();

gulp.task('default', function() {
	gulp.watch('sass/**/*.scss',['styles']);
});

gulp.task('styles', function() {
	gulp.src('sass/**/*.scss')
		.pipe(sass().on('error', sass.logError))
		.pipe(autoprefixer({
			browsers: ['last 2 versions']
		}))
		.pipe(gulp.dest('./css'));
});


browserSync.init({
     server: "./"
 });
 browserSync.stream();
 ```

 # Prevention of erros

 #Linting

 Automatically check JS for errors (Code Style / Syntax)

 * JSHint
 * JSCS
 * ESLint

### Install

`npm install eslint`

Download any plugins on your editor
`ESLint`

## Setting up ESLint in Gulp

[ESLint](https://www.npmjs.com/package/gulp-eslint)

`npm install gulp-eslint@1.0.0`

Include `browserSync.reload();` where needed

```js
var gulp = require('gulp');
var sass = require('gulp-sass');
var autoprefixer = require('gulp-autoprefixer');
var browserSync = require('browser-sync').create();
var eslint = require('gulp-eslint');

gulp.task('default', ['styles', 'lint'], function() {
	gulp.watch('sass/**/*.scss',['styles']);
	gulp.watch('js/**/*.js',['lint']);
	
	browserSync.init({
		server: "./"
	});
});

gulp.task('styles', function() {
	gulp.src('sass/**/*.scss')
		.pipe(sass().on('error', sass.logError))
		.pipe(autoprefixer({
			browsers: ['last 2 versions']
		}))
		.pipe(gulp.dest('./css'));
		.pipe(browserSync.stream());
});

gulp.task('lint', function() {
	browserSync.reload();
	return gulp.src(['js/**/*.js'])
        // eslint() attaches the lint output to the "eslint" property
        // of the file object so it can be used by other modules.
        .pipe(eslint())
        // eslint.format() outputs the lint results to the console.
        // Alternatively use eslint.formatEach() (see Docs).
        .pipe(eslint.format())
        // To have the process exit with an error code (1) on
        // lint error, return the stream and pipe to failAfterError last.
		.pipe(eslint.failAfterError());	
});
```


## Unit Tests

### (PhantomJS) 
[gulp-Jasmine-phantom](https://www.npmjs.com/package/gulp-jasmine-phantom)

`npm install gulp-Jasmine-phantom`

```js
/*eslint-env node */

var gulp = require('gulp');
var sass = require('gulp-sass');
var autoprefixer = require('gulp-autoprefixer');
var browserSync = require('browser-sync').create();
var eslint = require('gulp-eslint');
var jasmine = require('gulp-jasmine-phantom');

gulp.task('default', ['styles', 'lint'], function() {
	gulp.watch('sass/**/*.scss',['styles']);
	gulp.watch('js/**/*.js',['lint']);
	
	browserSync.init({
		server: "./"
	});
});

gulp.task('styles', function() {
	gulp.src('sass/**/*.scss')
		.pipe(sass().on('error', sass.logError))
		.pipe(autoprefixer({
			browsers: ['last 2 versions']
		}))
		.pipe(gulp.dest('./css'))
		.pipe(browserSync.stream());
});

gulp.task('lint', function() {
	browserSync.reload();
	return gulp.src(['js/**/*.js'])
        // eslint() attaches the lint output to the "eslint" property
        // of the file object so it can be used by other modules.
        .pipe(eslint())
        // eslint.format() outputs the lint results to the console.
        // Alternatively use eslint.formatEach() (see Docs).
        .pipe(eslint.format())
        // To have the process exit with an error code (1) on
        // lint error, return the stream and pipe to failAfterError last.
		.pipe(eslint.failAfterError());	
});

gulp.task('tests', function () {
	gulp.src('tests/spec/extraSpec.js')
		.pipe(jasmine({
			integration: true,
			vendor: 'js/**/*.js'
		}));
});
```

# Optimization
Move files into `dist` folder
	* dist/
		* css/
		* js/
		* index.html

Change `styles` destination to correct folder


```js
/*eslint-env node */

var gulp = require('gulp');
var sass = require('gulp-sass');
var autoprefixer = require('gulp-autoprefixer');
var browserSync = require('browser-sync').create();
var eslint = require('gulp-eslint');
var jasmine = require('gulp-jasmine-phantom');

gulp.task('default', ['copy-html', 'copy-images','styles', 'lint'], function() {
	gulp.watch('sass/**/*.scss', ['styles']);
	gulp.watch('js/**/*.js', ['lint']);
	gulp.watch('index.html', ['copy-html']);

	browserSync.init({
		server: './dist'
	});
});

// HTML
// copies html file into dist folder and reloads
gulp.task('copy-html', function () {
	gulp.src('./index.html')
		.pipe(gulp.dest('./dist'))
		.pipe(browserSync.stream());
});

// IMGs
// copies all imgs into dist folder
gulp.task('copy-images', function () {
	gulp.src('img/*')
		.pipe(gulp.dest('./dist/img'));
});

// CSS 
// converts scss into css and puts files into dist folder and reloads
gulp.task('styles', function() {
	gulp.src('sass/**/*.scss')
		.pipe(sass().on('error', sass.logError))
		.pipe(autoprefixer({
			browsers: ['last 2 versions']
		}))
		.pipe(gulp.dest('dist/css'))
		.pipe(browserSync.stream());
});

// JS
gulp.task('lint', function () {
	browserSync.reload();
	return gulp.src(['js/**/*.js'])
		// eslint() attaches the lint output to the eslint property
		// of the file object so it can be used by other modules.
		.pipe(eslint())
		// eslint.format() outputs the lint results to the console.
		// Alternatively use eslint.formatEach() (see Docs).
		.pipe(eslint.format())
		// To have the process exit with an error code (1) on
		// lint error, return the stream and pipe to failOnError last.
		.pipe(eslint.failOnError());
});

// Tests
gulp.task('tests', function () {
	gulp.src('tests/spec/extraSpec.js')
		.pipe(jasmine({
			integration: true,
			vendor: 'js/**/*.js'
		}));
});
```

concatenate CSS and JS files together by using
```
.pipe(sass({outputsyle: 'compressed'}));
```

## Concat

`npm install gulp-concat`

## Minification

`npm install gulp-uglify`

```js
/*eslint-env node */

var gulp = require('gulp');
var sass = require('gulp-sass');
var autoprefixer = require('gulp-autoprefixer');
var browserSync = require('browser-sync').create();
var eslint = require('gulp-eslint');
var jasmine = require('gulp-jasmine-phantom');
var concat = require('gulp-concat');
var uglify = require('gulp-uglify');

gulp.task('default', ['copy-html', 'copy-images','styles', 'lint'], function() {
	gulp.watch('sass/**/*.scss', ['styles']);
	gulp.watch('js/**/*.js', ['lint']);
	gulp.watch('index.html', ['copy-html']);

	browserSync.init({
		server: './dist'
	});
});

// produce production ready version of site
gulp.task('dist', [
	'copy-html',
	'copy-images',
	'styles',
	'lint',
	'scripts-dist'
]);

// HTML
// copies html file into dist folder and reloads
gulp.task('copy-html', function () {
	gulp.src('./index.html')
		.pipe(gulp.dest('./dist'))
		.pipe(browserSync.stream());
});

// IMGs
// copies all imgs into dist folder
gulp.task('copy-images', function () {
	gulp.src('img/*')
		.pipe(gulp.dest('./dist/img'));
});

// CSS 
// converts scss into css and puts files into dist folder and reloads
gulp.task('styles', function() {
	gulp.src('sass/**/*.scss')
		.pipe(sass().on('error', sass.logError))
		.pipe(autoprefixer({
			browsers: ['last 2 versions']
		}))
		.pipe(gulp.dest('dist/css'))
		.pipe(browserSync.stream());
});

// JS
gulp.task('lint', function () {
	browserSync.reload();
	return gulp.src(['js/**/*.js'])
		// eslint() attaches the lint output to the eslint property
		// of the file object so it can be used by other modules.
		.pipe(eslint())
		// eslint.format() outputs the lint results to the console.
		// Alternatively use eslint.formatEach() (see Docs).
		.pipe(eslint.format())
		// To have the process exit with an error code (1) on
		// lint error, return the stream and pipe to failOnError last.
		.pipe(eslint.failOnError());
});

//Combine all js into dist/all.js
gulp.task('scripts', function() {
	gulp.src('js/**/*.js')
		.pipe(concat('all.js'))
		.pipe(gulp.dest('dist/js'));
});

//Combine all js into dist/all.js and minify
gulp.task('scripts-dist', function() {
	gulp.src('js/**/*.js')
		.pipe(concat('all.js'))
		.pipe(uglify())
		.pipe(gulp.dest('dist/js'));
});

// Tests
gulp.task('tests', function () {
	gulp.src('tests/spec/extraSpec.js')
		.pipe(jasmine({
			integration: true,
			vendor: 'js/**/*.js'
		}));
});
```

## Transpilers

## BabelJS
`npm install babel`
`npm install --save-dev babel-core`

# JavaScript Source Maps

[Source maps](https://www.npmjs.com/package/gulp-sourcemaps) are files that associate line numbers from the processed file to the original. This way the browser can lookup the current line number in the sourcemap and open the right source file at the correct line when debugging. 

## Setup
`npm i gulp-sourcemaps`


add to code:
``` js 
/*eslint-env node */

var gulp = require('gulp');
var sass = require('gulp-sass');
var autoprefixer = require('gulp-autoprefixer');
var browserSync = require('browser-sync').create();
var eslint = require('gulp-eslint');
var jasmine = require('gulp-jasmine-phantom');
var concat = require('gulp-concat');
var uglify = require('gulp-uglify');
var babel = require('gulp-babel');
var sourcemaps = require('gulp-sourcemaps');

gulp.task('default', ['copy-html', 'copy-images','styles', 'lint'], function() {
	gulp.watch('sass/**/*.scss', ['styles']);
	gulp.watch('js/**/*.js', ['lint']);
	gulp.watch('index.html', ['copy-html']);

	browserSync.init({
		server: './dist'
	});
});

// produce production ready version of site
gulp.task('dist', [
	'copy-html',
	'copy-images',
	'styles',
	'lint',
	'scripts-dist'
]);

// HTML
// copies html file into dist folder and reloads
gulp.task('copy-html', function () {
	gulp.src('./index.html')
		.pipe(gulp.dest('./dist'))
		.pipe(browserSync.stream());
});

// IMGs
// copies all imgs into dist folder
gulp.task('copy-images', function () {
	gulp.src('img/*')
		.pipe(gulp.dest('./dist/img'));
});

// CSS 
// converts scss into css and puts files into dist folder and reloads
gulp.task('styles', function() {
	gulp.src('sass/**/*.scss')
		.pipe(sass().on('error', sass.logError))
		.pipe(autoprefixer({
			browsers: ['last 2 versions']
		}))
		.pipe(gulp.dest('dist/css'))
		.pipe(browserSync.stream());
});

// JS
gulp.task('lint', function () {
	browserSync.reload();
	return gulp.src(['js/**/*.js'])
		// eslint() attaches the lint output to the eslint property
		// of the file object so it can be used by other modules.
		.pipe(eslint())
		// eslint.format() outputs the lint results to the console.
		// Alternatively use eslint.formatEach() (see Docs).
		.pipe(eslint.format())
		// To have the process exit with an error code (1) on
		// lint error, return the stream and pipe to failOnError last.
		.pipe(eslint.failOnError());
});

//Combine all js into dist/all.js
gulp.task('scripts', function() {
	gulp.src('js/**/*.js')
		.pipe(babel())
		.pipe(concat('all.js'))
		.pipe(gulp.dest('dist/js'));
});

//Combine all js into dist/all.js and minify
gulp.task('scripts-dist', function() {
	gulp.src('js/**/*.js')
		.pipe(sourcemaps.init())
		.pipe(babel())
		.pipe(concat('all.js'))
		.pipe(uglify())
		.pipe(sourcemaps.write())
		.pipe(gulp.dest('dist/js'));
});

// Tests
gulp.task('tests', function () {
	gulp.src('tests/spec/extraSpec.js')
		.pipe(jasmine({
			integration: true,
			vendor: 'js/**/*.js'
		}));
});
```

# Images

## Image Compression
`npm i imagemin`
`npm gulp-imagemin`
`npm i imagemin-pngquant`

TBC


# Tools to copy / paste
[yeoman](http://yeoman.io/)
[Web Starter Kit](https://developers.google.com/web/tools/starter-kit/)