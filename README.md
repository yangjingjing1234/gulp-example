# gulp-example


这是一个本地的gulp 编译小例子 很好用


入坑1::

webpack = require("webpack-stream"),  这个是gulp-stream 更改之后的用在gulp中的
wp = require('webpack'),   这是webpack 方法里面需要用插件的时候，new 一个webpack 对象的时候，必须用这个。

入坑2::

webpack 思想就是让所有css  img js 当成模块被加载，但是在node环境中这种方式编译出来的文件会遇到各种bug

所以最终定下用gulp 来编辑jsx ,es6, 只用webpack 来打包编译之后的文件。

入坑3::

如果不用webpac 编译模块，那么在react中是不能用 import "css/index.css" 这种模式写的，因此在react 代码中最好就直接写es6
语法，对于公共的库在页面中引入好了.

入坑4::
有些东西看会了，可是只要一写就会出错下边就是一个例子：
gulp.task("es6:compile",function(){
    return gulp.src(PATH.jsPath+"**/*.es6")
		//.pipe(changed(PATH.jsPath+"**/*.es6"))
		.pipe(plumber({errorHandler:notify.onError("ES6 Error:<%=error.message %>")}))
		.pipe(babel({"presets":[es2015]}))
		.pipe(gulp.dest(PATH.distJsPath))
		.pipe(selfNotify({title:"ES6 to js and minify",message:"ES6 package task complete."}));
});
gulp.task("es6:compile",function(){
    return gulp.src(PATH.jsPath+"jsx/*.es6")
		//.pipe(changed(PATH.jsPath+"**/*.es6"))
		.pipe(plumber({errorHandler:notify.onError("ES6 Error:<%=error.message %>")}))
		.pipe(babel({"presets":[es2015]}))
		.pipe(gulp.dest(PATH.distJsPath))
		.pipe(selfNotify({title:"ES6 to js and minify",message:"ES6 package task complete."}));
});

2者唯一的区别就是入口路径那里；其他都是一模一样，但是生成路径却改变了,入口路径不同生成路径也改变了
第一个生成路径为PATH.distJsPath+"**/*.js"
第一个生成路径为PATH.distJsPath+"*.js"


入坑5：：
.pipe(webpack({
	entry:{
		lib:["react","react-dom","jquery"],
		main:PATH.compileJsPath+"active.js",
	},
	output:{
                path:PATH.distJsPath,
                filename:"[name].js",
       },
       ....
 webpack entry 如果多个配置这里是花括弧{}，如果是一个配置，可以用数组[],但是一旦乱用就会出错
 入坑6：：
 
 package.json文件里面严格遵守json书写格式，紧跟着最后花括弧的那个数据后面不能有逗号，否则也会报错！
 
