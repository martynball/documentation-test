<!-- Space: WE -->
<!-- Parent: Web Documentation -->
<!-- Parent: Web Planner -->
<!-- Title: Gulp -->
<!-- Layout: (plain) -->

# Gulp

Below is the code to the gulpfile, simply pace this within your dealers theme folder called **gulp.js**, ensure that you enter your theme folder name within the ```THEME``` variable at the top.

To start gulping run the following command:
```
gulp --user 'username' --password 'password'
```

##JavaScript:
```
// Theme Folder

var THEME = "";

// End Theme Folder

// Dont mess under this line :)

// Include Essentials
var gulp = require('gulp');
var gutil = require('gulp-util');
var ftp = require('vinyl-ftp');
var minimist = require('minimist');
// Include plugins
var notify = require('gulp-notify');
var plumber = require('gulp-plumber');
var watch = require('gulp-watch');
var clean = require("gulp-clean");
// CSS Plugins
var less = require('gulp-less');
var autoprefixer = require('gulp-autoprefixer');
var cleanCSS = require('gulp-clean-css');
var gcmq = require('gulp-group-css-media-queries');
// Image plugins
var imagemin = require('gulp-imagemin');
// JS Plugins
var jshint = require('gulp-jshint');
var uglify = require('gulp-uglify');

var rename = require("gulp-rename");

var plumberErrorHandler = {
    errorHandler: notify.onError({
        title: 'Gulp',
        message: 'Error: <%= error.message %>',
        sound: 'beep'
    })
};
var args = minimist(process.argv.slice(2));
var conn = ftp.create({
    host: '185.182.88.3',
    user: args.user,
    password: args.password,
    parallel: 10,
    log: gutil.log,
    secureOptions: {rejectUnauthorized: false}
});

var config = {
    dev: !!gutil.env.dev
};

var themeimages = ['img-src/theme/**/*.jpg', 'img-src/theme/**/*.jpeg', 'img-src/theme/**/*.png', 'img-src/theme/**/*.svg', 'img-src/theme/**/*.gif'];
var carimages = ['img-src/cars/**/*.jpg', 'img-src/cars/**/*.jpeg', 'img-src/cars/**/*.png'];
var compressedtheme = ['img-src/theme-compressed/*.png', 'img-src/theme-compressed/*.jpg', 'img-src/theme-compressed/*.gif', 'img-src/theme-compressed/*.jpeg', 'img-src/theme-compressed/*.svg'];
var compressedcars = ['img-src/cars-compressed/*.png', 'img-src/cars-compressed/*.jpg', 'img-src/cars-compressed/*.jpeg'];

// Compile CSS from Less files including sub folders
gulp.task('compile-css', function () {
    return watch('css-src/less/**/*.less', function () {
        gulp.src('css-src/less/theme.less')
            .pipe(notify({message: '<%= file.relative %> compile started'}))
            .pipe(plumber(plumberErrorHandler))
            .pipe(less())
            .pipe(autoprefixer({browsers: ['last 3 versions']}))
            .pipe(config.dev ? gutil.noop() : gcmq())
            .pipe(config.dev ? gutil.noop() : cleanCSS())
            .pipe(gulp.dest('css-src'))
            .pipe(notify({message: "Less Compiled Successfully"}))
    });
});

gulp.task('js', function () {
    return watch(['js-src/**/*.js', '!js-src/**/*-min.js'], function (event) {
        gulp.src(event.path)
            .pipe(plumber(plumberErrorHandler))
            .pipe(jshint())
            .pipe(jshint.reporter('default'))
            .pipe(jshint.reporter('fail')).on('error', function (e) {
            this.emit('end');
        })
            .pipe(notify({message: '<%= file.relative %> compile started'}))
            .pipe(uglify())
            .pipe(rename({suffix: '-min'}))
            .pipe(gulp.dest('js-src/min'));
    });
});
gulp.task('theme', function () {
    return watch(themeimages, {awaitWriteFinish: true}, function (event) {
        gulp.src(event.path)
            .pipe(notify({message: '<%= file.relative %> compression started'}))
            .pipe(imagemin({optimizationLevel: 5, progressive: true, interlaced: true}))
            .pipe(plumber(plumberErrorHandler))
            .pipe(gulp.dest('img-src/theme-compressed'))
            .pipe(notify({message: '<%= file.relative %> compressed'}));
    });
});
gulp.task('cars', function () {
    return watch(carimages, {awaitWriteFinish: true}, function (event) {
        gulp.src(event.path)
            .pipe(notify({message: '<%= file.relative %> compression started'}))
            .pipe(imagemin({optimizationLevel: 5, progressive: true, interlaced: true}))
            .pipe(plumber(plumberErrorHandler))
            .pipe(gulp.dest('img-src/cars-compressed'))
            .pipe(notify({message: '<%= file.relative %> compressed'}));
    });
});
gulp.task('templates', function () {
    var count = 0;
    var action = function (event) {
        gulp.src([event.path], {base: 'templates/', buffer: false})
            .pipe(conn.dest('/templates/' + THEME + '').on('error', function () {
                if (count <= 3) {
                    console.log('Failed to upload template, retrying... (' + count + ')');
                    count++;
                    action(event);
                } else {
                    count = 0;
                }
            }))
            .pipe(notify("<%= file.relative %> uploaded!"))
    };

    return watch('templates/**/*', {awaitWriteFinish: true}, (event) => {
        action(event)
    });
});

gulp.task('server', function () {

    var cssCount = 0;
    var jsCount = 0;
    var lessCount = 0;
    var themeCount = 0;
    var carsCount = 0;

    var less = function (event) {
        return gulp.src('css-src/less/**/*.less', {base: 'css-src/less/', buffer: false})
            .pipe(conn.dest('/css-src/' + THEME + '/less').on('error', function () {
                if (lessCount <= 3) {
                    console.log('Failed to upload less, retrying... (' + lessCount + ')');
                    lessCount++;
                    less(event);
                } else {
                    lessCount = 0;
                }
            }))
            .pipe(notify("<%= file.relative %> Uploaded!"));
    };

    var css = function (event) {
        return gulp.src([event.path], {base: 'css-src/', buffer: false})
            .pipe(notify({message: "Less Compiled Successfully"}))
            .pipe(conn.dest('/css-src/' + THEME + '').on('error', function () {
                if (cssCount <= 3) {
                    console.log('Failed to upload css, retrying... (' + cssCount + ')');
                    cssCount++;
                    css(event);
                } else {
                    cssCount = 0;
                }
            }))
            .pipe(notify("<%= file.relative %> Uploaded!"));
    };
    var js = function (event) {
        return gulp.src([event.path], {base: 'js-src/min', buffer: false})
            .pipe(notify({message: "JS Compiled Successfully"}))
            .pipe(conn.dest('/js-src/' + THEME + '').on('error', function () {
                if (jsCount <= 3) {
                    console.log('Failed to upload js, retrying... (' + jsCount + ')');
                    jsCount++;
                    js(event);
                } else {
                    jsCount = 0;
                }
            }))
            .pipe(notify("<%= file.relative %> uploaded!"));
    };
    var theme = function (event) {
        return gulp.src([event.path], {base: 'img-src/theme-compressed/', buffer: false})
            .pipe(conn.dest('/img-src/' + THEME + '/theme').on('error', function () {
                if (themeCount <= 3) {
                    console.log('Failed to upload theme, retrying... (' + themeCount + ')');
                    themeCount++;
                    theme(event);
                } else {
                    themeCount = 0;
                }
            }))
            .pipe(notify("<%= file.relative %> uploaded!"));
    };
    var cars = function (event) {
        return gulp.src([event.path], {base: 'img-src/cars-compressed/', buffer: false})
            .pipe(conn.dest('/img-src/' + THEME + '/cars/170x120/').on('error', function () {
                if (carsCount <= 3) {
                    console.log('Failed to upload cars, retrying... (' + carsCount + ')');
                    carsCount++;
                    cars(event);
                } else {
                    carsCount = 0;
                }
            }))
            .pipe(notify("<%= file.relative %> uploaded!"));
    };

    // upload to server
    watch('css-src/*.css', {awaitWriteFinish: true}, (event) => {
       css(event)
    });
    watch('js-src/min/**/*-min.js', {awaitWriteFinish: true}, (event) => {
        js(event)
    });
    watch('css-src/less/**/*.less', {awaitWriteFinish: true}, (event) => {
        less(event)
    });
    watch(compressedtheme, {awaitWriteFinish: true}, (event) => {
        theme(event)
    });
    watch(compressedcars, {awaitWriteFinish: true}, function (event) {
        cars(event)
    });
});

gulp.task('remove-template', function (cb) {
    conn.delete('/templates/' + THEME + '/' + args.file + '', cb);
    gulp.src('templates/' + args.file + '', {read: false}).pipe(clean())
        .pipe(notify("Template " + args.file + " deleted!!"));
});
gulp.task('remove-theme-image', function (cb) {
    conn.delete('/img-src/' + THEME + '/theme/' + args.file + '', cb)
    gulp.src('img-src/theme/' + args.file + '', {read: false}).pipe(clean());
    gulp.src('img-src/theme-compressed/' + args.file + '', {read: false}).pipe(clean())
        .pipe(notify("Image " + args.file + " deleted!!"));
});
gulp.task('remove-cars-image', function (cb) {
    conn.delete('/img-src/' + THEME + '/cars/170x120/' + args.file + '', cb)
    gulp.src('img-src/cars/' + args.file + '', {read: false}).pipe(clean());
    gulp.src('img-src/cars-compressed/' + args.file + '', {read: false}).pipe(clean())
        .pipe(notify("Image " + args.file + " deleted!!"));
});
gulp.task('no-theme', function () {
    gulp.src('')
    .pipe(notify({
        title: 'Error',
        subtitle: 'Error: Can\'t start Gulping without a straw!',
        message: '(Theme Folder)',
        sound: "Submarine"
    }));
});
gulp.task('default', function () {
    if (THEME !== "") {
        gulp.start('compile-css', 'templates', 'js', 'theme', 'cars', 'server');
    } else {
        gulp.start('no-theme');
    }
});

```
