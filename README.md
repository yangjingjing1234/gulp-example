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
