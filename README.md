# gulp-spawn

Plugin to spawn a CLI program for piping with [gulp](https://github.com/wearefractal/gulp). Uses [spawn](http://nodejs.org/api/child_process.html#child_process_child_process_spawn_command_args_options).

**This plugin has NOT been tested thoroughly**

## Usage

gulp-spawn options follow `child_process.spawn` conventions.

Not all CLI programs support piping. In fact, many newer ones don't. Some programs require that you pass certain arguments if you intend to use stdin and/or stdout. Please check the documentation of the program you intend to use to ensure piping is supported.

The following example pipes image files to ImageMagick's `convert`. In the case of `convert`, you must specify a `-` before arguments and after arguments if you wish to use stdin and stdout, respectively.

```javascript
var spawn = require("gulp-spawn");

// example using ImageMagick's convert
gulp.src("./src/images/*.{jpg,png,gif}")
	.pipe(spawn({
		cmd: "convert",
		args: [
			"-",
			"-resize",
			"50%",
			"-"
		],
		// optional
		filename: function(base, ext) {
			return base + "-half" + ext;
		}
	}))
	.pipe(gulp.dest("./dist/images/"));
```

## The UNIX Pipe Philosophy

If you write spawn programs please consider taking the time to support stdin & stdout. Piping is one of the many reasons UNIX systems have endured the test of time.
