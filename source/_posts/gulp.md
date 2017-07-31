---
title: gulp
date: 2017-01-14 15:00:27
tags:
categories: 'tools'
---

gulp常用配置和实例
<!-- more -->

概念
============================
Gulp.js 是一个简单、直观的前端自动化构建工具。崇尚代码优于配置，使复杂的任务更好管理。通过 NodeJS 的数据流的能力，能够快速构建。通过简单的 API 接口，只需几步就能搭建起自己的自动化项目构建工具。

## 安装 gulp

### 1.全局安装 gulp。
    默认你已经安装nodeJS，nodeJS自带包管理工具npm。首先需要初始化项目,建立package.json.
 ```js
    npm init --yes
 ```
   然后全局安装gulp
```js
    npm install -g gulp
```
### 2.在你需要的项目中安装gulp,作为项目依赖
```js
    npm install --save-dev gulp
```
### 3.安装gulp插件和常用gulp插件
gulp插件的安装方法大同小异
```js
    npm install --save-dev "插件名称"
```
一些常用的gulp插件:
[<font color=#0099ff size=3>gulp-htmlmin</font>](https://www.npmjs.com/package/gulp-htmlmin):压缩html，并且可以去掉注释
[<font color=#0099ff size=3>gulp-imagemin</font>](https://www.npmjs.com/package/gulp-imagemin):压缩图片利器,并且可以压缩svg图
[<font color=#0099ff size=3>gulp-uglify</font>](https://www.npmjs.com/package/gulp-uglify):压缩js利器
[<font color=#0099ff size=3>gulp-concat</font>](https://www.npmjs.com/package/gulp-concat):可以合并css或者js文件，已减少http请求
[<font color=#0099ff size=3>gulp-autoprefixer</font>](https://www.npmjs.com/package/gulp-autoprefixer):给css3的一些属性加浏览器前缀，很常用
[<font color=#0099ff size=3>gulp-rename</font>](https://www.npmjs.com/package/gulp-rename):看名字应该能理解，重命名一些文件
[<font color=#0099ff size=3>gulp-sass</font>](https://www.npmjs.com/package/gulp-sass):对css预编译语言sass和scss进行编译
[<font color=#0099ff size=3>gulp-jshint</font>](https://www.npmjs.com/package/gulp-jshint):代码校验
[<font color=#0099ff size=3>gulp-clean</font>](https://www.npmjs.com/package/gulp-clean):清空文件夹
### 4.建立gulpfile.js文件。
<font color=#c10000 size=3>说明</font>：gulpfile.js是gulp项目的配置文件，是位于项目根目录的普通js文件.
下面是一个简单的代码示例：
```js
/* 引入gulp文件 */
var gulp = require('gulp');

/* 引入gulp插件的文件 */ 
var concat = require('gulp-concat');
var uglify = require('gulp-uglify');
var imagemin = require('gulp-imagemin');
 
/*  要使用gulp插件进行压缩的图片路径和js路径 */
var paths = {
  scripts: ['client/js/**/*.js', '!client/external/**/*.js'],
  images: 'client/img/**/*'
};
 
gulp.task('scripts', function() {
  return gulp.src(paths.scripts)//通过gulp.src引入需要压缩的js文件
    .pipe(uglify())//执行js压缩
    .pipe(concat('all.min.js'))//把压缩后的文件和并到一个新文件中
    .pipe(gulp.dest('build/js'));//把新文件输出到build/js文件中
});
 
// Copy all static images
gulp.task('images', function() {
 return gulp.src(paths.images)//通过gulp.src引入需要压缩的图片文件
    .pipe(imagemin({optimizationLevel: 5}))//通过gulp-imagemin对图片进行压缩,optimizationLevel控制压缩大小,数字越小,图片大小越小.
    .pipe(gulp.dest('build/img'));//把图片输出到build/js文件中
});
 
gulp.task('watch', function() {//新建watch任务
  gulp.watch(paths.scripts, ['scripts']);//gulp.watch监控paths.scripts下的js文件，如果有改变，则执行'scripts'任务
  gulp.watch(paths.images, ['images']);
});
 
gulp.task('default', ['scripts', 'images', 'watch']);//新建默认任务
```
### 5.gulp执行

在命令提示符执行gulp任务
```js
    gulp '任务名称'//例如：gulp scripts
```
<font color=#c10000 size=3>说明</font>：当你执行gulp或者gulp default时会默认执行default任务里的所有任务,例如[‘testLess’,’elseTask’]。