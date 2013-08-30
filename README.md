# grunt-contrib-jst [![Build Status](https://travis-ci.org/gruntjs/grunt-contrib-jst.png?branch=master)](https://travis-ci.org/gruntjs/grunt-contrib-jst)

> Precompile Underscore & EJS templates to JST file.



## Getting Started
This plugin requires Grunt `~0.4.0`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-contrib-jst --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-contrib-jst');
```

*This plugin was designed to work with Grunt 0.4.x. If you're still using grunt v0.3.x it's strongly recommended that [you upgrade](http://gruntjs.com/upgrading-from-0.3-to-0.4), but in case you can't please use [v0.3.1](https://github.com/gruntjs/grunt-contrib-jst/tree/grunt-0.3-stable).*



## Jst task
_Run this task with the `grunt jst` command._

Task targets, files and options may be specified according to the grunt [Configuring tasks](http://gruntjs.com/configuring-tasks) guide.

_This plugin uses [the Lo-Dash library](http://lodash.com/) to generate JavaScript template functions. Some developers generate template functions dynamically during development. If you are doing so, please be aware that the functions generated by this plugin may differ from those created at run-time. For instance, [the Underscore.js library](http://underscorejs.org/) will throw an exception if templates reference undefined top-level values, while Lo-Dash will silently insert an empty string in their place._
### Options

#### separator
Type: `String`
Default: linefeed + linefeed

Concatenated files will be joined on this string.

#### namespace
Type: `String`
Default: 'JST'

The namespace in which the precompiled templates will be assigned. Use dot notation (e.g. App.Templates) for nested namespaces or false for no namespace wrapping. When false with amd option set true, templates will be returned directly from the AMD wrapper.

#### processName
Type: `function`
Default: null

This option accepts a function which takes one argument (the template filepath) and returns a string which will be used as the key for the precompiled template object.  The example below stores all templates on the default JST namespace in capital letters.

```js
options: {
  processName: function(filename) {
    return filename.toUpperCase();
  }
}
```

#### templateSettings
Type: `Object`
Default: null

The settings passed to underscore or ejs when compiling templates.

```js
jst: {
  compile: {
    options: {
      templateSettings: {
        interpolate : /\{\{(.+?)\}\}/g
      }
    },
    files: {
      "path/to/compiled/templates.js": ["path/to/source/**/*.html"]
    }
  }
}
```

#### prettify
Type: `boolean`
Default: false

When doing a quick once-over of your compiled template file, it's nice to see
an easy-to-read format that has one line per template. This will accomplish
that.

```js
options: {
  prettify: true
}
```

#### amd
Type: `boolean`
Default: false

Wraps the output file with an AMD define function and returns the compiled template namespace unless namespace has been explicitly set to false in which case the template function will be returned directly.

```js
define(function() {
    //...//
    return this['[template namespace]'];
});
```

Example:
```js
options: {
  amd: true
}
```

#### processContent
Type: `function`

This option accepts a function which takes one argument (the file content) and
returns a string which will be used as template string.
The example below strips whitespace characters from the beginning and the end of
each line.

```js
options: {
  processContent: function(src) {
    return src.replace(/(^\s+|\s+$)/gm, '');
  }
}
```

### Usage Examples

NB: Anything ending with .ejs is assumed to an EJS template, otherwise an underscore template

```js
jst: {
  compile: {
    options: {
      templateSettings: {
        interpolate : /\{\{(.+?)\}\}/g
      }
    },
    files: {
      "path/to/compiled/templates.js": ["path/to/source/**/*.html"],
      "path/to/compiled/templates.ejs": ["path/to/source/**/*.ejs"]
    }
  }
}
```


## Release History

 * 2013-08-30   v0.5.2   EJS Support
 * 2013-07-14   v0.5.1   Display filepath when fails to compile.
 * 2013-03-06   v0.5.0   When `namespace` is false and `amd` is true, return templates directly from AMD wrapper. Rename `amdwrapper` option to `amd` to match grunt-contrib-handlebars.
 * 2013-02-15   v0.4.1   First official release for Grunt 0.4.0.
 * 2012-01-29   v0.4.1rc7   Correct line endings for lodash output on windows.
 * 2013-01-23   v0.4.0rc7   Updating grunt/gruntplugin dependencies to rc7. Changing in-development grunt/gruntplugin dependency versions from tilde version ranges to specific versions.
 * 2013-01-09   v0.4.0rc5   Updating to work with grunt v0.4.0rc5. Switching to this.files api.
 * 2012-10-12   v0.3.1   Rename grunt-contrib-lib dep to grunt-lib-contrib.
 * 2012-08-23   v0.3.0   Options no longer accepted from global config key.
 * 2012-08-16   v0.2.3   Support for nested namespaces.
 * 2012-08-12   v0.2.2   Added processName functionality & escaping single quotes in filenames.
 * 2012-08-10   v0.2.0   Refactored from grunt-contrib into individual repo.

---

Task submitted by [Tim Branyen](http://tbranyen.com)

*This file was generated on Sun Jul 14 2013 19:23:02.*
